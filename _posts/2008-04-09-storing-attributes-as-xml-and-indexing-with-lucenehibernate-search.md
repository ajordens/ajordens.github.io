---
title: Storing Attributes as XML and Indexing with Lucene/Hibernate Search
author: ajordens
layout: post
permalink: /2008/04/storing-attributes-as-xml-and-indexing-with-lucenehibernate-search/
categories:
  - General Discussions
---
We recently finished a short two week spike that involved using Hibernate Search (backed by Lucene) to index additional attributes that were persisted as an xml snippet stored in CLOB field.

Simple enough goals:

  1. What does the performance curve look like?
  2. Can we search the indexed attributes? <span style="font-style: italic;">(the biggie here was to still be able to do a SQL-like contains query)</span>

**The scenario:**

Imagine the hypothetical <span style="font-style: italic;">Book</span> table and suppose you wanted to provide the ability for end-users to define and store new attributes of the book without having to make structural modifications each time.

The typical solution to this would be to provide a more complex data model alongside the actual entity that allows a user to both define an additional attribute and provide values.

What we wanted to test was the situation where you want to persist 5,000 books at a time w/ upwards of 20 additional attributes. The hypothesis we evaluated was that encoding these attributes in XML and indexing with Lucene would be more performant and just as functional as persisting to a data model that stored attributes as additional records in some other table <span style="font-style: italic;">(or tables)</span>.

**Our implementation:**

    @Entity
    @Indexed
    public class Book implements Serializable
    {
        private Long bookID;
        private String name;
        private String xml;
    
        @Id @GeneratedValue(strategy=GenerationType.AUTO)
        @DocumentId
        public Long getBookID()
        {
            return bookID;
        }
    
        public void setBookID(Long bookID)
        {
            this.bookID = bookID;
        }
    
        /**
         * Getter for property 'xml'.
         *
         * @return Value for property 'xml'.
         */
        @Lob
        @Field(index=Index.TOKENIZED, store = Store.NO)
        @FieldBridge(impl=XMLFieldBridge.class)
        public String getXml()
        {
            return xml;
        }
    
        public void setXml(String xml)
        {
            this.xml = xml;
        }
    }
    
    

    public class XMLFieldBridge implements FieldBridge
    {
        public void set(final String name, 
                        final Object value, 
                        final Document document, 
                        final Field.Store store, 
                        final Field.Index index, 
                        final Float boost)
        {
            if (value == null || "".equals(value))
            {
                return;
            }
    
           for (Attribute attribute : xmlParser.parse((String)value)))
           {
               Field field = new Field(attribute.name, attribute.value, store, index);
               if (boost != null
               {
                  field.setBoost(boost);
               }
               document.add(field);
            }
        }
    }
    

<span style="font-style: italic;">There really isn&#8217;t much more than this. Some of the details (ie. XML parsing) have been left out for brevity. Hibernate Search requires you to use annotations for the Lucene aspects but you&#8217;re free to using traditional xml-based (HBMs) configuration for ORM mappings.</span>

**  
**

**The results:**

By and large the results were pretty good. We did setup asynchronous indexing <span style="font-style: italic;">(</span><span style="font-style: italic;">but on the same physical machine)</span> which worked quite well. There was still fairly significant overhead associated with the actual XML parsing that was somewhat unavoidable. Once the XML was parsed the indexing did occur post-transaction which didn&#8217;t add any additional overhead.

Performance was pretty good too (<span style="font-style: italic;">roughly constant time depending on the amount of data being indexed</span>). Even with indexing on the same box <span style="font-style: italic;">(5 indexing threads)</span> the persistence time for 5,000 books and 20 extra attributes was in the same ballpark as persisting multiple records in the more complex data model.

If indexing were offloaded to another box, I’m confident that it would have been **significantly faster** <span style="font-style: italic;">(this was somewhat verified by inserting a Thread.sleep() between test iterations to sure that the backgrounded indexing had completed prior to starting another test iteration).</span>

The actual post-transaction indexing wasn’t particularly speedy <span style="font-style: italic;">(tokenizing and indexing).</span> There was <span style="font-style: italic;"><strong>significant</strong></span> **<span style="font-style: italic;">time</span>** spent indexing when re-indexing 500,000 -> 1,000,000 records.

What actually proved to be a show stopper was the inability to do a SQL-like contains query. Lucene does has an analyzer that allows you to do a <span style="font-style: italic;">starts with</span> query but nothing more complex than that. To Lucene’s credit, it isn’t particularly efficient to do this in most databases. If worse came to worse, I suspect we could have implemented our own Lucene analyzer.

Hibernate Search was quite easy to work with. Using annotations made sense and once we got past a few maven annoyances life was pretty smooth. Documentation was quite well done and covered most everything we wanted to test.

It doesn’t support the latest release of Lucen but I trust that will be coming at some point. Unless the API has changed, you may be able to use a newer version of Lucene but without access to it’s APIs via the Hibernate SearchFactory?