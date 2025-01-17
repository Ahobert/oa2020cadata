Data Descriptive: Corresponding author journal publishing activities
2014 - 2018
================

## Background & summary

Assessing the volume and share of corresponding author publications is
crucial for the planning of open access funding programs and licensing
models (Schimmer, Geschuhn, and Vogler 2015). However, funders and
national library consortia often lack access to bibliometric data, which
allows for determining the publication output per publisher, journal and
journal business model across countries. Here, by obtaining country
affiliations from the Web of Science at the level of journals, and
combining them with normalized publisher and open access status
information, we created a comprehensive dataset about the productivity
of corresponding authors for the period 2014-2018. This dataset is
expected to have essential value for the quantitative understanding of
scholarly publishing. It will not only help to analyze the market share
of publishing houses, but will also uncover the current state of the
transition of subscription-based publishing models to fully open access.

Only a few openly available datasets focusing on the scholarly
publishing industry exist. For example, Haustein, Larivière, and Mongeon
(2015) shared an aggregated dataset that contains the market share of
publishers in terms of articles indexed in the Web of Science between
1973-2013. Using this data, the authors were able to reveal a growing
market concentration among a few publishing houses (Larivière, Haustein,
and Mongeon 2015). Palzenberger (2015) provided a dataset presenting the
number and proportion of scholarly articles by country of affiliation
including a breakdown by author role for the period 2004-2014. Published
in 2015, this dataset, which was obtained from the Web of Science
in-house database from the German Competence Center for Bibliometrics,
formed the empirical basis for demonstrating that a large-scale
transition from a subscription-based to an open access business model is
is financially feasible in terms of the global amount spent on
subscriptions (Schimmer, Geschuhn, and Vogler 2015). Since then,
analyzing corresponding author publications has become a critical
component of open access negotiations between library consortia and
publishers.

There have also been analytical applications for such datasets. Major
bibliometric databases including the Web of Science, Scopus and
Dimension have started to integrate open access status information. In
these databases, Unpaywall data is often used to identify openly
available full-texts at the article-level, while the Directory of Open
Access Journals provides information about if a journal is fully open
access. In its most recent edition, the Leiden Ranking presents open
access indicators at the level of universities (Leeuwen, Costas, and
Robinson-Garcia 2019). In addition to university-specific data, the
German Open Access Monitor provides breakdowns by publisher and journal
and includes publications from non-university research institutions
based in Germany (Mittermaier et al. 2018).

Here, we build an open dataset on the global productivity of
corresponding authors. Drawing on Palzenberger’s (2015) previous work,
we not only created an updated dataset about the number and proportion
of scholarly articles per country of affiliation from corresponding
authors. The dataset also allows for a breakdown by journal, including
information whether it was operated as a subscription or fully open
access journal, and by publishers. We constructed the dataset using the
quality-assured Web of Science in-house database from the German
Competence Center for Bibliometrics. We enriched the data with publisher
information from Crossref, a large DOI registration agency for scholarly
work, and with open access journal information provided by the Biefeld
GOLD OA list, a dataset extending open access journal information from
the DOAJ with data from other sources (Bruns et al. 2019).

The data cannot only serve as a critical input for negotiations in the
context of transformative agreements, but also in the quantitative study
of the academic publishing industry and the open access uptake across
countries. For instance, national transformative agreements with large
publishers will increase opportunities to publish open access. The
existence of such agreements will therefore likely have an impact on the
open access share of a country with such agreements. To demonstrate the
dataset’s potential significance, we will present two new findings using
the dataset: a global map of publishers’s market share, and an analysis
of country of affiliation by publisher. Source code used for compiling
the dataset is shared along with the resulting datasets.

## Data and Methods

Following Palzenberger (2015), data were retrieved from the in-house Web
of Science database maintained by the German Competence Center for
Bibliometrics. The following data were obtained and aggregated:

  - Web of Science collections SCI, SSCI and AHCI
  - Article types Original Articles and Reviews
  - Country of affiliations
  - ISSN
  - Publication years 2014 - 2018
  - Author roles, interpreting the role “reprint author” as
    corresponding authorship.

The restriction to the article types original article and reviews
reflects that in most open access license negotiations other types of
journal content like letters or meeting abstracts are not considered. To
allocate open access costs to institutions, Schimmer, Geschuhn, and
Vogler (2015) proposed to use affiliations from corresponding authors,
presuming that corresponding author affiliations can be counted
straight. Under this counting method, only one institution or one
country receives full credit for a publication (Huang, Lin, and Chen
2011). However, there have been some concerns with using corresponding
authorship’s data from bibliometric databases for cost analysis
recently. Gumpenberger, Hölbling, and Gorraiz (2018) noted two potential
issues: multiple corresponding author affiliations and multiple
corresponding authors per article. Indeed, the Web of Science has begun
to systematically keep track of more than one corresponding author
recently (see Figure 1). We also found that the Web of Science did
record more than one corresponding author for 6.2% of indexed articles
published between 2014 - 2018. Moreover, a 5% of corresponding authors
author was internationally co-located (see Figure 2). We therefore
decided to use whole counting where every original article or review was
counted once per country of affiliation of the corresponding author(s).

