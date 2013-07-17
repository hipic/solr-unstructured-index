solr-unstructured-index
=======================

Unstructured text file is not easy to index as it does not have 'id' in Solr. However, Solr supports indexing unstructured text file. This illustrates how to index unstructured text file.

#### Using uuid

Unstructured text file is composed of number of words for a line so that we could create UUID as each line's id field and the line becomes a text to index.
In order to use uuid, schema.xml file should be updated.

At $SOLR_HOME/example/solr/[your collection name]/conf/schema.xml, you need to insert the following uuid filed name and type. 
Besides, you need to remove 'id' field and its uniqueKey element.
```bash
   <!-- field name="id" type="string" indexed="true" stored="true" required="true" multiValued="false" /-->
   <field name="uid" type="uuid" indexed="true" stored="true" default="NEW" multiValued="false" />
...
    <fieldType name="uuid" class="solr.UUIDField" indexed="true" />
...
    <!-- uniqueKey>id</uniqueKey -->  
```

```bash
```

#### References
##### 1. Apache Solr 4 Cookbook, Rafal Kuc, Jan 2013, Packt Publishing Ltd
