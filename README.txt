The following distribution contains VEDAMO to Salesforce integration APP.
Before deploying the VEDAMO metadata take a look at package.xml -> this Salesforce members will be replicated in your environment.

--------------------------------------------------------
Deploy instructions
--------------------------------------------------------
1. Install the Salesforce CLI from https://developer.salesforce.com/tools/salesforcecli based on your OS. (The instruction below will follow the Windows OS process)
2. After the installation open CMD navigate to VEDAMO distribution folder: 
3. In CMD execute:
	 sfdx auth:web:login -a TargetOrg
4. After a successful authentication execute in CMD:
   sfdx force:mdapi:deploy -d metadata -u TargetOrg -w -1
5. DONE. The VEDAMO SDK should appear in your Salesforce environment

--------------------------------------------------------
Setup instructions
--------------------------------------------------------
1. Setup Salesforce Named Credentials.
   - Go to your Vedamo Dashboard with your administrative account.
	   - Under the Integrations tab, create a Custom Integration via the "Set Custom Integration" button.
	   - For LMS name enter "Salesforce" and press Enable LTI Integration.
	   - Copy your Consumer Key and Shared Secret
	   
   - Go to your Salesforce environment Setup -> Named Credentials -> External Credentials -> Vedamo -> Principals -> Vedamo -> Actions -> Edit
   - In Authentication Parameters Add
	 - Parameter 1 Name: Username Value: Vedamo Consumer Key
	 - Parameter 2 Name: Password Value: Vedamo Shared Secret
		
2. Setup Salesforce Vedamo Permission Set 
   - Go to your Salesforce environment Profile -> Settings -> Advanced User Details -> Permission Set Assignments -> Edit Assignments
   - Add Vedamo in Enabled Permission Sets
   
--------------------------------------------------------
APP Usage
--------------------------------------------------------
- The purpose of the Vedamo App is to easily onboard you with the Vedamo integration and serve as integration debugging tool.
- Vedamo objects will be represented as Tabs there and you will have Salesforce default Records manipulation UI.
- Altering or skipping the App won't affect the Salesforce->Vedamo communication.  
- Each Custom Object has predefined Flows triggered by a Record Create or Update event.
- Adding or updating Records in Custom Objects will reflect into your Vedamo Academy. 
- In order to automate further you can create custom flows that will manage the Records as you need.

--------------------------------------------------------
Objects
--------------------------------------------------------
Vedamo User
	-> purpose: Creates, Updates or Deletes a user entity in the Vedamo system. 
	-> field:
			-> User ID (Text) Expects the Salesforce ID of the entity you want to represent as a User in Vedamo.
			-> First Name(Text) Expects the First Name of the entity you want to represent as a User in Vedamo.
			-> Last Name (Text) Expects the Last Name of the entity you want to represent as a User in Vedamo.
			-> Password (Text) Expects the Password of the entity you want to represent as a User in Vedamo.
			-> Email (Text) Expects the Email of the entity you want to represent as a User in Vedamo.
			-> Role (Picklist) Expects the role of the entity you want to represent as a User in Vedamo.
			-> API Operation Error (Text Area (Long)) will be populated in case Vedamo API returns an error in the process.
			-> API Operation Status (Text) will populated with a value either "OK" or value "FAIL" (in case there is a problem with the API request to the Vedamo system)
			-> API Object Status (Picklist) will be populated with a value either "active" OR "deleted".
			-> API User ID (Text) will be populated with the Vedamo internal user id.
			
IMPORTANT: Changing Record's "Vedamo API Object Status" field to "deleted" will remove the corresponding object in the Vedamo system. 


