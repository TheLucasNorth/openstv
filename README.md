# openstv
A python3 port of the open source OpenSTV, https://github.com/Conservatory/openstv

This repository does not aim to add functionality, or even to reach true feature parity with the original OpenSTV. The aim is to maintain "good enough" python3 compatibility with the command line usage of OpenSTV as python 2 has now reached end-of-life.

## To use:

Clone this repository

Run the `runElection.py` file from the command line, adding flags as needed. EG, `python3 runElection.py ERS97STV "path to ballot file"`

You may need to install the future package, eg by running `python3 -m pip install future`

See below, or the included Help.html file, for information on ballot file formatting.

### Flags:

You can use flags to decide the report format, and the counting method.

#### Counting methods available:

    Approval
    Borda
    Bucklin
    CambridgeSTV
    Condorcet
    Coombs
    ERS97STV
    FTSTV // not currently working in python3
    GPCA2000STV
    IRV
    MeekNZSTV
    MeekQXSTV
    MeekSTV
    MinneapolisSTV
    NIrelandSTV
    QPQ
    RTSTV // not currently working in python3
    SNTV // not currently working in python3
    SanFranciscoRCV
    ScottishSTV
    SuppVote
    WarrenQXSTV
    WarrenSTV
    
The counting method must be stated before the path to the ballot file, and is required.
    
#### Report formats available:

    CsvReport
    HtmlReport
    MinimalReport
    TextReport
    YamlReport
    
The report format is set by using the flag `-r ReportFormat`, and should be declared before the counting method. For example, `python3 runElection.py -r HtmlReport ERS97STV "path to ballot file"`. If the flag is not provided, the results will be presented in the default format.
    
Depending on your use case, you may wish to change the default report format. You can set this in line 57 of runElection.py:

`reportformat = "TextReport"`

Simply change TextReport to the desired report format. It is also possible to customise the report formats by modifying the files in ReportPlugins.

### Ballot file format:

    4 2          # four candidates are competing for two seats
    -2           # Bob (candidate 2, as listed below) has withdrawn (optional)
    1 4 1 3 2 0  # first ballot
    1 2 4 1 3 0
    1 1 4 2 3 0  # The first number is the ballot weight (>= 1).
    1 1 2 4 3 0  # The last 0 is an end of ballot marker.
    1 1 4 3 0    # Numbers in between correspond to the candidates
    1 3 2 4 1 0  # on the ballot.
    1 3 4 1 2 0
    1 3 4 1 2 0  # Chuck, Diane, Amy, Bob
    1 4 3 2 0
    1 2 3 4 1 0  # last ballot
    0            # end of ballots marker
    "Amy"        # candidate 1
    "Bob"        # candidate 2
    "Chuck"      # candidate 3
    "Diane"      # candidate 4 (these do not have to be in alphabetical order)
    "Gardening Club Election"  # title, shown in results report
    
Ballots should be saved as .blt files, as this format is the most comprehensive and easiest to use, and support for .txt format ballots cannot be guaranteed. 
