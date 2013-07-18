solr-unstructured-index
=======================

Unstructured text file is not easy to index as it does not have 'id' in Solr. However, Solr supports indexing unstructured text file. This illustrates how to index unstructured text file.

#### Using uuid schema.xml

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

And, we need to remove or comment elevate.xml at solrconf.xml, which is to . Note: 
```bash
<!-- searchComponent name="elevator" class="solr.QueryElevationComponent" -->
    <!-- pick a fieldType to analyze queries -->
    <!-- str name="queryFieldType">string</str>
    <str name="config-file">elevate.xml</str>
  </searchComponent -->

```
#### Sample unstructured text file
Sample unstructured text file is the number of paragraphs separated by lines (carriage return). For example, Shakespeare's King Henry IV has:
```bash
...
FALSTAFF        Shall I? O rare! By the Lord, I'll be a brave judge.

PRINCE HENRY    Thou judgest false already: I mean, thou shalt have
        the hanging of the thieves and so become a rare hangman.

FALSTAFF        Well, Hal, well; and in some sort it jumps with my
        humour as well as waiting in the court, I can tell
        you.

PRINCE HENRY    For obtaining of suits?

...
```

The file is composed of character name and dialogue. Thus, we could use two field names: character_name and dialogue, 
which are of text field types including dynamicField listed at schema.xml of the Solr example.
```bash
...
<field name="name" type="text_general" indexed="true" stored="true"/>
...
<dynamicField name="*_txt" type="text_general"   indexed="true"  stored="true" multiValued="true"/>
...
```

#### Indexing unstructured text file
We could use 
```bash
```

#### References
##### 1. Apache Solr 4 Cookbook, Rafal Kuc, Jan 2013, Packt Publishing Ltd
