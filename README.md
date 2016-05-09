Disclaimer
----------
Copyright (c) 2016 Heinrich Widmann (DKRZ)

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

The python script mdmanager.py in this directory provide functionality required for ingestion (including OAI harvesting, semantic mapping and uploading to CKAN ) of metadata.

Preconditions
=============

Install required modules simplejson, sickle and e.g. by :
  > sudo pip install <module>

or just by installing all modules listed in requirements.txt :
  > less requirements.txt
  sickle
  lxml
  simplejson
  python-Levenshtein
  git+https://github.com/noumar/iso639.git

  > sudo pip install -r requirements.txt

Usage
=====
mdmanager.py [ OPTIONS ]


Description
===========
Management of meta data within EUDAT Joint Metadata Domain (JMD), i.e.
I.  Ingestion of meta data comprising
- 1. Harvesting of XML files from OAI-PMH MD provider(s)
- 2. Converting XML to Jason and semantic mapping of tags to CKAN fields
- 3. Uploading resulting JSON {key:value} dict's as datasets to JMD portal

Options
=======
--version               show program's version number and exit
--help, -h              show this help message and exit
--verbose, -v           increase output verbosity (e.g., -vv is more than -v)
--jobdir=JOBDIR          directory where log, error and html-result files are
                        stored. By default directory is created as
                        startday/starthour/processid .
--mode= h | harvest | c | convert | u | upload | h-c | c-u | h-u | h-d | d | delete
                         This can be used to do a partial workflow. If you use
                        converting without uploading the data will be stored
                        in .json files. Default is "h-u" which means a totally
                        ingestion with (h)arvesting, (c)onverting and
                        (u)ploading to a CKAN database.
--check_mappings=BOOLEAN
                        Check all mappings which are stored in './maptables/'
                        for converting the .xml in .json format and choose the
                        mapping table with the best results.
--community=STRING, -c STRING
                        community where data harvested from and uploaded to
--fromdate=DATE         Filter harvested files by date (Format: YYYY-MM-DD-hh-
                        mm-ss).
--epic_check=FILE       check and generate handles of CKAN datasets in handle
                        server EPIC and with credentials as specified in given
                        credstore file
--ckan_check=BOOLEAN    check existence and checksum against existing datasets
                        in CKAN database
--outdir=PATH, -d PATH  The absolute root dir in which all harvested files
                        will be saved. The converting and the uploading
                        processes work with the files from this dir. (default
                        is '/oaidata')
Multi Mode Options
------------------
Use these options if you want to ingest from a list in a file.

--list=FILE, -l FILE    list of OAI harvest sources (default is
                        ./harvest_list)
--parallel=PARALLEL     [DEPRECATED]

Single Mode Options
-------------------
Use these options if you want to ingest from only ONE source.

--source=PATH, -s PATH  A URL to .xml files which you want to harvest
--verb=STRING           Verbs or requests defined in OAI-PMH, can be
                        ListRecords (default) or ListIdentifers here
--mdsubset=STRING       Subset of harvested meta data
--mdprefix=STRING       Prefix of harvested meta data
--target_mdschema=STRING
                        Meta data schema of the target
Upload Options
--------------
These options will be required to upload an dataset to a CKAN database.

--iphost=IP, -i IP      IP adress of JMD portal (CKAN instance)
--auth=STRING           Authentification for CKAN APIs (API key, iby default
                        taken from file $HOME/.netrc)

Heinrich Widmann (DKRZ), 04.05.2016