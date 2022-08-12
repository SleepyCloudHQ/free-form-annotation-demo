# Import data structure
The data should be in JSON format. It should contain a list of samples. 

## Sample
A **sample** has the following structure:

| **Property** | **Type** | **Explanation** |
|---|---|---|
| text | string | Text of the sample (text to be annotated) |
| annotations | AnnotationData \| null | Pre-generated annotations (entities or relationships). Can be used to create suggestions for the annotator |
| metadata | Metadata \| null | Contains metadata unique to the given sample. Consists of unique entity/relationship tags for the given sample |

## AnnotationData

**AnnotationData** object has the following structure:

| **Property** | **Type** | **Explanation** |
|---|---|---|
| entities | Array\<Entity\> | List of pre-generated entities |
| relationships | Array \<Relationship\> | List of pre-generated relationships |

## Entity
**Entity** object has the following structure:

| **Property** | **Type** | **Explanation** |
|---|---|---|
| id | number | unique ID of the entity |
| start | number | index to the starting character of the entity in the context of the sample text |
| end | number | index to the ending character of the entity in the context of the sample text |
| tag | string \| null | tag given to the entity (e.g. NOUN, VERB or any custom tag) |
| color | string \| null | hex color string, determines the highlight color of the entity |
| notes | string \| null | any additional information about the entity |

## Relationship
**Relationship** object has the following structure:

| **Property** | **Type** | **Explanation** |
|---|---|---|
| id | number | unique ID of the relationship |
| entity1 | number | ID of the first entity |
| entity2 | number | ID of the second entity |
| name | string | name of the relationship (can be used to capture the purpose, e.g. has/is/coreference, etc.) |
| color | string \| null | hex color string, determines the color of the relationship box and the arrow |