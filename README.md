# cu_class_primer_bundle

STEP 1: Prime a site

Assuming the export process from UIS remains consistant, you should recieve 4 tab separated files for the classes in the term you are working with.  Currently these need to converted from tab separated to comma separated.  There several ways to convert them, but the easiest is probably...

```
tr '\t' ',' < ClassDetail.txt > ClassDetail.csv
tr '\t' ',' < ClassMeetingDetail.txt > ClassMeetingDetail.csv
tr '\t' ',' < ClassInstructorDetail.txt > ClassInstructorDetail.csv
```

Once converted, add import each file into a database where the first row are the column titles then export all the tables as a single .sql export.  Currently this file must be manually imported using something like...

```
drush sql-cli < sites/all/modules/custom/cu_class_primer_bundle/cu_classes_primer.sql
```

This will not directly import the classes as entities, but simply mimics the XML of the API so that the site can be pointed at itself to prime the courses and classes before a term is available through the API.

A site can be primed from itself, but in most cases you will want to prime another site to temporarily act as the API.  Once a site is primed to provide the course data, confirm that the expected XML is being displayed when accessing primer/courses/CUBLD/2164/HIST where the last 3 parts of the URL are the institution, term, and subject codes.  Now add the base url of that site to the consuming site in the Class Import Configuration . 

STEP 2: Course Import

course/import - Will import all courses matching the instituion, term, and subject selected

STEP 3: Class Import

class/import - Shows a list of courses.  Will create class entities for all classes/sections in this course

TODO: Still working on the updating the courses via cron.  Becuase the number of queries we are allowed to make is limited by the API key that all Express sites currently share, we need to figure out how often sites can update each course.



