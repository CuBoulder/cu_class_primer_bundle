# cu_class_primer_bundle

Assuming the export process from UIS remains consistant, you should recieve 4 tab separated files for the classes in the term you are working with.  Currently these need to converted from tab separated to comma separated.  There several ways to convert them, but the easiest is probably...

```
tr '\t' ',' < ClassDetail.txt > ClassDetail.csv
tr '\t' ',' < ClassMeetingDetail.txt > ClassMeetingDetail.csv
tr '\t' ',' < ClassInstructorDetail.txt > ClassInstructorDetail.csv
```

Once converted, add each file to site as file node then configure the pathes in admin/classes/primer.

Select Import.  This will not directly import the classes as entities, but simply mimics the XML of the API so that the site can be pointed at itself to prime the courses and classes before a term is available through the API.

A site can be primed from itself, but in most cases you will want to prime another site to temporarily act as the API.  Once a site is primed to provide the course data, confirm that the expected XML is being displayed when accessing primer/courses/CUBLD/2164/HIST where the last 3 parts of the URL are the institution, term, and subject codes.  Now add the base url of that site to the consuming site in the Class Import Configuration . 

```
`drush sql-connect` < sites/all/modules/custom/cu_class_primer_bundle/cu_classes_primer.sql
```
