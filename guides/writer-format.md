---
layout: default
title: Writer format
active: /guides/
---

# Writer format
In this guide the format used by Newspilot Writer for articles and metadata or "concepts" are described.

## Article format
In order for Newspilot Writer to render and process articles these need to be in a specific format. The format used is based on NewsML which is an IPTC standard (further explained in detail here [https://iptc.org/standards/newsml-g2/](https://iptc.org/standards/newsml-g2/){:target="_blank"}). 

Newspilot Writer is using an extended version of the `NewsItem` to represent articles. The Newspilot Writer NewsItem format is documented here; [https://github.com/Infomaker/writer-format/blob/master/newsml/newsitem/newsitem-text.xml](https://github.com/Infomaker/writer-format/blob/master/newsml/newsitem/newsitem-text.xml){:target="_blank"}.

### Format explained
Below are links to xsd files that can be used to understand and validate the Newspilot Writer format.

- [NewsItem](https://github.com/Infomaker/writer-format/blob/master/validation_service/xsd/Infomaker-NewsItem_ver1.0.xsd){:target="_blank"} - Represent the "whole" article (i.e. metadata and content)
- [Extensions](https://github.com/Infomaker/writer-format/blob/master/validation_service/xsd/Infomaker-NewsML-Extensions_ver1.0.xsd){:target="_blank"} - The extensions to the standard that is used by Newspilot Writer
- [Infomaker Data Format (idf)](https://github.com/Infomaker/writer-format/blob/master/validation_service/xsd/Infomaker-Data-Format_ver1.0.xsd){:target="_blank"} - The format used to represent the actual content of the article (i.e. headlines, text, inline images etc.)

Below are the extensions used in the format explained in more detail.


#### object
The `object` node is an extension to the standard which is used to wrap plugin specific data. Below is an example of how to use the `object` node.

~~~xml
<object id="46f60ada63fd" type="x-im/image" uri="x-im://image/znX8U1CU124n26zu7gb40_jBzSk.jpeg"
    uuid="c382c937-8511-5d48-9677-55658c2bbb32">
    <data>
        <width>1536</width>
        <height>1024</height>
        <text>Maecenas at nisl in lorem egestas egestas.</text>
    </data>
    <links>
        <link title="Jane Doe" rel="author" type="x-im/user" 
        	uuid="bad4314c-7e33-11e5-8bcf-feff819cdc9f"/>
    </links>
</object>
~~~

The attribute `object/@type` is used to map the `object` to a specific plugin. The `object/@id` must be a unique value within the `NewsItem`.

The `data` node wraps any plugin specific data that the plugin might need. 

#### metadata
The `metadata` node is used to wrap `object` nodes that are not located inside the content part (i.e. `idf`) of the article. `object` nodes within `metadata` node represent data that is not "inline" so to say. Example below.

~~~xml
<metadata xmlns="http://www.infomaker.se/newsml/1.0">
    <object id="8400c74d665x" type="x-im/newsvalue">
        <data>
            <score>1</score>
        </data>
    </object>
</metadata>
~~~

### links and link
The `links` node wraps `link` nodes that are used to represent related entities to the article. Example below.

~~~xml
<links xmlns="http://www.infomaker.se/newsml/1.0">
    
    <!-- Related articles -->
    <link title="Quisque pharetra id velit quis commodo" rel="article" type="x-im/article"
        uuid="2175c4bb-fdcc-5a52-bc3b-658562f554cf"/>       
    
    <!-- Articles authors -->
    <link title="John Doe" rel="author" type="x-im/author"
        uuid="9e1653f3-7575-4cb7-9b74-dc4dea63513e"/>
    
</links>
~~~

#### idf
The `idf` (Infomaker Data Format) node wraps the actual content of the article, i.e. headlines, text and inline images etc. It is wrapped by the standard node `inlineXML`. Example below.

~~~xml
<idf xmlns="http://www.infomaker.se/idf/1.0" xml:lang="sv">
    <group type="body">
        <element id="e6b8aa25" type="headline">Secrets of the Emoji World</element>
        <element id="7aa198qw" type="leadin">The party felt like a text-message bubble brought to
            life.</element>
        <element id="8bc7c94e" type="body">On Friday night, more than 400 people gathered here in a
            sleek co-working space near the headquarters of Uber, Pinterest and Airbnb to kick off
            the first Emojicon, a three-day “celebration of all things emoji.” </element>
        <object id="9oc7c92r" uuid="092a051c-a013-57eb-b992-3bb06aaf7601" type="x-im/image">
            <links>
                <link rel="self" type="x-im/image" uri="im://image/g31EiQrY5juw2yOWXoqH8loLQ8Q.jpeg"
                    uuid="092a051c-a013-57eb-b992-3bb06aaf7601">
                    <data>
                        <width>1280</width>
                        <height>852</height>
                        <text>One visitor to Emojicon dressed as the old peach emoji, because she
                            prefers it to the redesigned one, she said.</text>
                    </data>
                    <links>
                        <link rel="author" uuid="00000000-0000-0000-0000-000000000000"
                            title="John Doe"/>
                    </links>
                </link>
            </links>
        </object>
        <element id="5225aa42" type="body">But emoji are more significant than they seem, and with
            Emojicon, Ms. Lee was out to create more than just a good time. </element>
    </group>
</idf>
~~~

### Modifying the format

Using the Newspilot Writer plugin framework it is possible to modify any part of the `NewsItem` as long as it is compliant with the standard and with the Newspilot Writer extensions.

How to use the plugin framework to modifiy the format is explained in the [API Reference]({{site.url}}{{site.baseurl}}/api-reference/){:target="_blank"}.

## Concept format

Concept format can be used to represent different types of metadata such as geodata, categories etc. In order to 
use plugins developed by Infomaker that handle metadata a specific "concept format" - `ConceptItem` - is used. This
format is part of the NewsML standard and is used with some extensions by metadata plugins developed by Infomaker.

Example of `ConceptItems` can be found here; [https://github.com/Infomaker/writer-format/tree/master/newsml/conceptitem](https://github.com/Infomaker/writer-format/tree/master/newsml/conceptitem).
The examples include comments describing the nodes used in the `ContentItem`s. The same extensions to the standard are
used as for the `NewsItem` (see above).

### Example ConceptItem - Geodata (position)
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<conceptItem xmlns="http://iptc.org/std/nar/2006-10-01/" guid="bce38dda-555b-11e5-885d-feff819cdc9f"
    version="1" standard="NewsML-G2" standardversion="2.20" conformance="power">
    <!-- catalog for ninat:, nprov:, irel:, cpnat:, drol:, etc... -->
    <catalogRef href="http://www.iptc.org/std/catalog/catalog.IPTC-G2-Standards_27.xml"/>

    <!-- catalog for infomaker extensions: imchn, imext etc... -->
    <catalogRef href="http://infomaker.se/spec/catalog/catalog.infomaker.g2.1_0.xml"/>

    <itemMeta>
        <itemClass qcode="cinat:concept"/>

        <!-- The party (person or organisation) responsible for the management of the Item. -->
        <provider literal="John Doe"/>

        <!-- Timestamps for created and updated. https://www.ietf.org/rfc/rfc3339.txt -->
        <versionCreated>2015-12-07T15:03:42+00:00</versionCreated>
        <firstCreated>2015-12-07T15:03:42+00:00</firstCreated>
        
        <!-- The publishing status of the Item, its value is "usable" by default. -->
        <pubStatus qcode="stat:usable"/>

        <!-- Extension used to map concept to x-im/place -->
        <itemMetaExtProperty type="imext:type" value="x-im/place"/>        

        <links xmlns="http://www.infomaker.se/newsml/1.0">
            <!-- User that has created the concept. -->
            <link title="John Doe" rel="creator" type="x-im/user"
                uuid="9e1653f3-7575-4cb7-9b74-dc4dea63513e"/>

            <!-- Additional information for the concept. -->
            <link rel="irel:seeAlso" type="text/html" url="http://example.org/alvesta"/>
        </links>
    </itemMeta>
    <concept>
        <!-- Mandatory. @qcode or @uri must be used -->
        <conceptId created="2015-08-11T07:30:42Z" qcode="imcpt:bce38dda-555b-11e5-885d-feff819cdc9f"
            uri="im://place/bce38dda-555b-11e5-885d-feff819cdc9f"/>

        <!-- Mandatory (for writer usage). Identifies the concept as an abstract which maps to "place" -->
        <type qcode="cpnat:poi"/>

        <!-- Mandatory. Name of concept -->
        <name>Alvesta</name>

        <!-- Descriptions -->
        <definition role="drol:long">A long description...</definition>
        <definition role="drol:short">A short description</definition>

        <!--
            To represent geodata we are using WKT, for more info see
            https://en.wikipedia.org/wiki/Well-known_text.
        -->
        <metadata xmlns="http://www.infomaker.se/newsml/1.0">
            <object id="B1Lkp0OqQXo" type="x-im/position">
                <data>
                    <geometry>POINT(14.55600 56.89921)</geometry>
                </data>
            </object>
        </metadata>
    </concept>
</conceptItem>
~~~
