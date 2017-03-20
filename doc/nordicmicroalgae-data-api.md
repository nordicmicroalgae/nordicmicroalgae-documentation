
# Nordicmicroalgae Data API

## Overview

Provides information about taxa and their related resources, such as biovolumes, external links, media etc. Requests are made through HTTP and the response format is JSON.

## List of taxa

http://api.nordicmicroalgae.org/taxa.json

Retrieve a list of taxa. The list may be filtered using different parameters. All parameters are optional and can be used in conjunction with each other.

Available parameters

- name_status - “accepted” or “synonym”. Default is “accepted”
- name - e.g “Dinophysis” or “\*acuta” (\* can be used as wildcard)
- rank - e.g rank=species
- filters - e.g filters[Illustrated only]=True or filters[a][]=One&filters[a][]=Two
- per_page - e.g per_page=10
- page - e.g per_page=10&page=5

### Example 1 - Full list of accepted names

**GET: http://api.nordicmicroalgae.org/taxa.json**

    {
      "taxa": [
        {
          "name":"Abollifer",
          "author":"",
          "rank":"Genus"
        },
        …
      ]
    }

### Example 2 - Full list of synonym names

**GET: http://api.nordicmicroalgae.org/taxa.json?name_status=synonym**

    {
      "taxa": [
        {
          "synonym_name":"Acanthococcus aciculiferus",
          "synonym_author":"Lagerh.",
          "name":"Trochiscia aciculifera",
          "author":"(Lagerh.) Hansg.",
          "rank":"Species"
        },
        …
      ]
    }

### Example 3 - Search for synonym names that contains “acuminata”

**GET: http://api.nordicmicroalgae.org/taxa.json?name=*acuminata*&name_status=synonym**

    {
      "taxa": [
        {
          "synonym_name":"Dinophysis acuminata",
          "synonym_author":"",
          "name":"Dinophysis skagii",
          "author":"Paulsen, 1949",
          "rank":"Species"
        }
      ]
    }

### Example 4 - Paged list with 30 items per page on page 1

**GET: http://api.nordicmicroalgae.org/taxa.json?page=1&per_page=30**

    {
      "taxa": [
        {
          "name":"Abollifer",
          "author":"",
          "rank":"Genus"
        },
        …
      ],
      "total":6600,
      "page":1,
      "pages":220,
      "per_page":30
    }

### Example 5 - Filtered list: Diatoms

**GET: http://api.nordicmicroalgae.org/taxa.json?filters[Group]=Diatoms**


    {
      "taxa":[
        {
          "name":"Acanthoceras zachariasii",
          "author":"(Brun) Simonsen",
          "rank":"Species"
        },
        …
      ]
    }

### Example 6 - Taxa ranked as species

**GET: http://api.nordicmicroalgae.org/taxa.json?rank=species**

    {
      "taxa": [
        {
          "name":"Acanthoceras zachariasii",
          "author":"(Brun) Simonsen",
          "rank":"Species"
        },
        …
      ]
    }

## Taxon

http://api.nordicmicroalgae.org/taxa/\<Scientific name\>.json

http://api.nordicmicroalgae.org/taxa/\<Scientific name\>/\<part\>.json

Retrieve name, author, rank, facts and other related information for one taxon. Scientific name is used as identifier. All information, or just a subset of the available information can be retrieved in one request.

The URL format for retrieving all information is:

    http://api.nordicmicroalgae.org/taxa/\<Scientific name\>.json

The URL format for retrieving a subset (or a specific part) of information is:
http://api.nordicmicroalgae.org/taxa/\<Scientific name\>/\<part\>.json
where \<part\> must be one the following:

- navigation
- facts (includes facts, external_facts and facts_peg)
- external_links
- media
- synonyms

### Example 1 - Media for Dinophysis acuta

**GET: http://api.nordicmicroalgae.org/taxa/Dinophysis acuta/media.json**

    {
      "media":[
        {
          "media_id":
          "Dinophysis acuta_1.gif",
          "media_type":"image",
          "user_name":"0",
          "metadata":{
            "Caption":"Living cells (BF)",
            "Date added":"2007-10-28 23:03:51",
            "Media format":"image\/gif",
            "Title":"Dinophysis acuta",
            …
          },
          "small_url":"http:\/\/media…\/small\/Dinophysis acuta_1.jpg",
          "large_url":"http:\/\/media…\/large\/Dinophysis acuta_1.jpg",
          "original_url":"http:\/\/media…\/original\/Dinophysis acuta_1.jpg"
        },
        …
      ]
    }

### Example 2 - All available information for Dinophysis acuta

**GET http://api.nordicmicroalgae.org/taxa/Dinophysis acuta.json**

    {
      "name":"Dinophysis acuta",
      "author":"Ehrenb.",
      "rank":"Species",
      "navigation":{
        "prev_in_rank":"Dinophysis acuminata",
        "next_in_rank":"Dinophysis arctica",
        "next_in_tree":"Dinophysis arctica",
        "prev_in_tree":"Dinophysis acuminata",
        "classification":"Protozoa:Kingdom;…;Dinophysis acuta:Species",
        "parent":"Dinophysis",
        "children":"",
        "siblings":"Dinophysis acuminata:0;…;Dinophysis tripos:0"
      },
      "facts":{
        "Life form":"Solitary",
        "Note on taxonomy":"Testar",
        "Resting spore":"",
        "Scientific name":"Dinophysis acuta",
        "Size":"Length 54-94 \u00b5m, width 43-60 \u00b5m",
        "Tropic type":"A\/H",
        …
      },
      "external_facts":{
        "AlgaeBase":{"Algaebase id":"52218"},
        "Dyntaxa":{"Dyntaxa id":"238460"},
        "Generated facts":{"IDs in other systems":"…"},
        "IOC":{"Harmfulness, IOC":"…"}
      },
      "facts_peg":{
        "Author":"Ehrenberg 1839",
        "Class":"Dinophyceae",
        "Division":"DINOPHYTA (PYRROPHYTA)",
        "Formula":"p\/6*l*d1*d2",
        "Geometric shape":"flattened ellipsoid",
        "Order":"DINOPHYSALES",
        "Size classes":[…],
        "Species":"Dinophysis acuta",
        "Trophy":"MX"
      },
      "external_links":[
        {"provider":"AlgaeBase","type":"Taxon URL","value":"…"},
        {"provider":"Dyntaxa","type":"Taxon URL","value":"…"},
        {"provider":"IOC","type":"Taxon URL","value":"…"}
      ],
      "media":[…]
      "synonyms":[]
    }

