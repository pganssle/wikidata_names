# WikiData Names Data Set

This is a data set of human names, pulled from [WikiData](https://wikidata.org). It was extracted using the [WikiData Query Service](https://query.wikidata.org/). WikiData itself is a [CC-0](https://creativecommons.org/share-your-work/public-domain/cc0/) data set, and this derived data set is also available as CC-0.

WikiData [has a hard timeout of 60 seconds](https://en.wikibooks.org/wiki/SPARQL/Wikidata_Query_Service#Query_timeout), and so I was unable to run a single query that pulled in all the information I wanted. The best way I found to extract the list of people without taking forever or hammering WikiData's servers was to run queries for all people born within a specific range of time. This will necessarily exclude people whose birthdays are not included in their WikiData entry.

## Data location

The data can be found in the <a href="https://github.com/pganssle/wikidata_names/tree/pages/data">data folder</a>. The most recent version is [`2021-04-23-wikidata-names-00.json.bz2`](data/2021-04-23-wikidata-names-00.json.bz2). This is the first published version, and contains data scraped from people born between 1850 and 2020.

## Data Format
The data is collected in a large compressed JSON file. The top level of the JSON file has two entries: `metadata` and `data`. Additional entries may be added to the top level or to `metadata` at any time.

### The `metadata` section

The `metadata` section contains the following keys:

- `columns`: A mapping between column names and their types (taken directly from the WikiData types). Currently the data only contains types `uri` (a link to the Wikidata entry) and `literal` (for data labels). This does not capture whether a given column is singled-valued or can have multiple values.

### The `data` section

The data section is a list of mappings between column name and value. Most columns are optional, and when no value for the column is found in WikiData, the column is missing in the mapping. Some columns can only have a single value (e.g. `item`, which is the URI corresponding to the unique WikiData entry), while others can have multiple values (e.g. `given_name`, since many people have multiple given names). If a column supports multiple values, it will be a  list, even if the list has only one entry.

An example entry:

```json
{
  "item": "http://www.wikidata.org/entity/Q13396290",
  "item_label": "Jozef M\u00e1jovsk\u00fd",
  "gender": "male",
  "given_name": [
    "Jozef"
  ],
  "ethnicity": [
    "Slovaks"
  ],
  "country_of_citizenship": [
    "Slovakia",
    "Czechoslovakia"
  ]
}
```