![Figure 1](002_kb_rp_coverage_files/figure-gfm/ca_author_count-1.png)

![Figure 2](002_kb_rp_coverage_files/figure-gfm/ca_country_count-1.png)

After obtaining aggregated article counts at the level of countries and
journals from the Web of Science, Crossref’s REST API was queried using
the rcrossref package (Chamberlain et al. 2019) to retrieve publisher
and journal titles. To control for developments of the publishing market
resulting in name changes of publishers or journal titles over time,
only the most frequent field name was used from the API facet counts.
Drawing on ISSN-L, a journal identifier that links between different
media versions of a journal, ISSN variants were obtained to improve the
retrieval. Next, the open access status per journal was identified and
added to the dataset. This information was retrieved from a
comprehensive list of open access journals indexed in the Web of
Science, which joins open access journal information from various
sources including the DOAJ, PubMed Central and the Directory of Open
Access Scholarly Resources (ROAD) (Bruns et al. 2019). Again, ISSN-L
were used for the matching procedure.

## Data and Code availability

The underlying source code in R and SQL for both testing the retrieval
and compiling the datasets are openly shared as executable reports,
making our data work more reproducible and transparent. The data
analytics work, which was organized as research compendium (Marwick,
Boettiger, and Mullen 2018) using the holepunch R package (Ram 2019), is
accessible at <https://github.com/subugoe/oa2020cadata>

## The Dataset

Overall, our dataset consists of two separate tables, which are openly
available at (Link to Zenodo) as comma-separated values (csv) files and
Excel spreadsheets.

### Global journal and publisher data

The first file, named `journal_publisher_14_18`, contains information
about the publishing market landscape for the period 2014-2018 in terms
of the aggregated number of articles and reviews by year and journal
represented by the ISSN identifier indexed in the Web of Science. Table
1 describes the data variables in detail. We were able to retrieve
publisher and journal titles from Crossref for 88 % of all journals,
representing 95 % of the overall article volume. 1,981 out of 12,006
investigated journals with `ISSN-L` were identified as fully open access
journals. In total, the dataset provides information for 8,151,911
records indexed in the Web of Science with journal information in the
five-years period 2014-2018.

Data Schema
`journal_publisher_14_18`:

| Variable           | Description                                                                                                                                 | Source                                                                                         |
| :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------- |
| `issn_wos`         | ISSN, a standardized journal id.                                                                                                            | KB Web of Science: `wos_b_2019.issues.issn`                                                    |
| `publication_year` | Year of publication, obtained from KB Web of Science                                                                                        | KB Web of Science: `wos_b_2019.items.pubyear`                                                  |
| `articles`         | Number of original articles and reviews published.                                                                                          | KB Web of Science: Grouped counts over `wos_b_2019.issues.issn` and `wos_b_2019.items.pubyear` |
| `journal_title`    | Most frequently used journal title in terms of articles published between 2014 - 2018. If missing, the journal was not indexed in Crossref  | Crossref                                                                                       |
| `publisher`        | Most frequently used publisher name in terms of articles published between 2014 - 2018. If missing, the journal was not indexed in Crossref | Crossref                                                                                       |
| `oa_journal`       | Is the journal publishing all articles open access without delay (full open access)?                                                        | Bielefeld GOLD OA List V3                                                                      |
| `issn_l`           | Linking ISSN, a journal id that groups the different media of the same serial publication, e.g. ISSN for print with electronic issn.        | CIEPS                                                                                          |

### Corresponding author data

The file named `rp_14_18` provides a breakdown of journal information
aggregated by countries of affiliation. Only corresponding authorships,
indicated by the role “reprint author” in the Web of Science database,
were taken into consideration. The following table describes the
variables in detail. Overall, 99 % of records representing original
articles and reviews in the period 2014 - 2018 had affiliation
information for corresponding authors at the country-level.

Data
Schema:

