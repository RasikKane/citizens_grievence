# Predict the importance of citizen's grievences
given dataset contains grievances of various people living in a country. Notebook predicts the importance of the grievance with respect to various articles, constitutional declarations, enforcement, resources, and so on, to help the government prioritize which ones to deal with and when.

## Data Quality Plan
**After initial data analytics, following insights are drawn for feature data cleaning and wrangling**

| Features                  | Data<br>Classification| Subtype    | Description Or<br>domain significance  | Data quality issue |Solution Strategy |
|:------------------------- |:------------------ |:---------- |:-----------|:-------------- |:-------------- | 
| appno                                 | catagorical        | nominal    | application number<br><br>e.g. 53865/11|**NO_SIG**<br>13467 unique values<br>No nulls|**Drop**<br>|
| application                           | catagorical        | nominal    | software used<br><br>for lodging complaint<br>e.g. MS word|**NO_SIG**<br>1 unique value<br>no null|**Drop**<br>|
| country.alpha2                        | catagorical        | nominal    | country code<br><br>e.g. ie|**SIG**<br>46 unique countries<br>no nulls|**Keep**<br><br>one hot encode into constituent features|
| country.name                          | catagorical        | nominal    | country name<br><br>e.g. Ireland|**HCR**<br>Corr->1 with<br>'country.alpha2'|**Drop**<br>|
| decisiondate                          | numeric            | continuous<br>datetime   | date of decision|**NO_SIG**<br>92% null values|**Drop**<br>|
| docname                               | catagorical        | nominal    | name of case<br><br>e.g.CASE OF <br>EMINBEYLI v. RUSSIA|**NO_SIG**<br>name of complainant <br>and country available <br>in features 'country.name' <br>and 'parties.0'|**Drop**<br>|
| doctypebranch                         | catagorical        | Ordinal    | type of case<br><br>e.g. CHEMBER, COMMITTEE,<br>GRANDCHEMBER|**SIG**<br>represented in 1-hot<br>encoded form<br>in feature<br>'documentcollectionid=<br>{CHEMBER, COMMITTEE,<br>GRANDCHEMBER}'|**Drop**<br>|
| ecli                                  | catagorical        | nominal    | database case ID<br><br>e.g. ECLI:CE:ECHR:2015:<br>.1203JUD005386511|**NO_SIG**<br>primary key<br>no contribution<br>in prediction|**Drop**<br>|
| introductiondate                      | numeric            | continuous<br>datetime   | date of introduction|**NO_SIG**<br>92% null values|**Drop**<br>|
| itemid                                | catagorical        | nominal    | database item ID<br><br>e.g. 001-108659|**NO_SIG**<br>primary key<br>no contribution<br>in prediction|**Drop**<br>|
| judgementdate                         | numeric            | continuous<br>datetime   | date of Judgement|**SIG**<br>No null values<br>2088 unique<br>entries in<br>13638 samples|**Keep**<br><br>seperate into quarter, month,<br>year, weekday and<br>convert to categorical|
| kpdate                                | numeric            | continuous<br>datetime   | date of closure|**SIG**<br>No null values<br>2088 unique<br>entries in<br>13638 samples|**Drop**<br>Duplicate of judgementdate|
| languageisocode                       | catagorical        | nominal    | Language<br><br>e.g. ENG|**NO_SIG**<br>1 unique value<br>no null|**Drop**<br>|
| originatingbody                       | catagorical        | nominal    | Party originating<br>case<br><br>e.g. [29,1..]|**SIG**<br>13 unique value<br>no null|**Keep**<br><br>one hot encode into constituent features |
| originatingbody_name                  | catagorical        | nominal    | Name of party<br>originating<br>case<br><br>e.g. Fith Section Committee,<br>Second Section|**HCR**<br>Corr->1 with<br>'originatingbody'|**Drop**<br>|
| originatingbody_type                  | catagorical        | nominal    | Name of party<br>originating<br>case|**NO_SIG**<br>1 unique value<br>no null|**Drop**<br>|
| parties.0                             | catagorical        | nominal    | Name of party<br>filing<br>case|**NO_SIG**<br>12535 unique values<br>no null|**Drop**<br>|
| parties.1                             | catagorical        | nominal    | Name of country/s<br>against whome<br>case filed<br><br>e.g. "IRELAND", "RUSSIA"|**NO_SIG**<br>107 unique values<br>no null<br>majority of values<br>correlate with<br>'country.alpha2'|**Drop**<br>|
| parties.2                             | catagorical        | nominal    | party of body <br>from whom the<br> case originated<br><br>e.g. "IRELAND", "RUSSIA"|**NO_SIG**<br>~99% null values|**Drop**<br>|
| rank                                  | numerical        | continuous   | rank (0-10000)<br>of officials<br>rank of an official<br>increases with value|**SIG**<br>6484 unique values<br>no null|**Keep**<br><br>high cardinality feature<br>binning is necessary|
| respondent.0                          | catagorical        | nominal    | respondant to grievence<br>e.g. RUS|**HCR**<br>Corr->1 with<br>'country.alpha2'|**Drop**<br>|
| respondent.1                          | catagorical        | nominal    |respondant to grievence<br>e.g. RUS|**NO_SIG**<br>99% null values|**Drop**<br>|
| respondent.2                          | catagorical        | nominal    | respondant to grievence<br>e.g. RUS|**NO_SIG**<br>99% null values|**Drop**<br>|
| respondent.3                          | catagorical        | nominal    | respondant to grievence<br>e.g. RUS|**NO_SIG**<br>99% null values|**Drop**<br>|
| respondent.4                          | catagorical        | nominal    | respondant to grievence<br>e.g. RUS|**NO_SIG**<br>99% null values|**Drop**<br>|
| respondentOrderEng                    | catagorical        | nominal    | respondent information<br>numreic label<br>e.g. 49|**HCR**<br>Corr->1 with<br>'country.alpha2'|**Drop**<br>|
| separateopinion                       | catagorical        | nominal    |  on a case<br> e.g. {TRUE, FALSE}|**SIG**<br>No null values<br>Boolean feature|**Keep**<br><br>one hot encode into constituent features |
| sharepointid                          | catagorical        | nominal    | sharepoint ID<br><br>e.g. 359124|**NO_SIG**<br>primary key<br>no contribution<br>in prediction|**Drop**<br>|
| typedescription                       | catagorical        | nominal    | type_description {12- 19}|**SIG**<br>No null values<br>5 distinct values|**Keep**<br><br>one hot encode into constituent features |
| issue.{0-26}                          | catagorical        | nominal    | description with respect<br>to an issue<br><br>e.g. "Instruction regarding<br>the detention","Law on pre-trial<br>detention (1997-..|**NO_SIG**<br>text description<br>~99% null data in<br>most of columns|**Drop**<br>|
| article={27 numbers}                  | catagorical        | nominal    | type of article|**SIG**<br>1 hot encoded|**Keep**<br>|
| documentcollectionid=<br>CASELAW      | catagorical        | nominal    | document category=CASELAW   |**NO_SIG**<br>1 unique value<br>no null|**Drop**<br>|
| documentcollectionid=<br>JUDGMENTS    | catagorical        | nominal    | document category=JUDGEMENTS|**NO_SIG**<br>1 unique value<br>no null|**Drop**<br>|
| documentcollectionid=<br>ENG          | catagorical        | nominal    | document category=ENG|**NO_SIG**<br>1 unique value<br>no null|**Drop**<br>|
| documentcollectionid=<br>CHAMBER      | catagorical        | nominal    | document category=CHEMBERS|**SIG**<br>1 hot encoded<br>from feature<br>'doctypebranch'|**Keep**<br>|
| documentcollectionid=<br>COMMITTEE    | catagorical        | nominal    | document category=COMMITTEE|**SIG**<br>1 hot encoded<br>from feature<br>'doctypebranch'|**Keep**<br>|
| documentcollectionid=<br>GRANDCHAMBER | catagorical        | nominal    | document category=GRANDCHEMBER|**SIG**<br>1 hot encoded<br>from feature<br>'doctypebranch'|**Keep**<br>|
| applicability=<br>{61 numbers}        | catagorical        | nominal    |  applicability of case|**SIG**<br>1 hot encoded|**Keep**<br>|
| ccl_article=<br>{25 Type}             | catagorical        | nominal    | reliability of<br>CCL article type<br>e.g. {-1,0,1}|**SIG**<br>1 hot encoded|**Keep**<br><br>one hot encode into constituent features |
| paragraphs=<br>{132 numbers}          | catagorical        | nominal    | category   |**SIG**<br>1 hot encoded|**Keep**<br>|
| importance                            | catagorical        | ordinal    | Target variable<br>0-5|**SIG**<br>target variable|**Keep**<br>|


