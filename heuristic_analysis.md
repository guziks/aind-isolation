# Heuristic analysis

Following scores were tested:

1. Difference between my and opponent moves, given more weight to opponent
2. Difference between my and opponent moves with penalty near borders
3. Distance to opponent (closer is better)

Obtained results after performing 100 matches:

| Match # |   Opponent  | AB_Improved | AB_Custom | AB_Custom_2 | AB_Custom_3 |
|:-------:|:-----------:|:-----------:|:---------:|:-----------:|:-----------:|
|    _    |      _      |   Won/Lost  |  Won/Lost |   Won/Lost  |   Won/Lost  |
|    1    |    Random   |   163 - 37  |  165 - 35 |   164 - 36  |   162 - 38  |
|    2    |   MM_Open   |   129 - 71  |  128 - 72 |   134 - 66  |   131 - 69  |
|    3    |  MM_Center  |   158 - 42  |  156 - 44 |   155 - 45  |   151 - 49  |
|    4    | MM_Improved |   125 - 75  |  120 - 80 |   130 - 70  |   117 - 83  |
|    5    |   AB_Open   |   106 - 94  |  101 - 99 |   106 - 94  |   96 - 104  |
|    6    |  AB_Center  |   122 - 78  |  104 - 96 |   107 - 93  |   112 - 88  |
|    7    | AB_Improved |   96 - 104  |  97 - 103 |   95 - 105  |   90 - 110  |
|    _    |      _      |      _      |     _     |      _      |      _      |
|    _    |  Win Rate:  |    64.2%    |   62.2%   |    63.6%    |    61.4%    |

## Observation

All evaluation functions performed very close to each other. `AB_Custom_2` closest to reference `AB_Improved` with win rate differences:

- overall: 0.6% (64.2-63.6)
- against each other: 5% ((105-95)/200)

## Analysis

All of tested evaluation functions are fast to compute. Semantically:

- `AB_Custom` not much different to `AB_Improved`, a bit more sensitive to opponent, as a result - no noticeable gain.
- `AB_Custom_2` tries to avoid borders of a field in a middle of a game with assumption that borders reduce mobility. Achieves results comparable with `AB_Improved`.
- `AB_Custom_3` tries to be as close to opponent as possible. Assumption - this could work like in regular (not L shaped) isolation game. Overall performed 2.8% worse than `AB_Improved`.

## Conclusion

Among tested evaluation functions #2 performed best and it is recommended.