| Variable           | Description                                                                                                                                                                      | Source                                                                                                                                                     |
| :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `issn_wos`         | ISSN, a standardized journal id.                                                                                                                                                 | KB Web of Science: `wos_b_2019.issues.issn`                                                                                                                |
| `country_code`     | Country of affiliation corresponding author, represented as ISO 3 code                                                                                                           | KB Web of Science: `wos_b_2019.d_items_authors_institutions.inst_countrycode`                                                                              |
| `publication_year` | Year of publication, obtained from KB Web of Science                                                                                                                             | KB Web of Science: `wos_b_2019.items.pubyear`                                                                                                              |
| `articles`         | Number of original articles and reviews published. Whole counting where internationally co-located corresponding authorships were assigned to each contributing country equally. | KB Web of Science: Grouped counts over `wos_b_2019.issues.issn`, `wos_b_2019.d_items_authors_institutions.inst_countrycode` and `wos_b_2019.items.pubyear` |
| `journal_title`    | Most frequently used journal title in terms of articles published between 2014 - 2018. If missing, the journal was not indexed in Crossref                                       | Crossref                                                                                                                                                   |
| `publisher`        | Most frequently used publisher name in terms of articles published between 2014 - 2018. If missing, the journal was not indexed in Crossref                                      | Crossref                                                                                                                                                   |
| `oa_journal`       | Is the journal publishing all articles open access without delay (full open access)?                                                                                             | Bielefeld GOLD OA List V3                                                                                                                                  |
| `issn_l`           | Linking ISSN, a journal id that groups the different media of the same serial publication, e.g. ISSN for print with electronic issn.                                             | CIEPS                                                                                                                                                      |

<!--### Corresponding author co-authorship network -->

## Use-cases

### Global publisher market share

Based on the dataset `journal_publisher_14_18` the global market share
of publishing houses in terms of articles and reviews indexed in the Web
of Science can be analyzed for the period 2014-18. The following table
shows the overall market share for the ten largest publishers. The
following figure presents a breakdown by journal business model,
differentiating between subscription journals and fully open
access.

| Publisher                                                | Articles and Reviews published | Percentage |
| :------------------------------------------------------- | -----------------------------: | ---------: |
| Elsevier BV                                              |                      1,942,425 |       23.8 |
| Springer Nature                                          |                      1,134,385 |       13.9 |
| Wiley                                                    |                        711,824 |        8.7 |
| Informa UK Limited                                       |                        411,910 |        5.0 |
| American Chemical Society (ACS)                          |                        216,320 |        2.6 |
| SAGE Publications                                        |                        190,534 |        2.3 |
| Royal Society of Chemistry (RSC)                         |                        189,477 |        2.3 |
| Institute of Electrical and Electronics Engineers (IEEE) |                        178,400 |        2.2 |
| Oxford University Press (OUP)                            |                        176,699 |        2.2 |
| Ovid Technologies (Wolters Kluwer Health)                |                        149,951 |        1.8 |
| Other                                                    |                      2,849,986 |       35.0 |
| Total                                                    |                      8,151,911 |      100.0 |

Publisher Market Share 2014 - 2018 in terms of articles and reviews
indexed in the Web of Science

![Figure 3](figure/global_publisher_share.png)

Our data confirms that the global publishing landscape is dominated by a
few large publishers. In total, ten publishers accounted for around
two-thirds of articles published between 2014 - 2018. The Big 3,
Elsevier, Springer Nature and Wiley, accounted for a percentage of 46 %.
However, further analysis suggests large differences when
differentiating between subscription and fully open access journals: The
market for fully open access journals seems to be far less dominated by
major publishing houses. A notable exception is Springer Nature with its
large fully open access portfolio including BioMed Central and the large
mega-journals Scientific Reports and Nature Communications.

### Global Map of Journal Publishing

Using `rp_14_18` the publisher market shares can be further broken down
by country affiliation from corresponding authors. The following figure
presents a global map of scholarly journal publishing represented in the
Web of Science. Publications from institutions based in the European
Union were summarized as “EU28”. Together, all EU 28 member states
constituted the largest market for journal publishing between 2014-18.

![Figure 4](figure/map.png)

The following figure shows the country share per publisher in terms of
original articles and reviews published in subscription journals using
corresponding author affiliations. The flipped x-axis shows the top 10
countries of affiliations in terms of articles published, while the
y-axis depicts the percentage per publisher. The figure indicates, which
countries were of particularly importance to a publisher. Furthermore,
it suggests large variations across publishers. Take for instance the
publisher Royal Society of Chemistry. Around every third article
published in a subscription journal was submitted from an author based
in China, while the overall share of China-based authors was 17 %.

![](figure/publisher_share.png)

## Responsible use and limitations

Although the Web of Science database is a well-established bibliometric
database in the quantitative science studies it comes with certain
limitations that need careful consideration when using and interpreting
our data. First, the Web of Science is selective in terms of journal
inclusion, likely not covering the whole journal portfolio of the
investigated publishers. Although publisher names were disambiguated,
journal title transfers between publishers were not tracked.
Furthermore, the year of inclusion in a journal issue, i.e. print
publication date, was used. However, there can be a considerable
time-lag between online-first publication and issue inclusion.

