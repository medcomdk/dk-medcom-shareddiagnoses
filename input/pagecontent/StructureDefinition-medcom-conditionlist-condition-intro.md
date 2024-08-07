### Scope and usage 

This profile is intended to encapsulate information about condition, also referred to as diagnosis, that is relevant to share in a ConditionList. The profile inherits from DkCoreCondition and introduces some further constraints. 

#### Condition codes 
The codes for the condition are provided to the ConditionList by the general practitioner (GP) who reconciled the diagnoses with the subject, also referred to as patient. The condition codes from the GP's system will most often include a [SKS-D-code](https://medinfo.dk/sks/brows.php?s_nod=6314), [ICPC2-code](https://kiap.dk/kiap/praksis/services/koder/icpc/icpc2.php) and a text describing the condition (Danish: Diagnosetekst). However, it is not always the case that both codes and the text is available, why the requirements in the profile are fairly loose. 

The SKS-D-code and ICPC2-code must be included in the respective slice at Condition.code.coding, so they can be interpreted correct based on the Condition.code.system. It is allowed to include the display-value for the codes. The text selected by the GP must always be added in the element Condition.code.text.

The quality of the registered diagnose is not always as expected with two codes and a text. However, from the project it is decided to exchange the available information despite the incompleteness. To accommodate this, the following must be followed: 
* If only one SKS-D or ICPC2 code and a text is available, this information must be included in the respective elements 
* If no code, but a text is available, the text must be included in the text element 
* If one or both SKS-D or ICPC2 codes are available, but no text is available, the codes must be included in the respective elements
* If neither code nor text is available, a Condition instance must still be created with the remaining information
* If a code from another CodeSystem than SKS-D or ICPC2 is available, this code must be included in a new slice with a suited system, code and if available a display name.

The above cases are illustrated on the [example page](examples.html).

#### Description of the condition
As mentioned the GP has in most cases selected a text that represents the diagnosis the best (Danish: Diagnosetekst). This text must be included in the element Condition.code.text. It is further allowed for the GP to add an additional, short description of the diagnosis (Danish: Tillægstekst). If this is available, the text must be included in the element Condition.note.text. 

#### Condition status and category 
Both the status and category are selected by the GP. If the status is available, the Condition must contain information in the element Condition.clinicalStatus. This status can either be 'active' (Danish: aktuel), which represents conditions that the patient is currently experiencing, or 'inactive' (Danish: relevant), which represents condition that the patient no longer receives treatment for. 

If the category is available, the Condition must contain information in the element Condition.category, representing the type of diagnoses. The category can either be a 'problem-list-item' (Danish: forløbsdiagnose), which represents a condition that is managed over time, or a 'encounter-diagnosis' (Danish: kontaktdiagnose), which represents a diagnose that has been subject during an encounter. 

#### Timestamps
There can be different timestamp associated with a diagnosis. They must be included when the information is available:
* Condition.recordedDate: The date of the individual diagnosis entry in the database (Danish: registreringsdato).
* Condition.onsetDateTime: Actual or estimated date the condition began, in the opinion of the patient's GP (Danish: debutdato).
* Condition.abatementDateTime: The date or estimated date that the condition resolved or went into remission (Danish: afslutningsdato). 
