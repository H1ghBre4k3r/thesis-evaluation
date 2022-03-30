# Bachelor Thesis Evaluation

This is the repo containing all my evaluation resuluts (or rather the results of all my simulation runs). The source code for my simulation can be found [here](https://github.com/H1ghBre4k3r/swarm-simulation).

## Structure

Each folder in this repo contains different (but important) files:

-   [original](original): Results for executing ORCA without my changes
-   [improved](improved): Results for executing ORCA with my changes
-   [increased_tau](increased_tau): Some files, where i tested different values for tau (not really needed)
-   [scripts](scripts): Folder containing some scripts for generating fancy graphs

## Scripts

I provided several scripts to easily generate fancy graphs from all the data.

### Summary

To summarize all data in a certain subfolder, i provided a script:

```sh
$ ./scripts/sum-evaluations.py -d improved -o summary.json
```

It accepts 2 parameters:

-   `-d`: directory to take files from
-   `-o`: name for output file

### Graph By Noise

To generate a graph by noise, you can use `scripts/generate-graph-by-noise.py`:

```sh
$ ./scripts/generate-graph-by-noise.py -f summary.json -p 8 16 32 64 -m runtime -d ticks -t 100 -xlabel "Average Inaccuracy [meter]" -ylabel "N° Of Ticks Until Reaching Target" -l participants -s 1 -ci 0.95
```

It accepts several parameters:

-   `-h`: show help message and exit
-   `-f <string>`: Path to file
-   `-o <string>`: Path to output file
-   `-p int [int, ...]`: Different numbers of participants you want to plot
-   `-c`: Flag for evaluating shared state (default: False)
-   `-m {runtime,collisions}`: Mode: runtime or collisions
-   `-d <string>`: Name of detail
    -   the options depend on the mode:
        -   `runtime`:
            -   `avg`: average computing time
            -   `ticks`: total ticks
            -   `duration`: total runtime
        -   `collisions`:
            -   `total`: total number of collisions
            -   `avg`: average number of collisions
            -   `most`: most number of collisions
            -   `least`: least number of collisions
-   `-s <float>`: Scale for values on Y-axis
-   `-ci <float>`: Confidence interval for graph
-   `-t <int>`: Value of tau to plot
-   `-l <string>`: Label for each line in the legend
-   `-xlabel <string>`: Label for x-axis
-   `-ylabel <string>`: Label for y-axis

### Compare Scenarios

If you want to compare two different (summarized - using `scripts/sum-evaluations.py`) scenarios by a certain detail, you can use `scripts/compare.py`:

```sh
$ ./scripts/compare.py -f original-summary.json summary.json -p 32 -t 100 -xlabel "Average Inaccuracy [meter]" -l "Original Algorithm" "Improved Algorithm" -s 1 -ci 0.95 -m runtime -d ticks -ylabel "N° Of Ticks Until Reaching Target" -o comparison-ticks.pdf
```

-   `-h`: show help message and exit
-   `-f <string> [<string>, ...]`: Paths to files you want to compare
-   `-o <string>`: Path to output file
-   `-p <int>`: The numbers of participants you want to plot
-   `-c`: Flag for evaluating shared state (default: False)
-   `-m {runtime,collisions}`: Mode: runtime or collisions
-   `-d <string>`: Name of detail
    -   the options depend on the mode:
        -   `runtime`:
            -   `avg`: average computing time
            -   `ticks`: total ticks
            -   `duration`: total runtime
        -   `collisions`:
            -   `total`: total number of collisions
            -   `avg`: average number of collisions
            -   `most`: most number of collisions
            -   `least`: least number of collisions
-   `-s <float>`: Scale for values on Y-axis
-   `-ci <float>`: Confidence interval for graph
-   `-t <int>`: Value of tau to plot
-   `-l <string>`: Label for each line in the legend
-   `-xlabel <string>`: Label for x-axis
-   `-ylabel <string>`: Label for y-axis
