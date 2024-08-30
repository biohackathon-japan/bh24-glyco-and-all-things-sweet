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
  - name: Issaku Yamada
    orcid: 0000-0001-9504-189X
    affiliation: 1
  - name: Evan Bolton
    orcid: 0000-0002-5959-6190
    affiliation: 2
  - name: Nathan John Edwards
    orcid: 
    affiliation: 3
  - name: Masaaki Matsubara
    orcid: 0000-0001-6809-1568
    affiliation: 1
  - name: Masae Hosoda
    orcid: 0000-0002-4750-4041
    affiliation: 4
  - name: Akihiro Fujita
    orcid: 0000-0003-3748-7791
    affiliation: 5
  - name: Yui Asano
    orcid: 
    affiliation: 6
  - name: Kiyoko F. Aoki-Kinoshita
    orcid: 0000-0002-6662-8015
    affiliation: 7
affiliations:
  - name: The Noguchi Institute
    index: 1
  - name: National Center for Biotechnolog Information (NCBI), PubChem
    index: 2
  - name: Georgetown University
    index: 3
  - name: Database Center for Life Science
    index: 4
  - name: Nagoya University
    index: 5
  - name: Swallow Design Studio Inc.
    index: 6
  - name: Soka University
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
authors_short: Issaku Yamada \emph{et al.}
---

# 2024 BioHackathon Report: Glyco Group

## Introduction

The field of glycoscience is rapidly advancing in terms of data integration, software tool improvement, and addressing key research challenges. The activities of the Glyco group at the 2024 BioHackathon represent a significant step towards these goals. The structure of glycans has long posed challenges due to the lack of clear, distinguishable definitions, making it problematic to determine which structures should be considered as glycan data. This research tackles fundamental questions such as "What is a glycan?", "What is a natural glycan?", "What is a carbohydrate?", and also explores the scope of GlyTouCan (the International Glycan Structure Repository). The hackathon focused on five main objectives: refining glycan definition and classification, clarifying the scope of the GlyTouCan repository, collaborating with PubChem, developing and improving software tools, and community outreach and education. Particular emphasis was placed on using the WURCS framework to filter and classify glycans, employing tools like MolWURCS to detect and evaluate glycan structures in PubChem, and updating and improving existing glycan-related tools. These efforts aim to enhance the quality and consistency of data in the field of glycoscience and promote the use and understanding of glycan data in the broader scientific community. This paper reports in detail on the activities, outcomes, and future prospects of the Glyco group at the 2024 BioHackathon.

## Objectives

The main objectives of the Glyco group during the 2024 BioHackathon were:

1. **Refinement of Glycan Definition and Classification:**
   - Establish clear criteria for defining what constitutes a "natural" glycan.
   - Use the WURCS framework to filter and classify glycans.

2. **Waht is scope of GlyTouCan Repository:**
   - Scope of structures to be registered in GlyTouCan

3. **Collaboration with PubChem:**
   - Use MolWURCS and other tools to detect glycan structures in PubChem and evaluate their relevance to glycoscience.

4. **Software and Tool Development:**
   - Implement new features in WURCSFilter for better glycan structure data filtering.
   - Extend and improve PyGly-based scripts for SNFG consistent matching of glycan structures.
   - GlyCosmos development of motifs including reducing end information
   - Updates to existing glycan-related tools, including software for glycan structure drawing, glycan text format conversion, and WURCS to image generator

5. **Community Outreach and Education?:**
   - - Creating a clearer and more understandable flyer for the GlyCosmos glycoscience portal.

## Key Activities and Outcomes

### Refinement of Glycan Definition

- **Glycan Classification:**
  - The group focused on defining "natural" glycans by matching, using the GNOme subsumption alignment algorithm, of monosaccharides and substituents to those from the SNFG lists. Common “natural” substituents, extracted from WURCS sequences, that were missing from the SNFG list were added, and a frequency analysis used to discover potential additional substituents for addition. 
  - Current analysis suggests a very long tail for the monosaccharides and substituents found in WURCS sequences derived from pubchem entries, with just 13% of such sequences passing the stringent SNFG-based test implemented by the PyGly script. For GlyTouCan WURCS sequences, about 60% pass this test. 

Table 1. The types and numbers of substituents contained in PubChem compounds

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

MAP is a modification representation in WURCS notation

Table 2. The types and numbers of monosaccharides contained in PubChem compounds

| WURCS(ResidueCode) | Count | Category |                   |
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

ResidueCode is representation of a monosaccharide core structure in WURCS notation

