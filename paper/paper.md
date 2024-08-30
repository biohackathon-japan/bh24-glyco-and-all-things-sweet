---
title: '2024 BioHackathon Report: Glyco Group'
title_short: 'BioHackJP 2024 Glyco'
tags:
  - Glycoscience
  - Chemoinformatics
  - Glycans
  - Glycoconjugates
  - Software
  - WURCS
authors:
  - name: Kiyoko F. Aoki-Kinoshita
    orcid: 0000-0002-6662-8015
    affiliation: 1
  - name: Evan Bolton
    orcid: 0000-0002-5959-6190
    affiliation: 2
  - name: Issaku Yamada
    orcid: 0000-0001-9504-189X
    affiliation: 3
  - name: Nathan John Edwards
    orcid: 
    affiliation: 4
  - name: Akihiro Fujita
    orcid: 0000-0003-3748-7791
    affiliation: 5
  - name: Masaaki Matsubara
    orcid: 0000-0001-6809-1568
    affiliation: 3
  - name: Masae Hosoda
    orcid: 0000-0002-4750-4041
    affiliation: 6
  - name: Yui Asano
    orcid: 
    affiliation: 7
affiliations:
  - name: Soka University
    index: 1
  - name: National Center for Biotechnolog Information (NCBI), PubChem
    index: 2
  - name: The Noguchi Institute
    index: 3
  - name: Georgetown University
    index: 4
  - name: Nagoya University
    index: 5
  - name: Database Center for Life Science
    index: 6
  - name: Swallow Design Studio Inc.
    index: 7
date: 31 Aug 2024
cito-bibliography: paper.bib
event: BH24JP
biohackathon_name: "BioHackathon Japan 2024"
biohackathon_url:   "https://2024.biohackathon.org/"
biohackathon_location: "Fukushima, Japan, 2024"
group: Glyco
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/biohackathon-japan/bh24-glyco-and-all-things-sweet/
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Kiyoko F. Aoki-Kinoshita \emph{et al.}
---

# 2024 BioHackathon Report: Glyco Group

## Introduction

The 2024 BioHackathon for the Glyco group focused on advancing the integration of glycan data, improving software tools, and addressing key challenges in glycoscience research. This report summarizes the group's objectives, activities, and outcomes during the event.
The structure of glycans lacks clear, distinguishable definitions, making it problematic to determine which structures should be considered as glycan data. We considered questions **“what is a ..”: “ .. glycan?”, “.. natural glycan?”, “.. carbohydrate?”** and **“what is the scope of GlyTouCan?”**

## Objectives

The main objectives of the Glyco group during the 2024 BioHackathon were:

1. **Refinement of Glycan Definition and Classification:**
   - Establish clear criteria for defining what constitutes a "natural" glycan.
   - Use the WURCS (Web3.0 Unique Representation of Carbohydrate Structures) framework to filter and classify glycans.

2. **Enhancement of GlyTouCan Repository:**
   - Improve the accuracy and comprehensiveness of glycan entries in GlyTouCan by integrating new filtering tools and updating data structures.

3. **Collaboration with PubChem:**
   - Use MolWURCS and other tools to detect glycan structures in PubChem and evaluate their relevance to glycoscience.

4. **Software and Tool Development:**
   - Update and improve existing glycan-related tools, including GlycanBuilder2, GlycanFormatConverter, MolWURCS, PDB2Glycan and TCarpRDF.
   - Implement new features in WURCSFilter for better glycan structure data filtering.
   - Extend and improve PyGly-based scripts for SNFG consistent matching of glycan structures.
   - GlyCosmos development of motifs including reducing end information

5. **Community Outreach and Education?:**
   - Develop clearer and more accessible documentation and flyers for tools like GlyCosmos.
   - Engage with the broader scientific community to promote the use and understanding of glycan data.

## Key Activities and Outcomes

### Refinement of Glycan Definition

- **Glycan Classification:**
  - The group focused on defining "natural" glycans by matching, using the GNOme subsumption alignment algorithm, of monosaccharides and substituents to those from the SNFG lists. Common “natural” substituents, extracted from WURCS sequences, that were missing from the SNFG list were added, and a frequency analysis used to discover potential additional substituents for addition. 
  - Current analysis suggests a very long tail for the monosaccharides and substituents found in WURCS sequences derived from pubchem entries, with just 13% of such sequences passing the stringent SNFG-based test implemented by the PyGly script. For GlyTouCan WURCS sequences, about 60% pass this test. 

