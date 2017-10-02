# Deep Blue review

Paper describes another attempt (and this time successful) to build world-class chess machine capable of reliably beating Grandmaster human player. System has been built by IBM Research team during middle 1990s.

It did not appeared out of nothing but was next step in evolution of such systems. Notable design improvements are as follows:

- parallelism
- complex evaluation function
- good heuristics in form of best human player games database

From a hardware perspective system consisted of 30 nodes each with 16 specialized chess chips, each node had 1Gb of RAM and 4Gb of disk space.

Deep Blue team used many well known ideas such as quiescence search, iterative deepening, transposition tables as well as inventing new ones.

System had two major types of search: hardware and software.

Hardware search performed on a chess chip, used fixed depth search with quiescence and was relatively simple but fast; made only shallow (4-, 5-ply) searches.

As for software, new selective search was invented and called "dual credit with delayed extensions" search.

## Evaluation function

Interesting fact: despite system was massively parallel, overall efficiency of parallelism was not good at all (8 to 12%), so system was good largely because of big effort in tuning evaluation function and heuristics.

Evaluation function consisted of about 8000 features and were created not only manually but also using automated analysis tools.

## Heuristics

Previous revision of the system often loose to Grandmaster Joel Benjamin so he was chosen to to create an opening book of about 4000 positions. Moves of best played (during previous matches) games were prioritized.

Extended book mechanism was implemented, basically it was a 700000 game database. Moves made by Grandmasters were assigned bonuses to increase their priority after regular search.

Finally database of endgame (up to 6-piece) positions were available to each node. For every position this database holds "lose"/"does not lose" indicator which along with evaluation function is used to check if it is possible to cutoff search.