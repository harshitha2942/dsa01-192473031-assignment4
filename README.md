# DSA01-RegisterNumber-Assignment4
## Assignment 4 – CO4: Designing Reusable Class Hierarchies

**Student name:** YOUR NAME  
**Register number:** YOUR REGISTER NUMBER  
**Compiler:** GNU g++ (record exact version with `g++ --version`)  
**Language standard:** C++17

## Contents
- `Task01`: payroll class hierarchy and polymorphic pay
- `Task02`: university people hierarchy and virtual diamond
- `Task03`: derived/member class construction, destruction and completed TODO
- `Task04`: derived pointers, virtual functions, virtual destructor and slicing
- `Task05`: object pointers, references, `this`, method chaining and completed TODOs
- `Task06`: extensible vehicle rental hierarchy and new ElectricBus type
- `scripts`: build/run helpers

## Compile and run
From the repository root:
```bash
g++ --version
g++ -std=c++17 -Wall -Wextra -pedantic Task01/main.cpp -o Task01/task01
./Task01/task01
```
Compile each task similarly. On Windows PowerShell use `.\Task01\task01.exe`.

Compile Task04 prediction program:
```bash
g++ -std=c++17 -Wall -Wextra -pedantic Task04/predict.cpp -o Task04/predict
./Task04/predict
```
Compile Task03 completed TODO program:
```bash
g++ -std=c++17 -Wall -Wextra -pedantic Task03/complete_code.cpp -o Task03/complete
./Task03/complete
```
Compile Task05 completed TODO program:
```bash
g++ -std=c++17 -Wall -Wextra -pedantic Task05/complete_code.cpp -o Task05/complete
./Task05/complete
```

## Results summary
1. Common payroll data is moved into an abstract `Staff` base class; pay is polymorphic.
2. Student and Staff virtually inherit Person to resolve the diamond; TeachingAssistant has one Person base.
3. Constructors initialise bases and member objects in the required order; destructors run in reverse order.
4. Virtual dispatch and virtual destruction repair the Account hierarchy; the slicing example is isolated in a prediction program.
5. Cart supports direct, pointer and reference access; `this` enables chaining; pointer iteration finds the highest total.
6. Abstract Vehicle hierarchy supports different charge rules and adding ElectricBus without changing fleet traversal.

## Submission evidence still required
- Replace the placeholder student identity and repository name.
- Execute all programs on your own system and capture genuine terminal screenshots.
- Record your exact compiler version and commands.
- Record predictions before running the two supplied prediction programs.
- Run the relevant sanitizer experiments and save actual reports.
- Record `sizeof` results, warnings and any platform-dependent measurements.
- Commit progressively, at least one commit per task; do not upload everything in one final commit.
- Share the repository with faculty and put its working URL on the report cover page.

## Suggested progressive commits
```bash
git init
git add README.md Task01
git commit -m "Complete Task 1 class hierarchy review"
git add Task02 && git commit -m "Complete Task 2 virtual inheritance"
git add Task03 && git commit -m "Complete Task 3 constructors and member classes"
git add Task04 && git commit -m "Complete Task 4 polymorphism and slicing"
git add Task05 && git commit -m "Complete Task 5 pointers and this pointer"
git add Task06 && git commit -m "Complete Task 6 vehicle fleet hierarchy"
git branch -M main
git remote add origin YOUR_GITHUB_REPOSITORY_URL
git push -u origin main
```
"# dsa01-192473031-assignment4" 
