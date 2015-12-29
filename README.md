# cu_class_primer_bundle

Assuming the export process from UIS remains consistant, you should recieve 3 tab separated files for the classes in the term you are working with.  Currently these need to converted from tab separated to comma separated.  There several ways to convert them, but the easiest is probably...

tr '\t' ',' < ClassDetail.txt > ClassDetail.csv
tr '\t' ',' < ClassMeetingDetail.txt > ClassMeetingDetail.csv
tr '\t' ',' < ClassInstructorDetail.txt > ClassInstructorDetail.csv

Once converted, add each file to site as file node then configure the pathes in admin/classes/primer.

Select Import.  This will not directly import the classes as entities, but simply mimics the XML of the API so that the site can be pointed at itself to prime the courses and classes before a term is available through the API.
