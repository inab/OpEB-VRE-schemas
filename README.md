# oeb

My project is to make a json schema to validate the tools of the openebench website.

This json schema validator we want to linked to an ontology because we have that validation in mongo with collections.

##json_schema_mongodb.json

##tool_schema_internal_MuG.json
A json schema for MuG.

##tool_schema_internal_OEB.json
A json schema for OEB. Is to validate all the data the developer introduce. Also we have a mongo collection with extensions of file_type and what datasets accept. For example: dataset aggregation oly accept file_type JSON and TAR and JSON has extension of "json" and TAR extension of "tar".

##protege_folder
We want to do the validation that do mongo with collections with two ontologies. One about formats (FASTA, JSON, TAR,...) linked to ontology EDAM, and other ontology with datasets importing the other ontology and linked to that. 