Table 1. Substituents of …

| WURCS(MAP)               | Count | Category |                                 |
|--------------------------|-------|----------|---------------------------------|
| *                        | 72733 | Not SNFG | anhydro                         |
| *OC(CCCCCC$4)            | 54674 | Not SNFG | Bn                              |
| *OCO*/3C/3C              | 31389 | Not SNFG | O,O-2-propylidene               |
| *C                       | 27037 | Not SNFG | methylation                     |
| *OC(CCCCCC$4)/3=O        | 21141 | Not SNFG | Bz                              |
| *N=N=N                   | 13058 | Not SNFG | azido                           |
| *OC^XO*/3(CCCCCC$6)      | 7256  | Not SNFG | benxylidene                     |
| *OCCCC                   | 4775  | Not SNFG | O-nBu                           |
| *OC(CCCCCC$4/7)OC        | 3723  | Not SNFG | O-benzyl-4-O-methyl             |
| *CO                      | 3365  | Not SNFG | C-hydroxymethyl                 |
| *OC^RO*/3(CCCCCC$6)      | 3186  | Not SNFG | (1R)-benzylidene                |
| *OS(CCCCCC$4/7)C/3=O/3=O | 3040  | Not SNFG | O-thio-benzyl-4-hydroxycarbonyl |
| *OCC=C                   | 2719  | Not SNFG | O-allyl                         |
| *OSC/3=O/3=O             | 2649  | Not SNFG | S-C-Me                          |
| …             | …  | …  | …                          |

Table 2. Monosaccharide of …

| WURCS(Residue code) | Count | Category |                   |
|---------------------|-------|----------|-------------------|
| [a2122h-1x_1-5]     | 59719 | SNFG:    | Glc               |
| [a2112h-1x_1-5]     | 13828 | SNFG:    | Gal               |
| [a1122h-1x_1-5]     | 11049 | SNFG:    | Man               |
| [ax12xh-1u_1-5]     | 7704  | Bad:     |                   |
| [ax11xh-1u_1-5]     | 6428  | Bad:     |                   |
| [ax12xh-1d_1-5]     | 4838  | Bad:     |                   |
| [a2211m-1x_1-5]     | 3995  | SNFG:    | Rha               |
| [hxxxxh]            | 3624  | Good:    | Hexitol           |
| [a2212h-1x_1-5]     | 3591  | SNFG:    | Gul               |
| [ha122h-2b_2-5]     | 3323  | Good:    | b-D-Fructofranose |
| [a2122A-1x_1-5]     | 3187  | SNFG:    | GlcA              |
| [a2122m-1x_1-5]     | 3135  | SNFG:    | Qui               |
| [a212h-1x_1-5]      | 2959  | SNFG:    | Xyl               |
| [a1211h-1b_1-5]     | 2903  | Good:    | b-L-Glucopyranose |
| …     | …  | …    | …  |

- **WURCSFilter Implementation:**
  - A significant effort was made to enhance WURCSFilter, enabling it to better handle various glycan structures and substituents.

### Enhancement of GlyTouCan

- **Data Integration and Update:**
  - Updated GlyTouCan data with new WURCS versions and implemented stricter filtering criteria.
  - Focused on ensuring that only well-defined glycans, based on new criteria, are included in the database.

### Collaboration with PubChem

- **WURCS Analysis:**
  - Performed exhaustive analysis of PubChem entries to identify glycan-containing structures.
  - Analytical results will be integrated with GlyTouCan to improve the consistency and coverage of glycan data.

### Software and Tool Development

- **Tool Updates:**
  - GlycanBuilder2, GlycanFormatConverter, MolWURCS, PDB2Glycan and TCarpRDF were updated libs.
  - WURCSFilter was enhanced to support more flexible filtering based on user-defined criteria.
  - The SNFG glycan classification script from the GlyGen-Glycan-Data github project (includes PyGly and GNOme code-bases) was improved in a number of ways:
    - The script was extended to provide more information about why a specific monosaccharide or substituent was considered consistent with SNFG or not, including whether attached substituents or the monosaccharide core was failing to match with SNFG lists.
    - The set of supported substituents was expanded, first to include all SNFG substituents, and then with the addition of “natural” substituents missing from the SNFG list.
     - The script was extended to check “floating” substituents in compositions, and bridging substituents in glycosidic links.
     - The script was extended to verify that all SNFG monosaccharides and substituents, as WURCS sequences, could be parsed by the internal WURCS monosaccharide parser, reducing the possibility of false negatives. 
     - 

