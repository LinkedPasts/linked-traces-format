## Linked Traces annotations
**_v0.2 Draft for comment, 19 October 2019._** 

*Pursuant to suggestions, the scope of Linked Traces has been expanded. In the first draft ([v0.1](README_20190321.md)) only annotations having place identifier content were considered, in order to meet requirements of the [Peripleo](http://peripleo.pelagios.org) and [World Historical Gazetteer](http://whgazetteer.org) platforms. By consensus, Linked Traces should concern Web Annotations of historical entities more generally, and include or reference multiple domain- and application-specific patterns.*

### Traces
The term "trace" refers to annotations of records about historical entities of any kind. Trace data takes the form of a [W3C web annotations](https://www.w3.org/TR/annotation-model/). The annotation **_Target_** is a _web resource_ [1], and the annotation **_Body_** either embeds RDF as text in a "value" or "textBody" attribute or links to an external RDF record with its "id" attribute.

Traces have already been indexed and displayed in the [Peripleo web application](http://peripleo.pelagios.org) developed by Rainer Simon for the [Pelagios](http://commons.pelagios.org) project; to date these are principally records of coins and inscriptions annotated with identifiers for places as "findspots" in the Classical Mediterranean region. 

In this new conception, Linked Traces amounts to a set of use patterns for the W3C Web Annotation [model](https://www.w3.org/TR/annotation-model/) and [vocabulary](https://www.w3.org/TR/annotation-vocab) to accommodate 

- more kinds of historical entities (not only **artifacts**, but **events** of all kinds, **people**, and **works**, broadly construed), 
- more motivations and use scenarios, e.g. transcriptions of page images
- more detailed content within, or referenced by, the annotation Body

###Issues

1. What are use scenarios for Linked Traces annotations?
2. What should be the model patterns for annotation Body RDF in each domain/scenario?
3. Are those patterns outside the scope of this work? 

### Scenarios and examples

A preliminary list, to be expanded. *NB: W3C Annotations are specified using JSON-LD format (an RDF syntax).*

- **The geographic case**: Annotations of web resources about any sort of historical item with identifiers for relevant places.

> The [World Historical Gazetteer](http://whgazetteer.org) (WHG) and [Peripleo](http://peripleo.pelagios.org) platforms solicit trace annotation contributions, the bodies of which include RDF expressing a setting (a place IRI and optional 'when' statement) and its relation to the entity referenced by the Target (e.g. 'waypoint', or 'findspot'). WHG software will display (and return via API), for an indexed place, any contributed traces associated with it, exposing the Target IRI and the 'when' and 'related' properties embedded in the Body. In this way, traces provide enhanced place description for users of WHG, e.g. place1234 was a waypoint on these several journeys centuries apart, was the findspot for these several artifacts, and was among the settings for this complex historical event. 

```
```

- **The transcription case**: Annotations of archival page images with structured transcriptions of them.

> [Free UK Genealogy](https://freeukgenealogy.org/) is organizing transcription of archival birth registries, which which they will store as RDF and make available via an API. In this case, the page image is the annotation Target (with an IRI as "id"), and the Body could either be only another IRI, to the transcription record for the page, or it could embed that RDF as media type application/rdf in a "value" field.

> The [Recogito]() tool allows users to annotate images, ...

```
```
---
**Contributors**: Karl Grossner (t,gh: @kgeographer); Rainer Simon (t: @aboutgeo, gh:@rsimon), Richard Light (t: @RichardOfSussex, Johannes Scholtz (t:@Joe_GISc)

