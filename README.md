## Linked Traces annotations
**_v0.2 Draft for comment, 19 October 2019._** 

*Pursuant to suggestions, the scope of Linked Traces has been modified. In the first draft ([v0.1](README_20190321.md)) only annotations having place identifier content were considered, in order to meet requirements of the [Peripleo](http://peripleo.pelagios.org) and [World Historical Gazetteer](http://whgazetteer.org) platforms. By consensus, Linked Traces should concern Web Annotations of historical entities more generally, and include or reference multiple domain- and application-specific patterns.*

### Traces
The term "trace" refers to web-published resources concerning historical entities of any kind, and conventionally, to the entities themselves. Trace **_data_** takes the form of a [W3C web annotations](https://www.w3.org/TR/annotation-model/). The annotation **_Target_** is a web resource of any type (Text, Image, Dataset, Video, Sound), and the annotation **_Body_** either embeds RDF as text in a "value" or "textBody" attribute, or links to an external RDF record with its "id" attribute. Annotations have **motivations**, which  include *describing*, *linking*, *classifying*, and *tagging*. It is possible to create new motivations; e.g. *transcribing* seems broadly useful.

Traces have already been indexed and displayed in the [Peripleo web application](http://peripleo.pelagios.org) developed by Rainer Simon for the [Pelagios](http://commons.pelagios.org) project; to date these are principally records of coins and inscriptions annotated with identifiers for places as "findspots" in the Classical Mediterranean region. 

In this new conception, Linked Traces amounts to a set of use patterns for the W3C Web Annotation [model](https://www.w3.org/TR/annotation-model/) and [vocabulary](https://www.w3.org/TR/annotation-vocab) to accommodate 

- more kinds of historical entities (not only **artifacts**, but **events** of all kinds, **people**, and **works**, broadly construed), 
- more motivations and use scenarios, e.g. transcriptions of page images
- more detailed content within, or referenced by, the annotation Body

### Issues

1. What are use scenarios for Linked Traces annotations?
2. What should be the model patterns for annotation Body RDF in each domain/scenario?
3. Are those patterns outside the scope of this work?
4. When should Body RDF be embedded as opposed to externally linked to?

### Scenarios and examples

A preliminary list, to be expanded. *NB: W3C Annotations are specified using JSON-LD format (an RDF syntax).*

- **The geographic case**: Annotations of web resources about any sort of historical item with identifiers for relevant places.

> The [World Historical Gazetteer](http://whgazetteer.org) (WHG) and [Peripleo](http://peripleo.pelagios.org) platforms solicit trace annotation contributions, the bodies of which include RDF expressing a setting (a place IRI and optional 'when' statement) and its relation to the entity referenced by the Target (e.g. 'waypoint', or 'findspot'). WHG software will display (and return via API), for an indexed place, any contributed traces associated with it, exposing the Target IRI and the 'when' and 'related' properties embedded in the Body. In this way, traces provide enhanced place description for users of WHG, e.g. place1234 was a waypoint on these several journeys centuries apart, was the findspot for these several artifacts, and was among the settings for this complex historical event. 

```
# places in the lifepath of Gautama Bhudda; json array in body.value

{ "@context":["http://www.w3.org/ns/anno.jsonld",
    { "lpo": "http://linkedpasts.org/ontology/lpo.jsonld"}],
  "id": "http://example.org/annotations/12345",
  "type": "Annotation",
  "creator": {
    "id":"https://orcid.org/0000-1234-2345-6789",
    "name":"Anne Annotator",
    "homepage":"http://annotationist.org"
  },
  "created": "2019-10-18",
  "motivation": "describing",
  "target": [{
    "id": "https://en.wikipedia.org/wiki/Gautama_Buddha",
    "type": "Text",
    "format": "text/html",
    "title": "Gautama_Buddha"
  }],
  "body": {
    "type": "Dataset",
    "format": "application/json",
    "value": [{ 
      "id": "http://whgazetteer.org/places/86438",
      "title": "Lumbini",
      "relation": "lpo:birthplace",
      "when": {"timespans":[{"start": "-0563/-0480"}]}
    },{ 
      "id": "http://whgazetteer.org/places/86001",
      "lpo:title": "Kusinagara",
      "lpo:relation": "lpo:deathplace",
      "lpo:when": {"timespans":[{"start": "-0483/-0400"}]}
    }]
  }
}
```

- **Transcription case #1**: Annotations of archival page images with structured transcriptions of them.

> [Free UK Genealogy](https://freeukgenealogy.org/) is organizing transcription of archival birth registries, which which they will store as RDF and make available via an API. In this case, the page image is the annotation Target (with an IRI as "id"), and the Body could either be only another IRI, to the transcription record for the page, or it could embed that RDF as media type application/rdf in a "value" field.

> Body type A (external):

```
RDF transcription of data from an image of a birth register page 

{
  "@context": "http://www.w3.org/ns/anno.jsonld",
  "id": "http://example.org/anno_0001",
  "type": "Annotation",
  "license”: "<https://opendatacommons.org/licenses/odbl/1-0/>”,
  "creator”: "https://freeukgenealogy.org/volunteers/richardofsussex",
  "created": "2017-05-24",
  "motivation”: "transcription”,
  "target": {
    "type": "Image",
    "id": "https://freeukgenealogy.org/data/b65432"
  },
  "body": {
    "type": "Dataset",
    "format": "application/rdf"
    "id”: "http://example.org/birthregistration/1234”
  }
}
```
> Body type B: (embedded)
> 

```
  "body": {
    "type": "Dataset",
    "format": "application/rdf"
    "value”: '
        @prefix fugont: <https://freeukgenealogy.org/ontology.rdf#> .
        @prefix freeukgen: <https://freeukgenealogy.org/data/> .
        @prefix fugregdist: <https://freeukgenealogy.org/registrationdistricts/> .
        @prefix fugreg: <https://freeukgenealogy.org/registers/> .
        @prefix dc: <http://purl.org/dc/elements/1.1/> .
        @prefix dcterms: <http://dublincore.org/documents/2012/06/14/dcmi-terms/> .
        @prefix crm: <http://www.cidoc-crm.org/sites/default/files/cidoc_crm_v6.2-draft-2015August.rdfs#> .
        freeukgen:bmd12345 a fugont:transcription;
        	crm:P70_documents freeukgen:be23456;
        	dc:creator fugvol:richardofsussex;
        	dc:date "2017-05-24"^^xsd:date;
        	dcterms:license <https://opendatacommons.org/licenses/odbl/1-0/> . 
        freeukgen:be23456 a fugont:registrationevent;
        	crm:P70_documents  freeukgen:b65432;
        	crm:P7_took_place_at fugregdist:Droxford;
        	crm:P70i_is_documented_in fugreg:Droxford_7_72;
        	crm:P4_has_time_span [
        		crm:P82a_begin_of_the_begin "1850-07-01T00:00:00"^^xsd:dateTime; 
        		crm:P82b_end_of_the_end "1850-09-30T23:59:59"^^xsd:dateTime .
        	] .
        freeukgen:b65432 a crm:E67_Birth;
        	crm:P98_brought_into_life freeukgen:b65432_child;
        	crm:P96_by_mother freeukgen:b65432_mother;
        	crm:P97_from_father freeukgen:b65432_father;
        	crm:P4_has_time_span [
        		crm:P82a_begin_of_the_begin "1849-07-01T00:00:00"^^xsd:dateTime; 
        		crm:P82b_end_of_the_end "1850-09-30T23:59:59"^^xsd:dateTime .
        	] .
        freeukgen:b65432_child a crm:E21_Person;
        	crm:P1_is_identified_by "Light, Thomas Edward" .   
    '
  }

```

- **Transcription case #2**: Annotations of ___ with ___.

> The [Recogito](http://recogito.pelagios.org) tool allows users to annotate images, ...
> 

```
sample record
```
<br/>

---
**Contributors**: Karl Grossner (t,gh: @kgeographer); Rainer Simon (t: @aboutgeo, gh:@rsimon), Richard Light (t: @RichardOfSussex, Johannes Scholtz (t:@Joe_GISc)

