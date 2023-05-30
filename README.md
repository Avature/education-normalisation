# Repository for Resume Education Normalisation

This repository shares a test set for the task of normalising education experiences parsed from resumes 
(including spans of text identified as _degree_ and _major_) into a set of levels and fields of education with a delimited set of possible standard values.

Levels of education are represented as a number up to 8, following [ISCED](http://uis.unesco.org/en/isced-mappings)'s 
definition of level of education. For our target work context, only levels 3 (~high school) and onwards are considered.

Fields of education are presented hierarchically in a 3-level taxonomy, also shared in this repository. 


## Fields of Study Taxonomy

The shared **taxonomy for fields of education** can be found at `./taxonomy/field_taxonomy_tree.json`.

This taxonomy was created using ISCED's and others as a reference, but adapted to the labour context. 
It is a 3-level taxonomy with 16 broad fields, 39 narrow fields, and 132 detailed fields. A key difference with 
ISCED is that detailed fields (the most specific elements) can be repeated across several groups. In this way, the 
path distance between fields is intended to be more informative. As an example, “biochemistry” appears both under 
“chemical sciences”, a sibling to “chemistry”, and under “biological and life sciences”, a sibling to “biology”.

It is structured as follows:

	{"broad field": {"narrow field": ["detailed field"]}, ...}
	

In addition to the taxonomy with the field names itself, we are sharing the mappings between field names and their 
corresponding codes, which represent their position in the hierarchy.

The shared **field-to-code mappings** can be found at `./taxonomy/field2code_taxonomy_mappings.json`.

Codes are 6-character long strings: the first two characters identify the broad field, the middle two identify the 
narrow field, and the last two the detailed field. For example, two detailed fields with the same parent narrow field 
will share the same four characters in their codes, and differ in the last two. Unknown or underspecified levels use a wildcard in their missing stages: e.g. "chemical sciences" is a narrow field with several child detailed fields, so its code's last two characters will be the wildcard, "0705??".

If a field name corresponds to several levels of the taxonomy, its mapped code will be the most detailed, as there is 
no ambiguity. For example, "Sports" is a broad field with one only child narrow field and one grandchild detailed 
field, so its code is the most detailed one ("140101", not "14????" nor "1401??").

Finally, note that as in the proposed taxonomy detailed fields can appear in several groups (under more than one 
narrow field), a field name could have more than one mapped code.


## Test Set for the Education Normalisation Task


The shared **test set** can be found at `./test_set/normalisation_system_test_set.json`.

This is a test set for the normalisation of education information extracted from resumes. The normalised version of an 
education experience is a list of one or more level and field of education pairs. The test set samples were labelled by 
two human annotators following the given taxonomy.
 

### General Statistics

The inputs are conformed by a total of 1119 education experiences (parsed from resumes). 

These are some statistics about the normalised outputs:

 - Unique normalised fields of study covered: 112
 - Target levels of study covered: all (3 to 8, _null_ when unknown)
 - Total output normalised items: 1357
 - Number of unknown or empty fields of study: 46
 - Number of unknown levels of study: 122
 - Number of normalised outputs per input experience: min 1, max 4, mean 1.21
 - Percentage of education experiences with one normalised output item only: 80.43%


Top most frequent normalised levels of study:

 - Level 6 (~bachelors): 667 times, 49.15%
 - Level 7 (~masters): 320 times, 23.58%
 - Level 5 (~associates): appears 160 times, 11.79%
 

Top most frequent normalised fields of study:

 - Field 'management and administration': 131 times, 9.65%
 - Field 'information technology, software development, and computer applications': 69 times, 5.08%
 - Field 'computer science': 67 times, 4.94%
 

## Reference

These data correspond to the paper:

**Normalisation of Education Information in Digitalised Recruitment Processes**

Laura García-Sardiña, Federico Retyk, Hermenegildo Fabregat, Lucas Alvarez Lacasa, Rus Poves, and Rabih Zbib. 

To be presented at the 39th International Conference of the Spanish Society for Natural Language Processing and to 
appear at the journal _Procesamiento del Lenguaje Natural_, September 2023. 

If you use these data, please include the following reference:


	@article{garcia2023normalisation,
	  title={Normalisation of Education Information in Digitalised Recruitment Processes},
	  author={Garc{\'\i}a-Sardi{\~n}a, Laura and Retyk, Federico and Fabregat, Hermenegildo and Alvarez Lacasa, Lucas and Poves, Rus and Zbib, Rabih},
	  journal={Procesamiento del Lenguaje Natural},
	  number={71},
	  year={2023},
	  publisher={Sociedad Espa{\~n}ola para el Procesamiento del Lenguaje Natural}
	}
