# Heuristic analysis

Following scores were tested:

1. Difference between my and opponent moves, given more weight to opponent
2. Difference between my and opponent moves with penalty near borders
3. Distance to opponent (closer is better)

Obtained results after performing 100 matches:

| Match # |   Opponent  | AB_Improved | AB_Custom | AB_Custom_2 | AB_Custom_3 |
|:-------:|:-----------:|:-----------:|:---------:|:-----------:|:-----------:|
|    _    |      _      |   Won/Lost  |  Won/Lost |   Won/Lost  |   Won/Lost  |
|    1    |    Random   |    153-47   |   169-31  |    163-37   |    169-31   |
|    2    |   MM_Open   |    131-69   |   127-73  |    133-67   |    122-78   |
|    3    |  MM_Center  |    153-47   |   151-49  |    150-50   |    156-44   |
|    4    | MM_Improved |    135-65   |   128-72  |    134-66   |    128-72   |
|    5    |   AB_Open   |    106-94   |   105-95  |    111-89   |    98-102   |
|    6    |  AB_Center  |    117-83   |   120-80  |    120-80   |    111-89   |
|    7    | AB_Improved |    96-104   |   107-93  |    102-98   |    94-106   |
|    _    |      _      |      _      |     _     |      _      |      _      |
|    _    |  Win Rate:  |    63.6%    |   64.8%   |    65.2%    |    62.7%    |

## Observation

All evaluation functions performed very close to each other. `AB_Custom_2` and `AB_Improved` are closest opponents with win rate differences:

- overall: 1.6% (65.2-63.6)
- against each other: 2% ((102-98)/200)

## Analysis

All of tested evaluation functions are fast to compute. Results comparison to `AB_Improved`:

- `AB_Custom` a bit more sensitive to opponent version of `AB_Improved`. Result: 1.2% better (64.8-63.6).
- `AB_Custom_2` tries to avoid borders of a field in a middle of a game with assumption that borders reduce mobility. Result: 1.6% better (65.2-63.6).
- `AB_Custom_3` tries to be as close to opponent as possible with assumption that this could work like in regular (not L shaped) isolation game. Result: 0.9% worse (63.6-62.7)

Average depth of search was measured for:

- `AB_Improved`: 6.6
- `AB_Custom_2`: 6.5

## Conclusion

Among tested evaluation functions #2 performed best and it is recommended, reasons:

- win rate is 1.6% higher compared to `AB_Improved`
- despite average depth is 0.1 (6.6-6.5) less compared to `AB_Improved` it manages to win, so it predicts game outcome better
- it is more complex to compute than `AB_Improved` (up to 3 additional multiplications and 5 comparisons) but not overly complicated (does not make additional game tree traverses)
- there is space for further tuning and improving