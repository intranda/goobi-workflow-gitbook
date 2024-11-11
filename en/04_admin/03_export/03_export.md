# Exporting to digital libraries

Goobi allows users to export processes (together with all their digitised objects) to digital libraries. As a rule, the XML file (METS) is exported last. It is generally preceded by any images, OCR results and other digital objects (e.g. audio files, video files, born digital data).

The following systems (e.g. intranda’s Solr Indexer) monitor the hotfolder and start to function when a specifically defined event occurs. Exporting the XML files last of all ensures that all the other files needed have been made available to the Solr Indexer. In this way, processing can begin as soon as the XML file is exported

The different export parameters can be configured in Goobi. They are located under project properties in the `Technical data` and `Mets parameters` tabs.