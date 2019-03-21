## The Linked Traces Annotation format
*v0.1 Draft for comment, 21 Mar 2019*

### Traces
The term "trace" refers to historical entities for which there is spatial-temporal data of interest. Trace data takes the form of W3C web annotations. The **_target_** is a LOD web-published record of some entity, and the **_body_** (annotation) contains one or more place record URIs, a relation between a place and the target entity, and an optional temporal scoping for each.

Traces have alrady been indexed and displayed in the [Peripleo web application](http://peripleo.pelagios.org) developed by Rainer Simon of the [Pelagios](http://commons.pelagios.org); to date these are principally records of coins and inscriptions annotated with their find spots in the Classical Mediterranean region. This new format is designed to better accomodate more kinds of traces, including not only such **artifacts**, but **events** of all kinds, **people**, and **works**.

The Linked Traces Annotation format (LTA format) will supercede the [Pelagios annotation format](https://github.com/pelagios/pelagios-cookbook/wiki/Joining-Pelagios) (under _The Dataset Summary_ > _Minimum Example_) as a template for contributions of "trace" data to both [World-Historical Gazeetteer](http://whgazetteer.org) and [Pelagios](http://commons.pelagios.org). Hopefully it will be found useful and adopted in other projects.


### Draft Examples
A first take at the LTA format is represented below for convenience, and stored [here](https://github.com/LinkedPasts/linked-traces-format/blob/master/samples_0.01.json). A small working group will refine the model and ensure it conforms to the [W3C Web Annotation Data Model](https://www.w3.org/TR/annotation-model/), [W3C Web Annotation Vocabulary](https://www.w3.org/TR/annotation-vocab/), and more generally the draft spec for [JSON-LD v1.1](https://w3c.github.io/json-ld-syntax/). 

Contribution datasets will include a list of brief records for the annotated items (traces), and a collection of the annotation records themselves.

If you would like to join this discussion, please contact one of the contributors listed below.

---
```
// CONTEXTS
// see lpo context below
{
  "@context":[
    "http://www.w3.org/ns/anno.jsonld",
    { "lpo": "http://linkedpasts.org/ontology/lpo.jsonld"}
  ]
}

// types: HistoricalProcess, Journey, Person, Text (Work?), Artifact

// **
// EVENT (PROCESS)
// **
{
  "@id": " http://my.org/event/98765",
  "type": "lpo:HistoricalProcess ",
  "dc:title": "Diffusion of Islam",
  "dc:description": "yada yada, not too long...",
  "lpo:when": {"timespans":[
    {"start":{"in":"633"},"":{"in":"652"}}
  ]},
  "language": "en",
  "dc:subject": ["cultural diffusion", "Islam"]
}
// ANNOTATIONS
{ "@context":"http://www.w3.org/ns/anno.jsonld",
  "id": "http://my.org/annotations/92837",
  "type": "Annotation",
  "creator": {
    "id":"http://example.org/people/1234",
    "name":"Ima Tracemaker",
    "homepage":"http://tracemaker.org"
  },
  "created": "2019-03-18",
  "motivation": "linking",
  "body": [
    { "id": "http://whgazetteer.org/places/86880",
      "dc:title": "Medina",
      "lpo:relation": "source",
      "lpo:when": {"timespans":[
        {"start":{"in":"634"},"end":{"in":"634"}}
      ]}
    },
    { "id": "http://whgazetteer.org/places/84774",
      "dc:title": "Hejaz",
      "lpo:relation": "target",
      "lpo:when": {"timespans":[
        {"start":{"in":"632"},"end":{"in":"634"}}
      ]}
    }
    // ... etc.
  ],
  "target": {
    "id": "http://my.org/event/98765",
    "type": "lpo:HistoricalProcess",
    "dc:title" "Diffusion of Islam"
  },
}

// **
// EVENT (JOURNEY)
// **
{
  "@id": " http://my.org/event/90001",
  "type": "lpo:Journey",
  "dc:title": "Pilgrimage of Xuanzang",
  "dc:description": "yada yada, not too long...",
  "lpo:when": {"timespans":[
    {"start":{"in":"630"},"end":{"in":"645"}}
  ]},
  "language": "en",
  "dc:subject": ["Buddhism","pilgrimage"]
}
// ANNOTATIONS
{ "@context":"http://www.w3.org/ns/anno.jsonld",
  "id": "http://my.org/annotations/92837",
  "type": "Annotation",
  "creator": {
    "id":"http://example.org/people/2345",
    "name":"Ima Tracemaker",
    "homepage":"http://tracemaker.org"
  },
  "created": "2019-03-18",
  "motivation": "linking",
  "body": [
    { "id": "http://whgazetteer.org/places/86880",
      "dc:title": "Tashkent",
      "lpo:relation": "lpo:waypoint",
      "lpo:when": {"timespans":[
        {"start":{"in":"630"},"end":{"in":"630"}}
      ]}
    },
    { "id": "http://whgazetteer.org/places/84774",
      "dc:title": "Mathura",
      "lpo:relation": "lpo:waypoint",
      "lpo:when": {"timespans":[
        {"start":{"in":"634"},"end":{"in":"634"}}
      ]}
    }
    // ... etc.
  ],
  "target": {
    "id": "http://my.org/event/90001",
    "type": "lpo:Journey",
    "dc:title" "Pilgrimage of Xuanzang"
  },
}

// **
// PERSON
// **
{
  "@id": "https://en.wikipedia.org/wiki/Kʼinich_Janaabʼ_Pakal",
  "type": "Person",
  "dc:title": "Kʼinich Janaabʼ Pakal",
  "dc:description": "yada yada, not too long...",
  "lpo:when": {"timespans":[
    { "start": {"in":"0603-03-21"},
      "end": {"in":"0683-08-26"}
    }
  ]},
  "language": "en",
  "dc:subject": ["Maya","ajaw"]
}
// ANNOTATIONS
{ "@context":"http://www.w3.org/ns/anno.jsonld",
  "id": "http://my.org/annotations/92837",
  "type": "Annotation",
  "creator": {
    "id":"http://example.org/people/2345",
    "name":"Ima Tracemaker",
    "homepage":"http://tracemaker.org"
  },
  "created": "2019-03-18",
  "motivation": "linking",
  "body": [
    { "id": "http://whgazetteer.org/places/12352710",
      "dc:title": "Palenque",
      "lpo:relation": [
        "lpo:birthplace",
        "lpo:deathplace"
      ],
      "lpo:when": {"timespans":[
        {"start":{"in":"0603-03-21"}}
      ]}
    }
    // ... etc.
  ],
  "target": {
    "id": "http://my.org/people/80001",
    "type": "lpo:Person",
    "dc:title" "Kʼinich Janaabʼ Pakal"
  },
}

// **
// TEXT
// **
{
  "@id": "https://lccn.loc.gov/99019900",
  "type": "Text",
  "dc:title": "Gods and Goddesses of the Ancient Maya",
  "dc:description": "yada yada, not too long...",
  "when": {"timespans":[
    { "start": {"in":"1999"}}
  ]},
  "language": "en",
  "dc:subject": ["Maya","gods","goddesses"]
}
// ANNOTATIONS
{ "@context":"http://www.w3.org/ns/anno.jsonld",
  "id": "http://my.org/annotations/92837",
  "type": "Annotation",
  "creator": {
    "id":"http://example.org/people/2345",
    "name":"Ima Tracemaker",
    "homepage":"http://tracemaker.org"
  },
  "created": "2019-03-18",
  "motivation": "linking",
  "body": [
    { "id": "http://whgazetteer.org/places/12347857",
      "dc:title": "Copán",
      "lpo:relation": ["dc:subject"]
    },
    { "id": "http://whgazetteer.org/places/12355022",
      "dc:title": "Tikal",
      "lpo:relation": ["dc:subject"]
    },
    // ... etc.
  ],
  "target": {
    "id": "https://lccn.loc.gov/99019900",
    "type": "lpo:Text",
    "dc:title" "Gods and Goddesses of the Ancient Maya"
  },
}

// **
// ARTIFACT
// **
{
  "@id": "https://www.britishmuseum.org/explore/a_history_of_the_world/objects.aspx#9",
  "type": "lpo:Artifact",
  "dc:title": "Maya Maize God Statue",
  "dc:description": "yada yada, not too long...",
  "lpo:when": {"timespans":[
    { "start": {"in":"0715"}}
  ]},
  "language": "en",
  "dc:subject": ["Maya","gods"]
}
// ANNOTATIONS
{ "@context":"http://www.w3.org/ns/anno.jsonld",
  "id": "http://my.org/annotations/92837",
  "type": "Annotation",
  "creator": {
    "id":"http://example.org/people/2345",
    "name":"Ima Tracemaker"
  },
  "created": "2019-03-18",
  "motivation": "linking",
  "body": [
    { "id": "http://whgazetteer.org/places/12347857",
      "dc:title": "Copán",
      "relation": ["findspot"]
    }
  ],
  "target": [
    { "id": "https://www.britishmuseum.org/explore/a_history_of_the_world/objects.aspx#9",
      "type": "lpo:Artifact",
      "dc:title" "Maya Maize God Statue"
    }
  ],
}

// ***
// Linked Pasts context
// ***
{
  "@context": {
    "lpo": "http://linkedpasts.org/ontology/#",
    "Event":              "lpo:Event",
    "HistoricalProcess":  "lpo:HistoricalProcess",
    "Journey":            "lpo:Journey",
    "relation":           "lpo:relation",
    "when":               "lpo:when",
    "waypoint":           "lpo:waypoint",
    "findspot":           "lpo:findspot",
    "birthplace":         "lpo:birthplace",
    "deathplace":         "lpo:deathplace"
  }
}
```
---
Contributors: Karl Grossner (@kgeographer); Rainer Simon (@rsimon)


