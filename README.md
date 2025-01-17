Scihub Downloader (forked from [Scihub.py](https://github.com/zaytoun/scihub.py))
[![Python](https://img.shields.io/badge/Python-3%2B-blue.svg)](https://www.python.org)
=======
### About this fork
I forked this so I could adapt the script to some of my needs.
Particularly, now when I pass the argument `-f`or `--file`, it looks for a file in this format:
```
https://doi.org/10.1016/0024-3841(49)90091-1, Title 1
https://doi.org/10.1016/0024-3841(49)90090-X, Title 2
https://doi.org/10.1016/0024-3841(49)90089-3, Title 3
```
It then proceeds to download the files whose DOI are specified in the file (just as it would in [Scihub.py](https://github.com/zaytoun/scihub.py)), and then rename the PDF to the Title found in the right side of the comma.

In case you're interested, I also wrote a couple scripts and named them [Crossref Metadata Extractor](https://github.com/ezxpro/Crossref-Metadata-Extractor). This one is able to fetch the metadata of all issues of a given serial publication (e.g a journal) using its [ISSN code](https://en.wikipedia.org/wiki/ISSN) from the [https://www.crossref.org](Crossref) database, using the [CrossRef Unified Resource API](https://api.crossref.org/swagger-ui/index.html).
It is then possible to convert the output to a text file like the one above, allowing one to download serial publications from Sci-Hub in bulk.

Original description (Scihub.py)
--------
scihub.py is an unofficial API for Sci-hub. scihub.py can search for papers on Google Scholars and download papers from Sci-hub. It can be imported independently or used from the command-line.

If you believe in open access to scientific papers, please donate to Sci-Hub.

Features
--------
* Download specific articles directly or via Sci-hub
* Download a collection of articles by passing in file of article identifiers
* Search for articles on Google Scholars and download them

**Note**: A known limitation of scihub.py is that captchas show up every now and then, blocking any searches or downloads.

Setup
-----
```
pip install -r requirements.txt
```

Usage
------
You can interact with scihub.py from the commandline:

```
usage: scihub.py [-h] [-d (DOI|PMID|URL)] [-f path] [-s query] [-sd query]
                 [-l N] [-o path] [-v]

SciHub - To remove all barriers in the way of science.

optional arguments:
  -h, --help            show this help message and exit
  -d (DOI|PMID|URL), --download (DOI|PMID|URL)
                        tries to find and download the paper
  -f path, --file path  pass file with list of identifiers and download each
  -s query, --search query
                        search Google Scholars
  -sd query, --search_download query
                        search Google Scholars and download if possible
  -l N, --limit N       the number of search results to limit to
  -o path, --output path
                        directory to store papers
  -v, --verbose         increase output verbosity
  -p, --proxy           set proxy
```

You can also import scihub. The following examples below demonstrate all the features.

### fetch

```
from scihub import SciHub

sh = SciHub()

# fetch specific article (don't download to disk)
# this will return a dictionary in the form 
# {'pdf': PDF_DATA,
#  'url': SOURCE_URL,
#  'name': UNIQUE_GENERATED NAME
# }
result = sh.fetch('http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=1648853')
```

### download

```
from scihub import SciHub

sh = SciHub()

# exactly the same thing as fetch except downloads the articles to disk
# if no path given, a unique name will be used as the file name
result = sh.download('http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=1648853', path='paper.pdf')
```

### search

```
from scihub import SciHub

sh = SciHub()

# retrieve 5 articles on Google Scholars related to 'bittorrent'
results = sh.search('bittorrent', 5)

# download the papers; will use sci-hub.io if it must
for paper in results['papers']:
	sh.download(paper['url'])

```
License
-------
MIT










