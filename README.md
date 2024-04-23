# MIA Helper Scripts # mia-helper-scripts
Scripts to make using MIA (mapping-iterative-assembler) easier

## Intro

I like using [MIA](https://github.com/mpieva/mapping-iterative-assembler/) to assemble mitogenomes, and so does a lot of other people. One barrier of entry to using MIA is that its manual is very limited, and the output most users desire (a consensus FASTA file) is not very easily produced. This repository aims at making it easier for users to use MIA and get the results they need.

## Obtaining a consensus FASTA file from MIA

[MIA](https://github.com/mpieva/mapping-iterative-assembler/) outputs a `maln` file. The file name is usually `assembly.maln.iter`, where `iter` is the number of iterations MIA took to produce the final file. It will look like `assembly.maln.3`, for example, if it took 3 iterations. In order to create a consensus FASTA file, most people a second program that comes packaged with MIA, `ma`. `ma` can parse the `maln` file and is able to create many different outputs.

To use the `create_fasta_from_mia.py` script you'll need to first create a `.41` file. You can do that this way:

```
ma -M assembly.maln.3 -f 41 > assembly.41
```
Of course, replace `assembly.maln.3` with your file name. One you have your `assembly.41` file you're ready to use `create_fasta_from_mia.py`.

The simplest way to run the script is:

```
python create_fasta_from_mia.py -m assembly.41
```

The script has a number of default paramters que that can be changed:

```
  -c COVERAGE, --coverage COVERAGE
                        Coverage cutoff; default = 3
  -I ID, --id ID        ID to assign; default is the name of the output FASTA file (without the .fasta extension)
  -p PERCENT, --percent PERCENT
                        Percentage of agreement of the base called; default = 0.66
  -q QUALITY, --quality QUALITY
                        Aggregate score quality cutoff; default = 40
  -m INPUT, --input INPUT
                        Input .41 file
  -o OUTPUT, --output OUTPUT
                        Output .fasta file
```

If you don't provide any parameters, it will create the FASTA file using a 3x minimum coverage for each ste that also has a quality score >40. The default file name and sequence name inside the FASTA file is whatever you name your `assembly.41` file, minus the file extensions.