- **New Features:**
  - Introduced new filtering options to handle substituents and stereochemistry more effectively.

### Community Outreach and Education

- **Documentation and Flyers:**
  - Worked on improving the clarity and accessibility of documentation for tools like GlyCosmos.
  - Engaged with the scientific community through the creation of educational materials.

## Future Work

1. **Further Refinement of Glycan Definitions:**
   - Continue to refine the criteria for what constitutes a natural glycan, focusing on edge cases and complex structures.

2. **Refinement of the Algorithmic Framework for SNFG Consistency Determination**
    - The straightforward removal of SNFG substituents prior to checking the monosaccharide against the SNFG monosaccharide list may be too aggressive, since the full SNFG substituents list may contain substituents found on SNFG monosaccharides. Furthermore, removing all substituents from monosaccharides of unknown status can create a monosaccharide core that is unrepresented in the SNFG list, even though a form of the monosaccharide with one or more substituents remaining is in the SNFG list. Doing this properly will require the combinatorial enumeration of the substituents that should remain with the core monosaccharide 
    - The elucidation of why specific WURCS sequences, and which portion of those sequences - core monosaccharide residue or substituent, are considered consistent with the SNFG sets needs to be thoughtfully improved.

3. **Expansion of GlyTouCan Database:**
   - Integrate additional glycan data from external sources and continue to improve the accuracy of existing entries.

4. **Development of Educational Resources:**
   - Expand the outreach efforts by developing more comprehensive educational materials and engaging with a broader audience.

## Acknowledgements

The Glyco group extends its gratitude to all participants and collaborators who contributed to the success of the 2024 BioHackathon.


## References

1. Fujita, Akihiro, Nobuyuki P Aoki, Daisuke Shinmachi, Masaaki Matsubara, Shinichiro Tsuchiya, Masaaki Shiota, Tamiko Ono, Issaku Yamada, and Kiyoko F Aoki-Kinoshita. "The international glycan repository GlyTouCan version 3.0." *Nucleic Acids Research* 49, no. D1 (2021): D1529-D1533. doi: [10.1093/nar/gkaa947](https://doi.org/10.1093/nar/gkaa947).

2. Kim, Sunghwan, Jie Chen, Tiejun Cheng, Asta Gindulyte, Jia He, Siqian He, Qingliang Li, Benjamin A Shoemaker, Paul A Thiessen, Bo Yu, et al. "PubChem 2023 update." *Nucleic Acids Research* 51, no. D1 (2023): D1373-D1380. doi: [10.1093/nar/gkac956](https://doi.org/10.1093/nar/gkac956).

3. Yamada, Issaku, Masaaki Shiota, Daisuke Shinmachi, Tamiko Ono, Shinichiro Tsuchiya, Masae Hosoda, Akihiro Fujita, Nobuyuki P Aoki, Yu Watanabe, Noriaki Fujita, et al. "The GlyCosmos Portal: a unified and comprehensive web resource for the glycosciences." *Nature Methods* 17, no. 7 (2020): 649-650. doi: [10.1038/s41592-020-0879-8](https://doi.org/10.1038/s41592-020-0879-8).

4. Matsubara, Masaaki, Kiyoko F Aoki-Kinoshita, Nobuyuki P Aoki, Issaku Yamada, and Hisashi Narimatsu. "WURCS 2.0 update to encapsulate ambiguous carbohydrate structures." *Journal of Chemical Information and Modeling* 57, no. 4 (2017): 632-637. doi: [10.1021/acs.jcim.6b00650](https://doi.org/10.1021/acs.jcim.6b00650).

5.  "Toward Integration of Glycan Chemical Databases: An Algorithm and Software Tool for Extracting Sugars from Chemical Structures” *Analytical and Bioanalytical Chemistry* doi: [https://doi.org/10.1007/s00216-024-05508-1](https://https://doi.org/10.1007/s00216-024-05508-1).