Moreover, as any other bibliometric databases, the data structure can be
subject of change. In particular, our pretests suggest that the Web of
Science author role field used to identify corresponding authorships has
undergone a change recently, starting to covering more than one reprint
resp. corresponding author per article.

The Bielefeld GOLD OA list (Bruns et al. 2019) was used to determine
fully open access journals. However, it does not contain the date when a
subscription-based journal became fully open access. The figures should
be therefore interpreted as numbers of articles available in current
fully open access journals, instead of published in an fully open access
journal at the time of publication. Open access article counts are
therefore upper estimates.

In the end, we present a novel bibliometric dataset representing the
journal publishing market with a particular focus on open access.
Although access to the underlying data infrastructure is restricted, we
decided to openly share the aggregated dataset as part of a research
compendium to demonstrate the technical reproducibility of this work.

## Acknowledgment

## References

<div id="refs" class="references">

<div id="ref-issn">

Bruns, Andre, Christopher Lenke, Constanze Schmidt, and Niels Christian
Taubert. 2019. “ISSN-Matching of Gold OA Journals (ISSN-GOLD-OA) 3.0.”
Bielefeld University. <https://doi.org/10.4119/unibi/2934907>.

</div>

<div id="ref-rcrossref">

Chamberlain, Scott, Hao Zhu, Najko Jahn, Carl Boettiger, and Karthik
Ram. 2019. *Rcrossref: Client for Various ’Crossref’ ’Apis’*.
<https://CRAN.R-project.org/package=rcrossref>.

</div>

<div id="ref-Gumpenberger_2018">

Gumpenberger, Christian, Lothar Hölbling, and Juan Ignacio Gorraiz.
2018. “On the Issues of a Corresponding Author Field-Based Monitoring
Approach for Gold Open Access Publications and Derivative Cost
Calculations.” *Frontiers in Research Metrics and Analytics* 3
(February). <https://doi.org/10.3389/frma.2018.00001>.

</div>

<div id="ref-haustein_2015">

Haustein, Stefanie, Vincent Larivière, and Philippe Mongeon. 2015. “Data
for: The Oligopoly of Academic Publishers in the Digital Era.” Figshare.
<https://doi.org/10.6084/m9.figshare.1447274.v1>.

</div>

<div id="ref-Huang_2011">

Huang, Mu-Hsuan, Chi-Shiou Lin, and Dar-Zen Chen. 2011. “Counting
Methods, Country Rank Changes, and Counting Inflation in the Assessment
of National Research Productivity and Impact.” *Journal of the American
Society for Information Science and Technology* 62 (12): 2427–36.
<https://doi.org/10.1002/asi.21625>.

</div>

<div id="ref-Larivi_re_2015">

Larivière, Vincent, Stefanie Haustein, and Philippe Mongeon. 2015. “The
Oligopoly of Academic Publishers in the Digital Era.” *PLOS ONE* 10 (6):
e0127502. <https://doi.org/10.1371/journal.pone.0127502>.

</div>

<div id="ref-leiden">

Leeuwen, Thed van, Rodrigo Costas, and Nicolas Robinson-Garcia. 2019.
“Indicators of Open Access Publishing in the Cwts Leiden Ranking
2019.” <https://www.cwts.nl/blog?article=n-r2w2a4>.

</div>

<div id="ref-Marwick_2017">

Marwick, Ben, Carl Boettiger, and Lincoln Mullen. 2018. “Packaging Data
Analytical Work Reproducibly Using R (and Friends).” *The American
Statistician* 72 (1): 80–88.
<https://doi.org/10.1080/00031305.2017.1375986>.

</div>

<div id="ref-oa_monitor">

Mittermaier, Bernhard, Irene Barbers, Dirk Ecker, Barbara Lindstrot,
Heidi Schmiedicke, and Philipp Pollack. 2018. “Der Open Access Monitor
Deutschland.” *O-Bib. Das Offene Bibliotheksjournal* 5 (4).
<https://doi.org/10.5282/o-bib/2018h4s84-100>.

</div>

<div id="ref-Palzenberger_2015">

Palzenberger, Margit. 2015. “Number of Scholarly Articles Per Country.”
Max Planck Digital Library. <https://doi.org/10.17617/1.2>.

</div>

<div id="ref-holepunch">

Ram, Karthik. 2019. *Holepunch: Configure Your R Project for
’Binderhub’*. <https://github.com/karthik/holepunch>.

</div>

<div id="ref-Schimmer_2015">

Schimmer, Ralf, Kai Geschuhn, and Andreas Vogler. 2015. “Disrupting the
subscription journals’business model for the necessary large-scale
transformation to open access.” Max Planck Digital Library.
<https://doi.org/10.17617/1.3>.

</div>

</div>
