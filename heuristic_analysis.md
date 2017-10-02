# Heuristic analysis

Following scores were tested:

1. Difference between my and opponent moves, given more weight to opponent
2. Simple number of my moves
3. Distance to opponent (closer is better)

Obtained results:

| Match # |   Opponent  | AB_Improved | AB_Custom | AB_Custom_2 | AB_Custom_3 |
|:-------:|:-----------:|:-----------:|:---------:|:-----------:|:-----------:|
|    _    |      _      |   Won/Lost  |  Won/Lost |   Won/Lost  |   Won/Lost  |
|    1    |    Random   |    7 - 3    |   8 - 2   |    6 - 4    |    8 - 2    |
|    2    |   MM_Open   |    6 - 4    |   8 - 2   |    6 - 4    |    8 - 2    |
|    3    |  MM_Center  |    9 - 1    |   8 - 2   |    8 - 2    |    8 - 2    |
|    4    | MM_Improved |    6 - 4    |   4 - 6   |    6 - 4    |    5 - 5    |
|    5    |   AB_Open   |    5 - 5    |   6 - 4   |    5 - 5    |    7 - 3    |
|    6    |  AB_Center  |    7 - 3    |   6 - 4   |    8 - 2    |    6 - 4    |
|    7    | AB_Improved |    5 - 5    |   7 - 3   |    5 - 5    |    5 - 5    |
|    _    |      _      |      _      |     _     |      _      |      _      |
|    _    |  Win Rate:  |    64.3%    |   67.1%   |    62.9%    |    67.1%    |

As we see the winner is `AB_Custom`, basically it is the same as `AB_Improved` but a bit more sensitive to opponents well-being.

`AB_Custom_2` performed slightly worse than `AB_Improved` as it is quite simple and does not consider opponents position.

Surprisingly strategy to be closer to opponent (`AB_Custom_3`) performed well and on par with `AB_Custom`. Well, some say too keep enemies close, in this case it turns out to be true.