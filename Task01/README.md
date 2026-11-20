# Task 1 – Class design review

## Diagnosis of the supplied design
1. `name`, `id` and basic pay are duplicated.
2. Data members are public, so invalid values can be written without validation.
3. The same concepts use inconsistent names (`name`/`nm`, `id`/`code`).
4. `da` is declared but never used.
5. `0.42` is a magic number with no named policy.
6. Adding a staff type requires another unrelated class and more caller-side branching.
7. Different classes cannot be handled uniformly in one polymorphic loop.

## Repaired design
`Staff` is an abstract base class holding common identity. Each derived class overrides `pay()` and `role()`. Payroll stores owning `unique_ptr<Staff>` values and calls virtual functions.

```text
              Staff (abstract)
              /      |       \
       Professor  LabAssistant  GuestFaculty
```

## Design defence (under 100 words)
The hierarchy puts shared identity and the common interface in `Staff`, while each derived class owns only the data needed for its pay rule. A payroll collection can store base-class pointers and call `pay()` without checking the concrete type. To add a new category, create a derived class and override the required functions; existing payroll-loop code remains unchanged. This follows the Open/Closed Principle and avoids duplicated fields and type-code switches.

## Alternative: one Staff class plus a switch
A single class would need a type code and fields for every category, with a `switch` in `pay()`. Both approaches take O(1) time per pay calculation. The single class wastes space on fields unused by many objects. Adding a category requires editing the enum/type code, data representation, switch, construction logic and often reporting code; the polymorphic design adds a new derived class.
