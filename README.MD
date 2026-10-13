# ESEP Grade Calculator

This library is a simple utility to calculate your grades.

A student can earn three kinds of grades in a course: assignments, exams, and essays. The
library averages each kind separately, multiplies each average by that kind's weight, adds
them together, and converts the result to a letter grade.

Current weights:

| Grade type | Weight |
| ---------- | ------ |
| Assignment | 50%    |
| Exam       | 35%    |
| Essay      | 15%    |

Grade scale:

| Numerical | Letter |
| --------- | ------ |
| 90 - 100  | A      |
| 80 - 89   | B      |
| 70 - 79   | C      |
| 60 - 69   | D      |
| below 60  | F      |

Passing the course requires a C or better.

The calculator also supports Pass/Fail evaluation. Pass the grading type you want to the
constructor: `LetterGrade` returns a letter from the scale above, `PassFail` returns "Pass"
for a 70 or better and "Fail" otherwise.

Runtime requirements:
Golang 1.24+

Project layout:
```
README.MD
grade-calculator/
    go.mod
    grade_calculator.go
    grade_calculator_test.go
```

Usage:
```go
gradeCalculator := esepunittests.NewGradeCalculator(esepunittests.LetterGrade)

gradeCalculator.AddGrade("open source assignment", 100, esepunittests.Assignment)
gradeCalculator.AddGrade("exam 1", 95, esepunittests.Exam)
gradeCalculator.AddGrade("essay on ai ethics", 91, esepunittests.Essay)

finalGrade := gradeCalculator.GetFinalGrade()
```

Run unit tests:
```
cd grade-calculator/
go test ./...
```

Run unit tests with verbose output so you can see each test name:
```
cd grade-calculator/
go test -v ./...
```

Run unit tests with code coverage:
```
cd grade-calculator/
go test -coverprofile=coverage.txt ./...
```

See which lines are and are not covered in the browser:
```
cd grade-calculator/
go tool cover -html=coverage.txt
```

Notes for the next person:
- The code lives in `grade-calculator/`, not `grade_calculator/`. Run the commands above from
  inside that folder or Go will not find the module.
- The package name is `esepunittests` even though the folder is `grade-calculator`.
- `computeAverage` divides by the number of grades, so adding a grade of every type before
  calling `GetFinalGrade` avoids a divide by zero.
