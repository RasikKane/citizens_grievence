# Predict the importance of citizen's grievences
given dataset contains grievances of various people living in a country. Notebook predicts the importance of the grievance with respect to various articles, constitutional declarations, enforcement, resources, and so on, to help the government prioritize which ones to deal with and when.

|Column_name                                |Count    |Description                                                                                    |
|---------------------------------|-----|-------------------------------------------------------------------------------------|
|appno                            |1    |Represents the application number                                                    |
|application                      |1    |Represents the type of application used to file a complaint                          |
|country.alpha2                   |1    |Represents the country code                                                          |
|country.name                     |1    |Represents the country name                                                          |
|decisiondate                     |1    |Represents the date on which a decision was taken                                    |
|docname                          |1    |Represents the case or document name                                                 |
|doctypebranch                    |1    |Represents the type of case                                                          |
|ecli                             |1    |Represents an alphanumeric value that is used to identify a case                     |
|introductiondate                 |1    |Represents the start date                                                            |
|itemid                           |1    |Represents the item ID                                                               |
|judgementdate                    |1    |Represents the judgment date                                                         |
|kpdate                           |1    |Represents the closure date                                                          |
|languageisocode                  |1    |Represents the language                                                              |
|originatingbody                  |1    |Represents a party or body from whom the case originated                             |
|originatingbody_name             |1    |Represents the name of the party of body from whom the case originated               |
|originatingbody_type             |1    |Represents the type of the party of body from whom the case originated               |
|parties.0                        |1    |Represents the details of the party of body from whom the case originated            |
|parties.1                        |1    |Represents the details of the party of body from whom the case originated            |
|parties.2                        |1    |Represents the details of the party of body from whom the case originated            |
|rank                             |1    |Represents the rank (0-10000) of officials (rank of an official increases with value)|
|respondent.0                     |1    |Represents a respondent information                                                  |
|respondent.1                     |1    |Represents a respondent information                                                  |
|respondent.2                     |1    |Represents a respondent information                                                  |
|respondent.3                     |1    |Represents a respondent information                                                  |
|respondent.4                     |1    |Represents a respondent information                                                  |
|respondentOrderEng               |1    |Represents a respondent information                                                  |
|separateopinion                  |1    |Represents the opinion on a case                                                     |
|sharepointid                     |1    |Represents the ID of an opinion                                                      |
|typedescription                  |1    |Represents a type_description {12- 19}                                               |
|issue.{0-26}                     |27   |Represents the description with respect to an issue                                  |
|article={number}                 |47   |Represents the type of article with respect to a case                                |
|documentcollectionid=CASELAW     |1    |Represents a document category of a case                                             |
|documentcollectionid=JUDGMENTS   |1    |Represents a document category of a case                                             |
|documentcollectionid=CHAMBER     |1    |Represents a document category of a case                                             |
|documentcollectionid=ENG         |1    |Represents a document category of a case                                             |
|documentcollectionid=COMMITTEE   |1    |Represents a document category of a case                                             |
|documentcollectionid=GRANDCHAMBER|1    |Represents a document category of a case                                             |
|applicability={number}           |61   |Represents the applicability of a case                                               |
|ccl_article={Type}               |25   |Represents the reliability of a CCL article type                                     |
|paragraphs={number}              |132  |Represents the reliability to a paragraph                                            |
|importance                       |1    |Represents the importance (0-5)                                                      |