Vedamo Session Permalink
	-> purpose: Creates, Updates or Deletes a session permalink in the Vedamo system. 
	-> field:
			-> Permalink Name (Text)   
			-> Permalink Description (Text Area (Long))
			-> Permalink Key (Text) Text that will be part of the session URL. Ex www.vedamo.com/vcl/room/{Permalink Key}
			-> Permalink User ID (Text) The user id that will be set as permalink creator. Found in Vedamo User Object -> User ID Field. 
			-> Session Name (Text) Name of each session opened via the permalink.
			-> Session Description (Text Area (Long)) Description of each session opened via the permalink.
			-> Session Participants Emails (Text Area (Long)) Separated by comma, email addresses that will receive a session invitation links as session guests.
			-> Session Observers Emails (Text Area (Long)) Separated by comma, email addresses that will receive a session invitation links as session observers.
			-> Session Recordable (Number) Should the session be recorded. 0 -> No, 1 -> Yes.
			-> Session Type (Picklist) Determines if the session is for registered users or guests.
			-> SP Audio Receiver (Number) Permission should participants receive audio in the session. 0 -> No, 1 -> Yes.
			-> SP Audio Send (Number) Permission should participants send audio in the session. 0 -> No, 1 -> Yes.
			-> SP Chat In Waiting Room (Number) Permission should participants have a chat in the session waiting room. 0 -> No, 1 -> Yes.
			-> SP Chat Private (Number) Permission should participants have private chat in the session. 0 -> No, 1 -> Yes.
			-> SP Chat View (Number) Permission should participants see chat in the session. 0 -> No, 1 -> Yes.
			-> SP Chat Write (Number) Permission should participants write in chat in the session. 0 -> No, 1 -> Yes.
			-> SP File Download (Number) Permission should participants download files in the session. 0 -> No, 1 -> Yes.
			-> SP File Upload (Number) Permission should participants upload files in the session. 0 -> No, 1 -> Yes.
			-> SP File View (Number) Permission should participants view files in the session. 0 -> No, 1 -> Yes.
			-> SP Fixed Mode (Number) Permission should the session layout be in a fixed mode. 0 -> No, 1 -> Yes.
			-> SP Groups Randomly (Number) Permission should participants be assigned into session groups randomly. 0 -> No, 1 -> Yes.
			-> SP Guests Lock (Number) Permission should the session be locked only for participants with signed URLs. 0 -> No, 1 -> Yes.
			-> SP Layout (Picklist) Permission which layout to be used in the session.
			-> SP Presenter (Number) Permission should participants be presenters in the session. 0 -> No, 1 -> Yes.
			-> SP Room Activated (Number) Permission should the session be reopanable from Vedamo dashboard. 0 -> No, 1 -> Yes.
			-> SP System Check (Number) Permission should the session have a system check. 0 -> No, 1 -> Yes.
			-> SP System Check Once (Number) Permission should the systemcheck should run once per device. 0 -> No, 1 -> Yes.
			-> SP Screen Sharing (Number) Permission should participants be able to request screen sharing in the session. 0 -> No, 1 -> Yes.
			-> SP Simple Mode (Number) Permission should be in simple mode. 0 -> No, 1 -> Yes.
			-> SP Video Individual Show (Number) Permission should have an individual video. 0 -> No, 1 -> Yes.
			-> SP Video Layout (Picklist) Permission which video layout to be used in the session.
			-> SP Video Mosaic Shown (Picklist) Permission which participants should be present in the session video mosaic.
			-> SP Video Mosaic View (Number) Permission should session have mosaic. 0 -> No, 1 -> Yes.
			-> SP Video Send (Number) Permission should the session has video. 0 -> No, 1 -> Yes.
			-> SP Wait For Admin (Number) Permission should participants have to wait for the session host before entering the session. 0 -> No, 1 -> Yes.
			-> SP Waiting Room Mode (Picklist) Permission which participants should be placed in the waiting room.
			-> SP Whiteboard Edit All (Number) Permission should participants can edit all objects on the session whiteboard. 0 -> No, 1 -> Yes.	
			-> SP Whiteboard Export (Number) Permission should participants be able to export the session whiteboard. 0 -> No, 1 -> Yes.
			-> SP Whiteboard View (Number) Permission should participants be able to see the session whiteboard. 0 -> No, 1 -> Yes.
			-> SP Whiteboard Write (Number) Permission should participants be able to write on the session whiteboard. 0 -> No, 1 -> Yes.
			-> API Operation Error  (Text Area (Long)) will be populated in case Vedamo API returns an error in the process.
			-> API Operation Status (Text) will populated with a value either "OK" or value "FAIL" (in case there is a problem with the API request to the Vedamo system)
			-> API Object Status (Picklist) will be populated with a value either "active" OR "deleted". 
			-> API Permalink ID (Text) will be populated with the Vedamo internal permalink ID.
			
			
