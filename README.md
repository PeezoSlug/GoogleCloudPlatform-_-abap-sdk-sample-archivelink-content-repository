
# Google Cloud Storage: Content Server for SAP

This solution utilizes Google Cloud Storage as a content repository to store SAP attachments and archive the data


![alt_text](images/image_architecture.jpg "Google Cloud Storage as Content Server Architecture")



## Pre-requisites

This solution is built on top of [ABAP SDK for Google Cloud](https://cloud.google.com/solutions/sap/docs/abap-sdk/on-premises-or-any-cloud/whats-new). Therefore your SAP system should have the latest version of the SDK installed to proceed ahead. All the required configuration for the SDK to connect to Google Cloud APIs should be set-up following the SDK’s [authentication guide](https://cloud.google.com/solutions/sap/docs/abap-sdk/on-premises-or-any-cloud/latest/authentication).

On your Google Cloud project enable the Google Cloud storage API and set up a bucket with nearline storage.


## Steps to setup Archive Link for Cloud Storage

**Step 1:** Create a background user (user id: ARCHIVEUSER)  to invoke the SICF HTTP Handler class during runtime.

**Step 2:** Create SICF Node for ArchiveLink

![alt_text](images/image1.jpg "New SICF Node")

**Step 3:** Configure the SICF node

*   Configure the user created in the SICF node along with password
*   Mark procedure as “Required with Logon Data” 

![alt_text](images/image2.jpg "SICF Node Configuration")

**Step 4:** Configure the HTTP handler Class

Configure the HTTP handler class that is provide with this repository: `ZGOOG_CL_CONTENT_REPO_GCS`

![alt_text](images/image3.jpg "Handle Class Configuration")

**Step 5:** Setup content server for Cloud Storage

Go to transaction `OAC0` and create an entry for a new content server.

![alt_text](images/image4.jpg)

![alt_text](images/image5.jpg)

![alt_text](images/image6.jpg)

**Step 6:** Link Business Object with Content Repository

1. Go to TCode `OAC3` to setup your business object to be stored in GCS through the Archivelink content repository setup done above, 
2. Here is an example to save Purchase Orders.

![alt_text](images/image7.jpg)


**Step 7:** Configure Google Cloud Content Server for SAP

Configure below in table `ZGOOG_CONT_REPO` provided with this repository by going to transaction SM30

1. Content repository created in SAP 
2. ABAP SDK for Google Cloud Client Key.
3. Google Cloud Storage repository name, where you want to store/archive SAP content.

![alt_text](images/image8.jpg)

