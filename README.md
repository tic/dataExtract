# Data extraction using Stanford NER

This repository is fundamentally identical to the Stanford NER repository. I have updated it to have an I/O interface that is better suited to my needs (web scraping). The setup process is identical to the original project, but running it is different.

## Changes

1. Input data is specified as a command-line argument rather than a path to a text file containing the input data. Use the `-s` or `--string` flag to provide your input. Examples:
```bash
python main.py -s "Google bought IBM for 10 dollars. Mike was happy about this deal."
python main.py --string "Google bought IBM for 10 dollars. Mike was happy about this deal."
```

2. Output is no longer written to a text file. It is instead printed to stdout as the script runs. Such output can be programmatically captured in a number of ways including piping it into a text file, if that is needed.

3. Output format is different. For both of the above examples, this *string* would be printed to the first line of stdout:
`[["Google", "ORGANIZATION"], ["IBM", "ORGANIZATION"], ["10 dollars", "MONEY"], ["Mike", "PERSON"]]`

As you can see, the output is formatted as an array of two-element arrays. Each sub-array contains a piece of data, and what data type the program classified it as.

4. Arbitrarily many input strings may be provided and they will be parsed and output individually each on a new line of stdout. Example:
Input: `python main.py -s "Hello John, this is Todd speaking" -s "today I went to sleep at 21:00"`

Output:
```
[['Todd', 'PERSON']]
[['today', 'DATE'], ['21:00', 'TIME']]
```

Notice each command-line flag has its results placed on a different stdout line. Consider parsing the result of multiple flags with something like `output.split("\n")`.

## Housekeeping

The original `README.md` is presented after this text.

------------------------------------------------------------------------
------------------------------------------------------------------------

# Python wrapper for Stanford NER

The unofficial cross-platform Python wrapper for the <b>state-of-art</b> named entity recognition library from Stanford University.

Input: `Google bought IBM for 10 dollars. Mike was happy about this deal.`

Output:
```
Google              	ORGANIZATION
IBM                 	ORGANIZATION
10 dollars          	MONEY
Mike                	PERSON
```

NOTE: It works well on Linux and Ubuntu but it's unclear for Windows.

## About Stanford NER

Named Entity Recognition (NER) labels sequences of words in a text which are the names of things, such as person and company names, or gene and protein names. It comes with well-engineered feature extractors for Named Entity Recognition, and many options for defining feature extractors. Included with the download are good named entity recognizers for English, particularly for the 3 classes (PERSON, ORGANIZATION, LOCATION).

More information can be found here : https://nlp.stanford.edu/software/CRF-NER.shtml

## Installation

First of all, make sure Java 1.8 is installed. Open a terminal and run this command to check:

```bash
java -version
```

If this is not the case and if your OS is Ubuntu, you can install it this way:

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

The code can be invoked either programmatically or through the command line. The program can be invoked with the following commands:

```bash
git clone https://github.com/philipperemy/Stanford-NER-Python.git
cd Stanford-NER-Python
chmod +x init.sh
./init.sh # will run this example above.
```

## Usage

#### Command
```bash
echo "Google bought IBM for 10 dollars. Mike was happy about this deal." > input.txt
python main.py -f input.txt
```

#### Output

```
Google              	ORGANIZATION
IBM                 	ORGANIZATION
10 dollars          	MONEY
Mike                	PERSON
```

## Support

Just open an issue. Any contributions are welcomed!
