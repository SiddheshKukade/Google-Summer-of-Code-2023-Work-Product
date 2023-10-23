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
 ### Talawa Admin & Talawa Web
 
 #### Issue : 
 - [Feature Request : Adding Plugin Logic to the Talawa Mobile Web App](https://github.com/PalisadoesFoundation/talawa-admin/issues/975)
 
 #### Pull request: 
 - [Adding Plugin Logic to the Talawa Mobile Web App](https://github.com/PalisadoesFoundation/talawa-admin/pull/976)
 
 Summary: 
- As the plugin would be installed by default the admins should be prompted that they would be using everything or they can visit the store to disable no required features. To understand the context please refer to this video: https://youtu.be/9rBc9sdpLjM?t=513


### Video Demo: 
- [Siddhesh Bhupendra Kukade - Talawa Plugins Explained](https://www.youtube.com/watch?v=9rBc9sdpLjM)
- [Updated Plugin Store talawa admin | GSoC Work Report July | Siddhesh Kukade](https://www.youtube.com/watch?v=klDNSYXnCno)
- [Plugin Store Dialog demo | GSoC Work Report July](https://www.youtube.com/watch?v=5GOGf-C3WEo)

---
 
 #### Issues:
 - [Feature Request: Refactoring old API queries to match them with updated queries for Plugin store.](https://github.com/PalisadoesFoundation/talawa-admin/issues/952)
 - [Adding a dialog to go to plugin store after an organization is created by the admin](https://github.com/PalisadoesFoundation/talawa-admin/issues/975)
 
 #### Pull request: 
 - [Adding a dialog to go to plugin store after an organization is created by the admin](https://github.com/PalisadoesFoundation/talawa-admin/pull/951)
 
 Summary : 
- Setting Up socket connections
- Adding the toggling logic
- Finding a way to store and handle that data.

### Video Demo: 
- [Talawa Plugin working demo on web version | GSoC 2023 Sept Work Report | Siddhesh Kukade Palisadoes](https://www.youtube.com/watch?v=iUd5zbpEAdI)
- [ Plugin Demo on Web app with Multiple features removal and additions | GSoC Work Report | Palisadoes](https://www.youtube.com/watch?v=zpV-P7El_qk)

---

### Talawa API

#### Issue: 
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
- [ [GSoC][Feature Request] : [Conversion from HTTP TO Websockets for all plugin operations](https://github.com/PalisadoesFoundation/talawa-api/pull/1355)
- [ [GSoC][Fix] : Removed Windows Specific Pacakges](https://github.com/PalisadoesFoundation/talawa-api/pull/1355)

 *Summary* : 
![image](https://github.com/SiddheshKukade/Google-Summer-of-Code-2023-Work-Product/assets/65951872/14c68aad-0477-4774-8f48-e580ab04aaf7)
![image](https://github.com/SiddheshKukade/Google-Summer-of-Code-2023-Work-Product/assets/65951872/2ae53fe2-c4d4-46c4-8471-e13d3f242941)

- Changed a Plugin model schema to reduce the complexity in the code.
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
- Fixed some windows related run-time errors.

#### Video Demo: 
- [Talawa API: Demos of Websocket, schema change, auto populating features](https://www.youtube.com/watch?v=MaETaxPGNxk)
- [Utilizing the subscription ](https://youtu.be/B72h2fM5KsA)
---





 ## 2. Development of Advertisement Feature
 Adding Ads would allow 2 types of benefits:
1. Earning revenue for the org.
2. Companies having products related to such orgs they can directly target those customers.
  

### Talawa Web and Talawa Admin

#### Issue : 

- [Bug Report: Missing REACT_APP_BACKEND_WEBSOCKET_URL=ws://localhost:4000/graphql](https://github.com/PalisadoesFoundation/talawa-admin/issue/993)
- [Feature Request: Adding advertisement management screen for the admin](https://github.com/PalisadoesFoundation/talawa-admin/issues/996)

 #### Pull request:
- [Feature request: Adding advertisement screen](https://github.com/PalisadoesFoundation/talawa-admin/pull/994)
 
 Summary : 
- Developed User interface for advetisement store only loading ads matching with the current logged in org of user with features like deleting seeing the ongoing ad campgins,etc.
- Developed a feature in Talawa User Web app to showcase those advertisement as promoted posts

#### Video Demo:
- [Advertisement in Talawa Admin and Talawa Mobile | Palisadoes Foundation | Google Summer of Code 23](https://www.youtube.com/watch?v=66q8GHktN8A)

---
### Talawa-api

#### Issue : 
- [Feature Request: Adding Advertisements](https://github.com/PalisadoesFoundation/talawa-api/issues/1394)
 
 #### Pull request:
 - [ Adding Advertisements](https://github.com/PalisadoesFoundation/talawa-api/pull/1395)
 
 Summary : 
- Added Adverstiment document Schema:

2. Developed GraphQL endpoint:
- createAdverstisement()
  - The created doc with the given provided schema data values and stores in the database.
- deleteAdvertisement()
  - To be used if user accidentaly created that document and he wants to delete that
- getAdvertisement()
  - Used by the mobile app to fetch all the ads to show filtered by the dates
---

#### Issue : 
- [Feature Request: deleting advertisements](https://github.com/PalisadoesFoundation/talawa-api/issues/1416)
 
 #### Pull request:
 - [ Delete ads mutation is talawa API](https://github.com/PalisadoesFoundation/talawa-api/pull/1415)

Summary:
- Added GraphQL endpoint in server to delete advertisement records.

--- 
 
# Conclusion 
Throughout my Google Summer of Code 2023 journey. I have worked on different features including both front-end and back-end web devlopment. I also worked with new technologies like WebsSocket protocol.
I've worked with my mentors  [Tasneem Koushar](https://github.com/tasneemkoushar), [Dominic Mills](https://github.com/DMills27) , & [Peter Harrison](https://github.com/palisadoes) to design and implement these features like advetisement, adding default plugin data in database. We had bi-weekly meeting to dicuss and provide feedback on current progress of work that helped me a lot to quickly figure out my mistakes. I would also like to thank my mentors, org admins and other contributors for helping me to make the project possible. Palisadoes Foundation has a very supportive community that believes in helping each other to grow together.

Thank you [Google](https://github.com/google) for Organizing such a great opportunity. 💛 🌞



