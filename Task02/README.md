# Task 2 – From requirement to hierarchy

## Relationships
- `Student is-a Person`: public, single inheritance.
- `Staff is-a Person`: public, single inheritance.
- `TeachingAssistant is-a Student` and `is-a Staff`: public multiple inheritance; combined structure is hybrid.
- `ResearchScholar is-a Student`: public multilevel inheritance.
- `Person has-a Address` and `Student has-a Course` would be composition/member-class relationships (not inheritance); these can be added as value members.

## Diamond problem
Without virtual inheritance, `TeachingAssistant` contains one `Person` through `Student` and another through `Staff`. A reference to `name` or `id` becomes ambiguous and duplicates the common identity. `virtual public Person` makes the shared Person a virtual base, so the most-derived `TeachingAssistant` constructs exactly one Person subobject.

## Access table (Person member visibility inside Student)
| Person member | public inheritance | protected inheritance | private inheritance |
|---|---|---|---|
| public | public | protected | private |
| protected | protected | protected | private |
| private | inaccessible | inaccessible | inaccessible |

## Prediction for the supplied virtual-base program
```text
Person Student Staff TA
```
The virtual base is constructed once by the most-derived object before its direct non-virtual bases. Removing `virtual` gives two Person subobjects; typical output becomes `Person Student Person Staff TA` (the exact base construction order follows the listed base order). Access to a duplicated `Person` member through the diamond is ambiguous. There is normally no compiler error merely from declaring the hierarchy; an ambiguous member use triggers a diagnostic.

## Composition alternative
A `TeachingAssistant` containing separate `Student` and `Staff` members has-a rather than is-a relationships. Each member contains its own Person subobject, so there are two identities unless a shared Person member is separately designed. Access is explicit (`ta.student.name`); there is no inherited-name ambiguity, but the object is not substitutable for Student or Staff. `sizeof` is compiler/platform dependent; compare the measured values on your compiler.
