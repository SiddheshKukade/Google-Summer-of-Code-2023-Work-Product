# Google-Summer-of-Code-2022-Work-Product

## Project Details : 

#### Organization : [The Palisadoes Foundation](https://github.com/PalisadoesFoundation/)
#### Project Name : Refactoring Plugins to WebSockets & Implementing Advertisement feature
#### Problem Statement :  
There are a number of features that while useful are not absolutely necessary for the base Talawa app and would be better suited as plugins. The goal of this task is to refactor the existing plugins such as Newsfeed Advertising, Spam Mitigation, Inter-group Messaging, Analytics Integration, Check-ins functionality, etc. We recommended that you use our Plugin Guide. The scope of the Newsfeed Advertising and Spam Mitigation are given below. They can act as a template for the any additional plugins you wish to discuss with the mentors.

**Newsfeed Advertising**: Community organizations often rely on the support of local businesses. This plugin would allow companies to advertise on the mobile application newsfeed. The plugin must consider both inexperienced advertisers who will only provide an image or video, and those who are more experienced users of online platforms.
Features
The type of content and ways to upload and display it (product placement) must be considered.
The plugin must provide a comprehensive set of advertising campaign features.
Integration with other advertising platforms should be considered.


### Project Progress Tracker: https://github.com/orgs/PalisadoesFoundation/projects/11/views/1

## Issue and Pull requests :

## 1. Refactoring Plugin architecture by transitioning into websockets.
  The plugin in talawa application  works just like a browser extension works in a browser. The difference here is that the plugin store from which the plugin is installed is handled by the admin of that organization and are used by the members of the organization. The current implementation uses long polling which is not very efficient in terms of cloud costs. These API connections should be converted to use subscription to reduce the number of calls we have to make to server.

Here are list of issues and pull requests reagarding that
 ### Talawa Admin
 
 #### Issue : [Feature Request : [Features as Plugins] Implement UI for AddOnStore with Proper Server Calls](https://github.com/PalisadoesFoundation/talawa-admin/issues/356)
 
 #### Pull request: [Plugin Architecture for Admin](https://github.com/PalisadoesFoundation/talawa-admin/pull/355)
 
 Summary : 
- Refractored Store UI 
- Implement Search Functionality for plugins
- Added fallback screen for the plugin store

### Talawa API

