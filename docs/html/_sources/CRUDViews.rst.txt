CRUDViews
====================

Views Distribution
------------------

Tables for organisms' data are: 
Organism, Taxonomy, Organism_Batch,OrgBatch_Image, OrgBatch_Stock, Organism_Culture, 
Drug, Breakpoint, VITEK_Card, VITEK_AST, VITEK_ID, MIC_COADD, MIC_Pub
Gene, ID_Pub, ID_Sequence, WGS_FastQC, WGS_CheckM,
Organisation, Collab_User, Collab_Group, Data_Source,
Screen_Run,
Document,

Tables for Application settings and utils are:
ApplicationUser, AuditModel, Dictionary, ApplicationLog

The general Read Data View in tables or cards are available in current application are for 
Organism, Taxonomy, OrgBatch_Stock, Drug, Breakpoint, VITEK_Card, VITEK_AST, VITEK_ID, MIC_COADD, MIC_Pub. 
The detail views for individual data entry are only for Taxonomy, Organism and Drug, where are update and delete functions located.
The CRUD views for Organism_Batch, OrgBatch_Image, OrgBatch_Stock(ChildTable of Organism_Batch) and Organism_Culture are in Organism Detail View since Organism as main foreignkey for them.

Only Admin can access ApplicationUser and Dictionary CRUDviews.

Views Layouts
--------------
General Table Views include:
 * the switch-views and create new buttons on left vertical bar
 * sidebar on main view left inlcude filter and the main view right part is the data table
 * pagination displaying, selection and download function in main view top horizontal bar 

General Views for Drug, Organism and Taxonomy are also in card views with data table replaced by cards

Detail Views for Drug, Taxonomy with lefticon contain: update / delete buttons and main parts are groupped detail information table.
Detail Views for Organism include related Organism_Batch, OrgBatch_Stock, Organism_Culture, OrgBatch_Image, micbiogram and Organism detail in collapsible sections. 


Export on General Read Data View
---------------------------------

The exprot data on main view top horizontal bar of each General Read Data View works with the filter (on sidebar). The data could be export via individual select button 
in front of each data row or via select all filtered result in either .csv or .xlsx format. 

Import
-------

Import function is currently only available to import vitekcard, vitek_id and vitek_ast data from .pdf files. The navigate button is on to navigate bar under Import menu. 
3 Steps in importing:


- Firstly select files to upload and validate:

  selecting one or more files to upload, should be in pdf.

  Uploading files via validation file type(must be valid .pdf), then will be pased into data list and verified with database. 

- Select Batch ID and Save to DB:

  Return validated result from first step. If validation passed, select BatchID if needed, and save to database else cancel or go back to correct data in database then start again.

- Finalizing import.

