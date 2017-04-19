# Heuristic Analysis

All problems are in the Air Cargo domain.  They have the same action schema defined,
but different initial states and goals.

## Air Cargo Action Schema:
```
Action(Load(c, p, a),
	PRECOND: At(c, a) ∧ At(p, a) ∧ Cargo(c) ∧ Plane(p) ∧ Airport(a)
	EFFECT: ¬ At(c, a) ∧ In(c, p))
Action(Unload(c, p, a),
	PRECOND: In(c, p) ∧ At(p, a) ∧ Cargo(c) ∧ Plane(p) ∧ Airport(a)
	EFFECT: At(c, a) ∧ ¬ In(c, p))
Action(Fly(p, from, to),
	PRECOND: At(p, from) ∧ Plane(p) ∧ Airport(from) ∧ Airport(to)
	EFFECT: ¬ At(p, from) ∧ At(p, to))
```

## Problem 1

### Definition

#### Initial state

```
Init(At(C1, SFO) ∧ At(C2, JFK)
	∧ At(P1, SFO) ∧ At(P2, JFK)
	∧ Cargo(C1) ∧ Cargo(C2)
	∧ Plane(P1) ∧ Plane(P2)
	∧ Airport(JFK) ∧ Airport(SFO))
```

#### Goal
```
Goal(At(C1, JFK) ∧ At(C2, SFO))
```

### Optimal plan

The optimal plan for the problem 1 has 6 steps which can be the following:

```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Fly(P1, SFO, JFK)
Fly(P2, JFK, SFO)
Unload(C1, P1, JFK)
Unload(C2, P2, SFO)
```

### Search algorithms results

| Algorithm                           | Expansions |  Goal Tests |  New Nodes | Plan length | Time elapsed (secods) |
|-------------------------------------|------------|-------------|------------|-------------|-----------------------|
| Breadth First Search                |    43      |       56    |    180     |     6       |       0.031616        |
| Depth First Search                  |    21      |       22    |     84     |    20       |       0.014577        |
| Uniform Cost Search                 |    55      |       57    |    224     |     6       |       0.039915        |
| A* Search with Ignore Preconditions |    55      |       57    |    224     |     6       |       0.051789        |
| A* Search with PG Level Sum         |    11      |       13    |     50     |     6       |       2.085718        |

### Analysis


## Problem 2

### Definition

#### Initial state
```
Init(At(C1, SFO) ∧ At(C2, JFK) ∧ At(C3, ATL)
	∧ At(P1, SFO) ∧ At(P2, JFK) ∧ At(P3, ATL)
	∧ Cargo(C1) ∧ Cargo(C2) ∧ Cargo(C3)
	∧ Plane(P1) ∧ Plane(P2) ∧ Plane(P3)
	∧ Airport(JFK) ∧ Airport(SFO) ∧ Airport(ATL))
```

#### Goal
```
Goal(At(C1, JFK) ∧ At(C2, SFO) ∧ At(C3, SFO))
```

## Optimal plan

The optimal plan for the problem 2 has 9 steps which can be the following:

```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Load(C3, P3, ATL)
Fly(P1, SFO, JFK)
Fly(P2, JFK, SFO)
Fly(P3, ATL, SFO)
Unload(C3, P3, SFO)
Unload(C2, P2, SFO)
Unload(C1, P1, JFK)
```

### Search algorithms results

| Algorithm                           | Expansions |  Goal Tests |  New Nodes | Plan length | Time elapsed (secods) |
|-------------------------------------|------------|-------------|------------|-------------|-----------------------|
| Breadth First Search                |    3343    |     4609    |   30509    |      9      |       13.57252        |
| Depth First Search                  |     624    |      625    |    5602    |    619      |        3.35698        |
| Uniform Cost Search                 |    4853    |     4855    |   44041    |      9      |       42.34409        |
| A* Search with Ignore Preconditions |    4853    |     4855    |   44041    |      9      |      51.630905        |
| A* Search with PG Level Sum         |      86    |       88    |     841    |      9      |      178.35878        |

### Analysis


## Problem 3

### Definition

#### Initial state
```
Init(At(C1, SFO) ∧ At(C2, JFK) ∧ At(C3, ATL) ∧ At(C4, ORD)
	∧ At(P1, SFO) ∧ At(P2, JFK)
	∧ Cargo(C1) ∧ Cargo(C2) ∧ Cargo(C3) ∧ Cargo(C4)
	∧ Plane(P1) ∧ Plane(P2)
	∧ Airport(JFK) ∧ Airport(SFO) ∧ Airport(ATL) ∧ Airport(ORD))
```

#### Goal
```
Goal(At(C1, JFK) ∧ At(C3, JFK) ∧ At(C2, SFO) ∧ At(C4, SFO))
```


## Optimal plan

The optimal plan for the problem 3 has 12 steps which can be the following:

```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Fly(P1, SFO, ATL)
Load(C3, P1, ATL)
Fly(P2, JFK, ORD)
Load(C4, P2, ORD)
Fly(P2, ORD, SFO)
Fly(P1, ATL, JFK)
Unload(C4, P2, SFO)
Unload(C3, P1, JFK)
Unload(C2, P2, SFO)
Unload(C1, P1, JFK)
```

### Search algorithms results

| Algorithm                           | Expansions |  Goal Tests |  New Nodes | Plan length | Time elapsed (secods) |
|-------------------------------------|------------|-------------|------------|-------------|-----------------------|
| Breadth First Search                |   14663    |    18098    |  129631    |     12      |       92.98073        |
| Depth First Search                  |     408    |      409    |    3364    |    392      |        1.65374        |
| Uniform Cost Search                 |   18223    |    18225    |  159618    |     12      |      355.57375        |
| A* Search with Ignore Preconditions |   18223    |    18225    |  159618    |     12      |     416.610795        |
| A* Search with PG Level Sum         |     414    |      416    |    3818    |     12      |    1214.164300        |

### Analysis