- **WURCSFilter Implementation:**
  - A significant effort was made to enhance WURCSFilter, enabling it to better handle various glycan structures and substituents.

### Scope of structures to be registered in GlyTouCan

- **Data Integration:**
  - Discussed the "New Standards for Registering Glycan Structures" to be proposed to the GlyTouCan Scientific Advisory Board and prepared the document.
 
### Collaboration with PubChem

- **WURCS Analysis:**
  - Performed exhaustive analysis of PubChem entries to identify glycan-containing structures.
  - Analytical results will be integrated with GlyTouCan to improve the consistency and coverage of glycan data.

### Software and Tool Development

- **Tool Updates:**
  - WURCSFilter   (PatternMatching library of WURCS string) was enhanced to support more flexible filtering based on user-defined criteria.
  - The SNFG glycan classification script from the GlyGen-Glycan-Data github project (includes PyGly and GNOme code-bases) was improved in a number of ways:
    - The script was extended to provide more information about why a specific monosaccharide or substituent was considered consistent with SNFG or not, including whether attached substituents or the monosaccharide core was failing to match with SNFG lists.
    - The set of supported substituents was expanded, first to include all SNFG substituents, and then with the addition of “natural” substituents missing from the SNFG list.
     - The script was extended to check “floating” substituents in compositions, and bridging substituents in glycosidic links.
     - The script was extended to verify that all SNFG monosaccharides and substituents, as WURCS sequences, could be parsed by the internal WURCS monosaccharide parser, reducing the possibility of false negatives. 
     - Updated some functions in PyGly/scripts (allimg.sh), a Java program + shell script for generating images from GlycanBuilder2-based WURCS.
    - In conjunction with the update of WURCSFramework, the basic library that processes WURCS, several related software libraries are currently being updated. This work in progress includes GlycanBuilder2, GlycanFormatConverter, MolWURCS, PDB2Glycan, and TCarpRDF.
     - Updated the GlycanBuilder2 library in wurcs2pic (https://gitlab.com/glycoinfo/wurcs2pic), a software that generates SNFG images from WURCS.
    - When a glycan structure contains multiple motifs, some smaller motifs may be nested within larger ones. In such instances, the larger motif is selected as the representative motif for that glycan structure. In this development, we refined the organization of motif information by considering details such as whether these smaller and larger motifs are 'located only at the reducing end,' ensuring a more accurate treatment of the motif data.


### Community Outreach and Education

- **Documentation and Flyers:**
  - In collaboration with the broader scientific community, we created an easy-to-understand flyer to promote the use and understanding of glycan data. This effort aims to make glycan-related information more accessible to researchers and scientists across various fields, potentially fostering increased engagement with and application of glycan data in scientific studies and projects.


## Future Work

1. **Further Refinement of Glycan Definitions:**
   - Continue to refine the criteria for what constitutes a natural glycan, focusing on edge cases and complex structures.

2. **Refinement of the Algorithmic Framework for SNFG Consistency Determination**
    - The straightforward removal of SNFG substituents prior to checking the monosaccharide against the SNFG monosaccharide list may be too aggressive, since the full SNFG substituents list may contain substituents found on SNFG monosaccharides. Furthermore, removing all substituents from monosaccharides of unknown status can create a monosaccharide core that is unrepresented in the SNFG list, even though a form of the monosaccharide with one or more substituents remaining is in the SNFG list. Doing this properly will require the combinatorial enumeration of the substituents that should remain with the core monosaccharide 
    - The elucidation of why specific WURCS sequences, and which portion of those sequences - core monosaccharide residue or substituent, are considered consistent with the SNFG sets needs to be thoughtfully improved.

3. **Expansion of GlyTouCan Repository:**
   - Integrate additional glycan data from external sources and continue to improve the accuracy of existing entries.

4. **Software and Tool Development:**
   - To improve existing tools and develop new ones that can be utilized in glycoscience research and for integration with other fields.

5. **Development of Educational Resources:**
   - Expand the outreach efforts by developing more comprehensive educational materials and engaging with a broader audience.

## Acknowledgements

The Glyco group extends its gratitude to all participants and collaborators who contributed to the success of the 2024 BioHackathon.

## Abbreviation

- GNOme: Glycan Naming and Subsumption Ontology

- GlyCosmos: GlyCosmos Glycoscience Portal

- GlyTouCan: International Glycan Structure Repository

- SNFG: Symbol Nomenclature for Glycans

- WURCS: Web3.0 Unique Representation of Carbohydrate Structures


## References
1.
