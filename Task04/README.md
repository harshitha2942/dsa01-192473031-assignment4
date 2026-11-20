# Task 4 – Pointers to derived classes: forensics

## Defects in the supplied code
1. `rate()` is non-virtual, so `Account*` calls `Account::rate()` (static binding).
2. `Account` has a non-virtual destructor; deleting a `SeniorAccount` through `Account*` is undefined behaviour and may skip the derived destructor, leaking `history`.
3. `Account copy = SeniorAccount();` slices the derived object: only the Account base subobject is copied, so derived state and dynamic type are lost.

## Repair
Make the polymorphic operation virtual, use `override` in derived classes, give a polymorphic base a virtual destructor, and store owning pointers such as `unique_ptr<Account>` rather than values. `main.cpp` demonstrates this repair.

## Prediction for supplied program
```text
3.5 4 3.5
```
`p->rate()` is bound at compile time using static type `Account*`; `p->vrate()` dispatches at run time to `SeniorAccount`; `copy.vrate()` calls Account because `copy` is a sliced Account object.

## Alternative
`vector<unique_ptr<Account>>` owns objects and destroys them automatically. Processing n accounts is O(n), with O(n) pointer storage plus each object. Smart pointers prevent forgotten deletes and make ownership clearer, but they do not prevent non-virtual dispatch or object slicing if code still copies derived objects into base values.