IMPORTANT: Changing Record's "Vedamo API Object Status" field to "deleted" will remove the corresponding object in the Vedamo system. 


Vedamo Session
	-> purpose: Creates, Updates or Deletes a session entity in the Vedamo system.
	-> field:
		-> Creator User ID (Text) The user id that will be set as session creator. Found in Vedamo User Object -> User ID Field
		-> Name (Text) Name of the session. If left blank the Session Name of the Permalink object will be used.
		-> Description(Text Area (Long)) Description of the session.  If left blank the Session Description of the Permalink object will be used.
		-> Permalink ID (Text) The ID of the Permalink found in Vedamo Permalink Object -> API Permalink ID Field.
		-> API Session ID (Text) The id of the session in the Vedamo System.
		-> API Session Key (Text) The session key of the session in the Vedamo System.
		-> API Session URL (Text Area (Long)) The URL of the session.
		-> API Operation Error (Text Area (Long)) will be populated in case Vedamo API returns an error in the process.
		-> API Operation Status (Text) will populated with a value either "OK" or value "FAIL" (in case there is a problem with the API request to the Vedamo system)
		-> API Object Status (Picklist) will be populated with a value either "active" OR "closed".

IMPORTANT: Changing Record's "Vedamo API Object Status" field to "closed" will close the session in the Vedamo system.

Vedamo Session Participants
	-> purpose: Getting a unique participant session URL for a registered Vedamo user. Redirecting the user to this URL will authenticate the users in the session.
	-> field:
		-> Participant User ID (Text) The ID of the User found in Vedamo User Object -> User ID Field.
		-> Participant Name (Text) The name of the User found in Vedamo User Object -> First Name and Vedamo User Object -> Last Name.
		-> Participant Role (Picklist) The role that the participant will have in the session.
		-> Participant Email (Text) Email of the participant used in combination with Participant Notify (email).
		-> Participant Notify (Picklist) Should the participant receive a session link from the Vedamo system.
		-> Session ID (Text) The ID of the Session found in Vedamo Session Object -> API Session ID Field.
		-> API Participant URL (Text Area (Long)) URL containing the user authentication to the session.
		-> API Operation Error (Text Area (Long)) will be populated in case Vedamo API returns an error in the process.
		-> API Operation Status (Text) will populated with a value either "OK" or value "FAIL" (in case there is a problem with the API request to the Vedamo system)

--------------------------------------------------------
Flows:
--------------------------------------------------------
The Vedamo Custom Flows use Salesforce External Services in order to provide a one way communication between Salesforce and Vedamo systems.
Keep in mind that Salesforce obligates External Services to be in Asynchronous Flow Execution. This means there will be some delay between completing the Record transaction and updating the VEDAMO API Records fields.

--------------------------------------------------------
External Services:
--------------------------------------------------------
The Vedamo External Services are predefined REST requests using the Vedamo API described in OpenApi3 standard.


--------------------------------------------------------
Uninstallation:
--------------------------------------------------------
Delete Vedamo Flows
Delete Vedamo Custom Objects
Delete Vedamo App
Delete Vedamo Permission Set
Delete Vedamo External Services    
Delete Vedamo Named Credentials
Delete Vedamo External Credentials
 
   
   