#### Issue : 
- [Feature Request: auto populating plugin data during the initial server setup](https://github.com/PalisadoesFoundation/talawa-api/issues/1337)
 
 #### Pull request:
 - [ [GSoC][Feature Request] : Feature Request: auto populating plugin data during the initial server setup](https://github.com/PalisadoesFoundation/talawa-api/pull/1345)
 
 Summary : 
- Add Node.JS funtion in the server that check if currently any default plugin data is present in the current database instance or not.
- If present it would not do anything
- If plugin data is not present it takes the default plugin data from server's file and upload to the database

#### Video Demo: 
- [Talawa API: Demos of Websocket, schema change, auto populating features](https://www.youtube.com/watch?v=MaETaxPGNxk)

#### Chapters:

- 0:00 Auto Populating plugins demo
- 05:38 Discussing websockets code and change schema code
- 10:10 Demo of Websockets, createPlugin, updatePluginStatus
--- 
#### Issue : 
- [Conversion from HTTP TO Websockets for all plugin operations(https://github.com/PalisadoesFoundation/talawa-api/issues/1354)Feature Request: Changing Schema of Plugins

 #### Pull request: 
- [ [GSoC][Feature Request] : Conversion from HTTP TO Websockets for all plugin operations](https://github.com/PalisadoesFoundation/talawa-api/pull/1355)

 *Summary* : 
![image](https://github.com/SiddheshKukade/Google-Summer-of-Code-2023-Work-Product/assets/65951872/14c68aad-0477-4774-8f48-e580ab04aaf7)
![image](https://github.com/SiddheshKukade/Google-Summer-of-Code-2023-Work-Product/assets/65951872/2ae53fe2-c4d4-46c4-8471-e13d3f242941)

- CHanged a Plugin model schema to reduce the complexity in the code.
  -  Before:
      ```js
        const pluginSchema = new Schema({
        pluginName: 
        pluginCreatedBy:
        pluginDesc: 
        pluginInstallStatus: 
        installedOrgs: [],
      });
      ```
  -  After:
      ```js
      const pluginSchema = new Schema({
          pluginName: 
          pluginCreatedBy:
          pluginDesc: 
          uninstalledOrgs: [], /// containing list of orgs who've that plugin feature disabled.
        });
      ```
- Created a websocket server in Apollo GraphQL to allow to subscribe to socket events.
- Wtitten API to update and delete plugin recrods and accordingly notify the server via GraphQL subscriptions.

#### Video Demo: 
- [Talawa API: Demos of Websocket, schema change, auto populating features](https://www.youtube.com/watch?v=MaETaxPGNxk)
- [Utilizing the subscription ](https://youtu.be/B72h2fM5KsA)
---

#### Issue :
 [Convers-ion fromHTTP TO Websockets for all plugin operations(https://github.com/PalisadoesFoundation/talawa-api/issues/1354)
 
 #### Pull request: [ [GSoC][Feature Request] : Conversion from HTTP TO Websockets for all plugin operations](https://github.com/PalisadoesFoundation/talawa-api/pull/1355)

 Summary : 
![image](https://github.com/SiddheshKukade/Google-Summer-of-Code-2023-Work-Product/assets/65951872/14c68aad-0477-4774-8f48-e580ab04aaf7)
![image](https://github.com/SiddheshKukade/Google-Summer-of-Code-2023-Work-Product/assets/65951872/2ae53fe2-c4d4-46c4-8471-e13d3f242941)

- Created a websocket server in Apollo GraphQL to allow to subscribe to socket events.
- Wtitten API to update and delete plugin recrods and accordingly notify the server via GraphQL subscriptions.

#### Video Demo: 
- [Talawa API: Demos of Websocket, schema change, auto populating features](https://www.youtube.com/watch?v=MaETaxPGNxk)
- [Utilizing the subscription ](https://youtu.be/B72h2fM5KsA)
---











 ## 2. The creation of Donations plugin to prove the concept
  Donation is a feature on `talawa` mobile app that enables organization members to donate to current organization throught credit card.The Donation is also implemented as plugin which makes it accessible in the mobile app only if it is installed by the admin of that organization
  

### Talawa

#### Issue : [Feature Request : Enabling Plugins , Donation as a Plugin, Refractor for TalawaPluginProvider Widget](https://github.com/PalisadoesFoundation/talawa/issues/1346)
 
 #### Pull request: [ [GSoC][Feature Request] : Enabling Plugins , Donation as a Plugin, Refractor for TalawaPluginProvider Widget ](https://github.com/PalisadoesFoundation/talawa/pull/1355)
 
 Summary : 
- Implementation of Donation feature as a plugin
- Designed and Added Logic to implement Navbar Features a plugins
- Added `TalawaPluginProviderNav` which is used for wrapping the navbar items to make them plugins
- Fixed how the components were rendering using `TalawaPluginProvider`

### Talawa API

#### Issue : [Feature Request : Performing Donations ( Ability to store donation transaction in Talwa-api )](https://github.com/PalisadoesFoundation/talawa-api/issues/755)
 
 #### Pull request: [ [GSoC]Feature Request : Performing Donations ( Ability to store donation transaction in Talwa-api ) ](https://github.com/PalisadoesFoundation/talawa-api/pull/756)
 
 Summary : 
- Implementation of Donation  API routes for talawa-api
-  Mutations and Queries
    - `getDonations` query to get list of donatinons made for that organization.
    - `getDonationById` query to get details about the speicic donation.
    - `getDonationByOrgsId` query getting the list of donation with thier organization id.
    - `createDonation` mutation to create new Donation.
    - `deleteDonation` mutation to delete the donation record in case if the transaction fails to complete from `flutter_braintree` pacakge or by the user.
    
## Other

#### Technical Documenmtation for plugins 

### Talawa Docs - The documentation for talawa project.


#### Issue : [Feature Request : Adding Plugin Architecture Overview Page](https://github.com/PalisadoesFoundation/talawa-docs/issues/251)
 
#### Pull request: [ [GSOC]Docs : Plugin Architecture Overview Page  ](https://github.com/PalisadoesFoundation/talawa-docs/pull/254)
 
 Documentation Includes : 
 - Overview of What a plugin actually means in talawa repositories
 - A High-level diagram to describe workflow with description
 - Code Explanation


#### Issue : [Docs : Adding Step by Step Plugin Example with Code explanation](https://github.com/PalisadoesFoundation/talawa-docs/issues/255)
 
#### Pull request:
 * [ [GSOC]Docs : Adding Step by Step Plugin Example with Code explanation   ](https://github.com/PalisadoesFoundation/talawa-docs/pull/256)
 * [[GSOC] Docs : Adding Step by Step Plugin Example](https://github.com/PalisadoesFoundation/talawa-docs/pull/258)
 
 
 Documentation Includes : 
 - Technical overview of the steps used to convert the features into pluigns
 - Step-by-step example of actual conversion of a feature to a plugin (ex. Donation feature) 

## Working Demo Video of Plugin Architecture : 
https://user-images.githubusercontent.com/65951872/189489729-ba913de7-8376-438f-a29d-bfcabecaddd2.mp4
# Conclusion 
I have spent my summer implementing a plugin for talawa application. This problem statement encouraged me to deeply study some technical concepts and writing.
I've worked with my mentors [Dominic Mills](https://github.com/DMills27) , [Yash Dubey](https://github.com/yasharth291) & [Peter Harrison](https://github.com/palisadoes) to design and implement the plugin architecture with a Donation feature as a plugin to prove the concept thier support and feedback helped me to very much. I would also like to thank my mentors, org admins and other contributors for helping me to make the project possible. Palisadoes Foundation has a very supportive community that believes in helping each other to grow together.



