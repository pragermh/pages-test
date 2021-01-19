Guide to ENA submission
=======================

This is a guide on how to submit sequence reads from environmental
samples to the [European Nucleotide Archive
(ENA)](https://www.ebi.ac.uk/ena/), provided by the [Swedish
Biodiversity Data Infrastructure (SBDI)](https://biodiversitydata.se/).
Our guide is largely a summary of [ENA's own extensive
instructions](https://ena-docs.readthedocs.io/en/latest/index.html),
with added pointers on issues specific to submission of metarbarcoding
data, as well as on more general matters that may confuse first-time
contributors. While ENA provides [three different routes for
submission](https://ena-docs.readthedocs.io/en/latest/general-guide.html),
we describe interactive submission only.

Preparation for submission
--------------------------

### Step 1: Prepare data and metadata

In ENA, raw sequencing output from a next generation platform, including
e.g. base calls and per-base quality scores, is called *reads* and is
accepted in [FASTQ, CRAM or BAM
format](https://ena-docs.readthedocs.io/en/latest/fileprep/reads.html).
Before submission, make sure that sequencing adapters have been removed
(*trimmed*), and that reads have been assigned to their sample of origin
(*demultiplexed*). In addition, gather all the information (*metadata*)
you have about how, when and where you acquired the samples and
generated the reads, as well as any contextual (environmental or
clinical) data that was collected during sampling (see [ENA's metadata
model](https://ena-docs.readthedocs.io/en/latest/general-guide/metadata.html)).

### Step 2: Register with ENA

To be able to submit data to ENA, you need to register an account. Go to
the [Interactive Webin submission service
page](https://www.ebi.ac.uk/ena/submit/sra/#home), select *Register* to
fill out the form, and submit your application. You will receive a
confirmation email with your account name.

Interactive submission
----------------------

### Step 1: Log in to submission portal

ENA provides two submission services: one for [test
submission](https://wwwdev.ebi.ac.uk/ena/submit/sra) and one for (real)
[production submission](https://www.ebi.ac.uk/ena/submit/sra). Make sure
that your data pass validation in the test procedure, before submitting
anything to the production environment. All test submissions are removed
the following day, but you will be able to download/upload most of the
input metadata as tab-separated text (\*.tsv) files, if you want to
continue testing at a later time without having to manually re-enter
everything (as explained below).

### Step 2: Register study

In the Webin submission portal, select the *New Submission | Register
study (project) | Next* to start filling out the Study form. In ENA, the
*study* object connects related samples and sequence reads (See step 4),
and is typically what you cite in publications (using the BioProject
accession number). For details on specific study attributes, see [ENA's
page on Study
edits](https://ena-docs.readthedocs.io/en/latest/update/metadata/interactive.html)
(points 5-7). Note that a single release date is set for all data within
a study, and that you thus may want to split sequenced batches of
samples into multiple ENA studies. After entering the required metadata
for a study, click *Submit | OK*. If successful, you will receive a
confirmation message, and should be able to see your study listed in the
*Studies* tab.

### Step 3: Register samples

Samples are the source material from which your sequences derive, and
the searchability and usability of your submitted data will depend on
how well you document these samples. Go back to the *New Submission* tab
and click *New Submission | OK | Register Samples | Next* to start the
process. While it is possible to download and edit metadata at different
steps of sample registration, we recommend doing so in step 3c.

#### Step 3a: Select sample checklist

The ENA sample checklists are partly overlapping sets of attributes (or
data fields) that can be used to describe samples, and by selecting one
of these you enable your sample metadata to be validated for correctness
during submission. For environmental and organismal (host-associated)
samples, alike, we recommend using one of the *Environmental Checklists*
and, among these, to select the alternative from the *Genomic Standards
Consortium (GSC) MIxS checklists* (described
[here](https://www.ebi.ac.uk/ena/submit/checklists) by GSC) that
provides the most specific match to your sampled environment, for
example:

![recommended checklists](/tables/recommended-checklists.csv)

Note that most GSC MIxS checklists have similar setups of mandatory and
recommended attributes, i.e. differ mainly in terms of which optional
attributes can be added and validated during submission. The
environmental attributes *altitude, elevation* and *depth*, are
mandatory only for some lists, however. Furthermore, the GSC MIxS built
environment list (not mentioned above) has several unique mandatories.

#### Step 3b: Add sample attributes

Once you have selected a checklist, you can inspect the attributes
available in that list. Mandatory and recommended attributes are
preselected, and you can add optional ones by ticking their boxes. We
suggest that you, at least, tick the following optional attributes for
metabarcoding data:

> file
> :   \_static/tables/optional-fields.csv
>
> header-rows
> :   1
>
To ensure that metadata are validated and searchable, you should use
existing attributes whenever possible, but you can also add custom
attributes to describe your data, if needed. Adding more than a few of
these is easier to do in a spreadsheet, though, and we explain how to do
that in the next step.

#### Step 3c: Create spreadsheet template

After selecting optional attributes, click the *Download Spreadsheet*
button (at the bottom of the form) to download a tab-separated values
(\*.tsv) file. Open the file in your spreadsheet application of choice
(In MS Excel, click *Data | Text to Columns | Delimited | Delimiter:
Tab*, to separate text into columns, if needed). With the added optional
attributes from 3b, a template created from the *GSC MIxS water*
checklist should look like this:

> file
> :   \_static/tables/sample-template.csv
>
> header-rows
> :   0
>
#### Step 3d: Edit spreadsheet structure

In the downloaded spreadsheet, you can add custom attributes (with
units, where applicable) to the right of existing columns, and samples
below the row starting with *\#units*. For instance, if you add two
custom attributes (*sampling\_station\_id* and *current\_velocity
[cm/s]*), and three samples (*xyz:1:01*, *xyz:1:02* and *xyz:1:03*) to
the template from Step 3c, your spreadsheet structure should look like
this:

> file
> :   \_static/tables/edited-sample-template.csv
>
> header-rows
> :   0
>
Note that *environmental package* refers to the checklist you selected
in Step 3a, e.g. if you selected the GSC MixS water list one of your
attributes will be called *water environmental package* and the value
for that column should be *water* in each of your sample rows.

#### Step 3e: Add sample metadata

Before adding actual sample metadata to your spreadsheet, take a close
look at ENA's explanations of the selected attributes (provided in the
list where you ticked optional attributes), but also note the following:

-   **Taxon attributes have unintuitive meaning for environmental
    samples**. For metabarcoding data, the *tax\_id* &
    *scientific\_name* attributes do not refer to the sequenced
    organisms, but instead *specify the sampled environment*. A *spider
    metagenome* is, for example, meant to describe samples for which a
    spider or spider body part (e.g. gut) is the *environment*, i.e. not
    samples from which you have derived spider sequences. The attributes
    *tax\_id* & *scientific\_name* should thus be selected from the list
    of [environmental and organismal metagenomes in NCBI's taxonomy
    browser](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?id=408169),
    and *common\_name* should be left empty. For host-associated
    samples, also differentiate between these generic attributes (i.e.
    *tax\_id* & *scientific\_name*) and *host taxid*, which you can also
    search for in [NCBI's taxonomy
    browser](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi),
    and should be as specific as possible.

-   **Some attributes should be selected from ontologies**. To increase
    searchability, some attribute values should be selected from
    designated ontologies, which are formal specifications of terms used
    in certain contexts, and of how these terms relate to each other.
    You can browse or search the latest versions of ontologies used in
    ENA submission using the [EMBL-EBI Ontology Lookup
    Service](https://www.ebi.ac.uk/ols/index). You can also use the
    following direct links to find valid terms for mandatory or
    recommended attributes in a GSC MixS checklists:

    > file
    > :   \_static/tables/ontology-fields.csv
    >
    > header-rows
    > :   1
    >
    In the linked ontology tree views, click the plus sign next to a
    blue-shaded branch to show all instances of that term, and continue
    downwards until you find the most specific term that accurately
    describes your data. It is good practice to then register the term
    together with ontology acronym and accession, e.g: *marine pelagic
    biome (ENVO:01000023)*.

-   **Environmental attributes of host-associated samples are
    ambiguous**. As stated above, a spider may in a sense be the
    environment from which a host-associated sample derives, but as the
    external environment also may be of interest here, we suggest that
    you interpret *environment (biome)* and *environment (feature)* the
    same way as for non-host-associated samples, and use the most
    specific instance of *organic material (ENVO:01000155)* for the
    *environment (material)* attribute.

-   **Geographic positions should be given in decimal degrees (DD)**. If
    conversion is needed, use an online tool, such as the [PGC
    Coordinate Converter](https://www.pgc.umn.edu/apps/convert/), or the
    following formula:

    +-----------------------+------+----------------------------------------+
    | Decimal Degrees       | =    | Degrees + Minutes/60 + Seconds/3600    |
    +-----------------------+------+----------------------------------------+
    | \*Ex: 58°11'12.34'' = | 58   | -   11/60 + 12.34/3600 = 58.1868°\*    |
    +-----------------------+------+----------------------------------------+
    | \*Ex: 58°11.21' = 58  | -    | .21/60 = 58.1868°\*                    |
    |                       | 11   |                                        |
    +-----------------------+------+----------------------------------------+

    The related *Geographic location (country and/or sea)* attribute
    should be selected from the [INSDC list for countries and
    seas](http://insdc.org/country.html).

-   **Investigation type** should be set to *mimarks-survey* for
    metabarcoding data.

#### Step 3f: Upload spreadsheet

With data added, your spreadsheet should look similar to this:

> file
> :   \_static/tables/filled-sample-template.csv
>
> header-rows
> :   0
>
If so, go back to the start page of sample submission and click *Submit
Completed Spreadsheet* and select your edited \*.tsv file. Given that
your spreadsheet structure is correct, you will be directed to a page
where you can toggle between samples in the left-hand panel, to inspect
attributes for each of these in the right panel. If you find yourself
stuck on the same page after uploading, you probably need to go back and
review your file structure.

#### Step 3g: Review and submit sample data

Before clicking the *Submit* button, have a look through the metadata
for each of your samples. Note that a red icon
![red-icon](_static/images/red-icon.png) next to a field or sample means
that data for a mandatory attribute is either missing or incorrect.
Depending on the type of validation used for a particular attribute, a
green icon ![green-icon](_static/images/green-icon.png) does not always
mean that data are correct, however, as you may instead get an error
message when submitting, or even get away with using a non-valid term.
After successful sample submission, you will receive a confirmation
message, and should be able to see your samples listed in the *Samples*
tab.

### Step 4: Prepare and upload read files

Before starting submission of reads and experiment data, you need to
prepare and upload read files to your own directory in the Webin file
upload area. We assume that you have paired-end reads in FASTQ format,
like the example files from the [mothur MiSeq
SOP](https://www.mothur.org/wiki/MiSeq_SOP) that we use below, but
please refer to [ENA's guidelines on file
formats](https://ena-docs.readthedocs.io/en/latest/fileprep/reads.html)
for other options:

#### Step 4a: Compress files and calculate checksums

On a Mac, open the Terminal app (in *Applications | Utilities*), and do
the following:

``` {.sourceCode .bash}
# Go to read file directory
# Tip: type 'cd ' and then drag/drop folder from Finder into Terminal
cd ~/your-read-file-dir

# Compress read files, if they are uncompressed (edit file extension as needed)
gzip -k *.fastq
```

To enable verification of file integrity after upload, calculate the md5
checksum of each (compressed) read file:

``` {.sourceCode .bash}
# Calculate and print md5 sums to tab-separated file (for easy cut-and-paste later)
for f in *.gz; do md5 $f | awk '{ gsub(/\(|\)/,""); print $2"\t" $4 }'; done > md5sums.tsv
```

The resulting file should look similar to this:

> file
> :   \_static/tables/md5sums.csv
>
> header-rows
> :   0
>
The *md5sum* command should work similarly on a Linux machine, but
Windows users may need to install some application to compress files to
\*.gz format, and refer to the following [Microsoft article on md5
generation](https://support.microsoft.com/en-gb/help/889768/how-to-compute-the-md5-or-sha-1-cryptographic-hash-values-for-a-file).

#### Step 4b: Upload read files to ENA

You can now upload your sequence reads to ENA's transit area, but
remember to keep local copies of your data. There are several FTP (File
Transfer Protocol) clients available for file transfer. We describe one
alternative
([lftp](https://brewinstall.org/Install-lftp-on-Mac-with-Brew/)) for Mac
users, but please refer to [ENA's guidelines on file
upload](https://ena-docs.readthedocs.io/en/latest/fileprep/upload.html)
for other options:

``` {.sourceCode .bash}
# Connect to FTP server
lftp webin.ebi.ac.uk
# Expected response: lftp webin.ebi.ac.uk:~>

# Request login to your account
login Webin-XXXXX
# Supply your password when prompted for it
xxxxxxxxxx
# Expected response: lftp Webin-XXXXX@webin.ebi.ac.uk:~>

# Transfer your read files
mput ~/your-read-file-dir/*.fastq.gz
# Expected response: ... Total x files transferred

# Disconnect from server
bye
```

### Step 5: Submit sequence reads

Once you have successfully uploaded your sequence reads, you need to
associate them with already submitted study and sample metadata, as well
as describe the sequencing experiment that produced the read files.

#### Step 5a: Select study, and create run template

Click *Restart Submission* (or *New Submission*, if logged out) |
*Submit sequence reads and experiments | Next*. In the presented *Study*
form, select the study you want to associate with your uploaded reads
(click ![reset-icon](_static/images/reset-icon.png) *Reset*, if needed)
and click *Next*. Then skip the *Sample* page, as you have already
uploaded sample metadata, and in the *Run* form, select your read file
format, here: *Two Fastq files (Paired)*. While you could now add data
directly into the resulting form, we recommend that you select *Download
Template Spreadsheet* to enter (and save!) metadata in an external
application.

#### Step 5b: Describe experiment and runs

In [the ENA metadata
model](https://ena-docs.readthedocs.io/en/latest/general-guide/metadata.html),
an *experiment* refers to a sequencing event, and contains information
on e.g. library construction and instruments, whereas *runs* represent
the read files resulting from an experiment. Click the info icon
![info-icon](_static/images/info-icon.png) to read ENA's explanation for
each attribute in the *Run* form, but enter your metadata into your
downloaded spreadsheet. Also note the following, when you describe the
experiment:

• **You can use any sample identifier as sample\_alias**. Toggle to the
*Sample* tab to copy values from *Primary / Secondary Accession* or
*Unique Name* (click ![reset-icon](_static/images/reset-icon.png)
*Reset*, if needed).

For metabarcoding, you would typically use the following values to
describe sequenced libraries (but see [ENA's guidelines on experiment
metadata](https://ena-docs.readthedocs.io/en/latest/reads/webin-cli.html)
for all available options):

• **library selection:** PCR

• **library source:** METAGENOMIC

• **library strategy**: AMPLICON

Also add the following metadata for read files:

• **forward [reverse]\_file\_name:** If you put your read files directly
into your account (in step 4b), you add filenames *only* here.
Otherwise, enter paths including all subdirectories.

• **forward [reverse]\_file\_md5:** Paste the md5 checksums from Step
4a.

Your spreadsheet should now look similar to this (but add as much
optional metadata as possible).

> file
> :   \_static/tables/runs.csv
>
> header-rows
> :   1
>
Note, however, that if you accidentally downloaded the template without
selecting file format, you also need to specify layout:

• **library layout**: PAIRED

Save your spreadsheet, go back to the Webin form and select *Upload
Completed Spreadsheet* | *Submit* to finally submit your read files. If
successful, you will receive a confirmation message.

### Step 6: Submit to production service

After careful inspection of data and metadata, you can now repeat the
process in the [production version of the Webin
interface](https://www.ebi.ac.uk/ena/submit/sra/#home).

Post-submission editing
-----------------------

ENA's interactive submission interface supports some [post-submission
editing](https://ena-docs.readthedocs.io/en/latest/update/interactive.html),
but for errors involving taxon attributes or sample aliases, you should
[contact ENA](datasubs@ebi.ac.uk) and they will help you cancel and
resubmit data.
