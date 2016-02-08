# CU Class Primer Bundle

This project is used to provide XMl in the same format as the UIS Class API with data from an export. This is essential when importing classes to start developing a site before a term is published using the API (ie. Summer Session) or when the data you'd like to filter classes is only found in the detail mode of the API (ie. CU Connect). To find the ~2,000 classes that are offered online accross all CU instituions, we'd have to query all courses for all instituions for all upcoming semesters.  That would require parsing > 76,000 classes every 24 hours to know if any new classes have been offered.  Instead, a query that only includes the online classes can be periodically exported by UIS to use with the primer.

STEP 1: Prime a site

~~Assuming the export process from UIS remains consistant, you should recieve 4 tab separated files for the classes in the term you are working with~~.  EXPORTS FROM UIS ARE STILL INCONSISTANT AS OF 2/8/2015.  Currently we are using a PSQuery export manually created by Continuing Education.

Currently these need to converted from tab separated to comma separated.  There several ways to convert them, but the easiest is probably...

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



