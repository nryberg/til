# Example Wikidata Query


Triple Format

| Subject | Property |  Object |

### Wikidata Prefixes

_wdt_

* Property
* P Format

_wd_

* Item
* Q Format



[Sample Query] and [Sample Results]
```
SELECT DISTINCT ?item ?itemLabel  (SUM(?population) AS ?pop) ?year WHERE {
  ?item wdt:P31 wd:Q35657;
    p:P1082 ?popStatement.
    
  ?popStatement ps:P1082 ?population;
                pq:P585 ?date.
  BIND(STR(YEAR(?date)) AS ?year)
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
  
}
GROUP BY ?item ?itemLabel ?year 
ORDER BY (?itemLabel)
```
