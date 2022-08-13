# Exported data structure
Exported data closely follows the structure used for the import data with a few tweaks:

## Sample tweaks
Exported samples additionally contain a `status` field, which describes whether the samples was accepted, rejected or marked as uncertain by the annotator.

Hence a **sample** has the following structure:

| **Property** | **Type** | **Explanation** |
|---|---|---|
| text | string | Text of the sample (text to be annotated) |
| annotations | AnnotationData \| null | Pre-generated annotations (entities or relationships). Can be used to create suggestions for the annotator |
| metadata | Metadata \| null | Contains metadata unique to the given sample. Consists of unique entity/relationship tags for the given sample |
| status | accepted \| rejected \| unceratin \| null | Describes whether the samples was accepted, rejected or marked as uncertain by the annotator |

## Entity tweaks
Exported entities additionally contain a `content` field. This is a convience field, which holds the subtext of the original text marked as the given entity. It is the same substring of the original text which will be obtained by using the `start` and `end` indices. 

Hence an **Entity** object has the following structure:

| **Property** | **Type** | **Explanation** |
|---|---|---|
| id | number | unique ID of the entity |
| start | number | index to the starting character of the entity in the context of the sample text |
| end | number | index to the ending character of the entity in the context of the sample text |
| tag | string \| null | tag given to the entity (e.g. NOUN, VERB or any custom tag) |
| color | string \| null | hex color string, determines the highlight color of the entity |
| notes | string \| null | any additional information about the entity |
| content | string | Text of the entity |