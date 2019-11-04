---
layout: default
title:  "Connecting Responsys with Ematic"
categories: New-To-Ematic
order: 7
---

# Connecting Responsys with Ematic

Before you could start sending out Hi-iQ list in your Responsys account, it is essential to create connect jobs between Responsys and Hi-iQ. There are a total of 5 set ups required:
1. Setting up SFTP folder
2. Setting up Export feed data
3. Setting up Export Profile list data
4. Create a Profile Extension Table (PET)
5. Setting up Import Profile Extension Data 

## Setting up SFTP folder
---
#### 1. Add integration@ematicsolutions.com to your Responsys account with Super User role, Data Director, Email Analytics Manager, Reporting Administrator and Reporting Manager by going to Account > Add or Manage Users.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/add_user.png" style="width:500px">

#### 2. Share your credentials of your Oracle Responsys SFTP for the export and import of data.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/ftp_credentials.png" style="width:500px">

## Setting up Export feed data 
---
#### 1. Responsys and Hi-iQ needs to communicate the same data. To set this, select these Event Types on your Events Export:
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/events_export.png" style="width:500px">
<pre class="highlight" style="background-color: #DAEFFD; color:#2B6A94; white-space:pre-line; display: inline-block">
<strong>Info:</strong> Do ensure that you do not miss any event types. However, you may select more than the essentials.
</pre>

#### 2. Upon successful set up, the data will be made in the indicate File Location, like so:
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/events_export_file_location.png" style="width:500px">

#### 3. Set a schedule to the Contact Events Export. We highly recommend to set it at 6 times a day.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/events_export_schedule.png" style="width:500px">

## Setting up Export Profile list data
---
#### 1. Next, to set up the export to your Profile List. Name this export job Z_EMATIC_EXPORT_LIST
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/contacts_export.png" style="width:500px">

#### 2. Create a naming convention with YYYYMMDD_LIST_[name of your Profile List from the previous screenshot] like so:
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/contacts_export_naming.png" style="width:500px">

#### 3. Set a schedule to the Profile list Export to run daily.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/contacts_export_schedule.png" style="width:500px">

## Create a Profile Extension Table (PET)
---
#### 1. Create a Profile Extension Table (PET). Create a folder and name it “z_ematic”.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/pet_creation1.png" style="width:500px"><br>
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/pet_creation2.png" style="width:500px">

#### 2. Next, specify the fields in the PET. Go to Data > Select the appropriate list > Profile Extensions Tab > Create Profile Extension Table > Specify Fields
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/pet_creation3.gif" style="width:500px">

#### 3. Fill the first First Field Name with ‘Email’ and ‘Medium Text Field’ for Data Type. Click Next.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/pet_creation_fields.png" style="width:500px">

#### 4. To ensure that you have set the PET up correctly, go to Folder and the PET will be there.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/pet_creation_verification.png" style="width:500px">

## Setting up Import Profile Extension Data
---
#### 1. Create a connect job name Z_EMATIC_IMPORT_HI-IQ
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/import_pet_creation1.png" style="width:500px">

#### 2. To match the PET created in the earlier steps, Check "Remove all existing records" and match "Email_address_".
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/import_pet_creation2.png" style="width:500px">

#### 3. Set to match incoming field "Email" to "Email_Aaddress_".
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/import_pet_fields.png" style="width:500px">

#### 4. A distro will be provided to you to be included in this step.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/import_pet_distro.png" style="width:500px">

#### 5. Set a schedule according to your preference.
<img src="{{site.baseurl}}/assets/img/connecting-responsys-with-ematic/import_pet_schedule.png" style="width:500px">