## Media list

    http://api.nordicmicroalgae.org/media.json

Retrieve a list of media items. The list may be filtered using different parameters. All parameters are optional and can be used in conjunction with each other.

Available parameters

- filters - e.g filters[Gallery]=NOMP
- per_page - e.g per_page=50
- page - e.g per_page=50&page=2

### Example 1 - Full list of media items

**GET: http://api.nordicmicroalgae.org/media.json**

    {
      "media": [
        {
          "media_id":"Acanthoceras zachariasii_1.jpg",
          "media_type":"image",
          "metadata":{
            "Media format":"image\/jpeg",
            "Date added":"2013-08-29 11:05:54",
            "Title":"Acanthoceras zachariasii",
            "Preservation":["Formaldehyde"],
            "Technique":["Light microscopy"],
            …
          },
          "small_url":"http:…/small/Acanthoceras zachariasii_1.jpg",
          "large_url":"http:…/large\/Acanthoceras zachariasii_1.jpg",
          "original_url":"http:…/original\/Acanthoceras zachariasii_1.jpg"
        },
        …
      ]
    }

### Example 2 - Filtered list of media items in the NOMP gallery

**GET: http://api.nordicmicroalgae.org/media.json?filters[Gallery]=NOMP**

    {
      "media": [
        {
          "media_id":"Protoperidinium oblongum_4.jpg",
          "media_type":"image",
          "metadata":{
            "Date added":"2013-11-05 08:21:51",
            "Title":"cf. cyst of Protoperidinium oblongum",
            …
          },
          "small_url":"http:…\/small\/Protoperidinium oblongum_4.jpg",
          "large_url":"http:…\/large\/Protoperidinium oblongum_4.jpg",
          "original_url":"http:…\/original\/Protoperidinium oblongum_4.jpg"
        },
        …
      ]
    }

### Example 3 - Paged list of media with 10 items per page on second page

**GET: http://api.nordicmicroalgae.org/media.json?per_page=10&page=2**

  {
    "media":[
      {
        "media_id":"Achnanthes brevipes_2.jpg",
        "media_type":"image",
        "metadata":{
          "Media format":"image\/jpeg",
          "Date added":"2013-04-26 10:12:04",
          …
        },
        "small_url":"http:…/small\/Achnanthes brevipes_2.jpg",
        "large_url":"http:…\/large\/Achnanthes brevipes_2.jpg",
        "original_url":"http:…\/original\/Achnanthes brevipes_2.jpg"
      },
      …
    ],
    "total":1517,
    "page":2,
    "pages":152,
    "per_page":10
  }

## Media item

    http://api.nordicmicroalgae.org/media/\<Media ID\>.json

Retrieve information about one media item. Media ID is used as identifier and can be found in media lists (such as in responses from the “Taxon” or “Media list” requests).

### Example

**GET: http://api.nordicmicroalgae.org/media/Dinophysis acuta_1.GIF.json**

    {
      "media_id":"Dinophysis acuta_1.gif",
      "media_type":"image",
      "user_name":"0",
      "metadata":{
        "Caption":"Living cells (BF)",
        "Date added":"2007-10-28 23:03:51",
        "Image galleries":["Kuylenstierna","Skagerrak-Kattegat"],
        "Institute":"University of Gothenburg, Marine botany",
        …
      },
      "small_url":"http:…\/small\/Dinophysis acuta_1.jpg",
      "large_url":"http:…\/large\/Dinophysis acuta_1.jpg",
      "original_url":"http:…\/original\/Dinophysis acuta_1.jpg"
    }

## Photographer/artist list

    http://api.nordicmicroalgae.org/media/artists.json

Retrieve a list of media contributors. Each item in the list contains the name of photographer and the total number of contributed images.

### Example

**GET: http://api.nordicmicroalgae.org/media/artists.json**

    {
      "artists":[
        {"name":"Ann-Turi Skjevik","total":"213"},
        {"name":"Bengt Karlson","total":"40"},
        …
      ]
    }

## Settings

    http://api.nordicmicroalgae.org/settings.json
    http://api.nordicmicroalgae.org/settings/\<Settings Key\>.json

Retreieves all or a specific subset of settings.

### Example 1 - All settings

**GET: http://api.nordicmicroalgae.org/settings.json**

    {
      "Filter groups":{
        "Group list":["Diatoms","Dinoflagellates",…],
      },
      …
    }

### Example 2 - Species view settings

**GET: http://api.nordicmicroalgae.org/settings/Species view.json**

    {
      "Field list":[
        "External Facts.Generated facts.IDs in other systems",
        "Facts.Note on taxonomy",
        "Facts.Tropic type",
        "Facts.Morphology",
        …
      ]
    }
