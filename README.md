Original App Design Project - README Template
===

# StudyGroupFind

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
The app will be a study tool for students so that they may be able to find study partners and groups for class. Basically a rate my professor but for study groups with the added benefit of being able to contact each other within the app. This app is aimed to fix the problem of students needing to find partners or groups for their class assignment. The age range from this app is 13+.

### App 

- **Category:** Social/ Educational 
- **Mobile:** Used in a School setting 
- **Story:** Found it hard to find study groups, this app makes it easy to find study groups (because it shows you people from your school that are taking the same class as you are people who are in the same major.
- **Market:** Students (specifically those who prefer to study in groups).  
- **Habit:** People who go to school need to study to do well in school, especially during exam time. It is also said that peer learning/teaching is a very effective way of retaining knowledge 
- **Scope:** Students 

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* User can create a new account
* User sets a profile picture 
* User can login
* User can search for other classes/majors/schools/
* User can view study groups you are participating in (Profile) 
* User can create a study group
* User can use a chat system

**Optional Nice-to-have Stories**

* User can add a comment to a study group 
* User can tap a photo to view a more detailed photo screen with comments
* User can see rate a class/course
* User can see notifications when new participants join
* User can make private study groups 
* User can see their profile page with their photos
* User can view other user’s profiles and see their photo feed
* User can like a study group


### 2. Screen Archetypes

* Login Screen
   * User can login
* Registration Screen
   * User can create a new account
* Stream (Profile) 
   * User can view their study groups
   * User can view profile 
   * User can view study groups you are participating in 
* Creation
   * User can create study groups 
   * Set a profile picture 
   * User can use a chat system 
* Search
   * User can search for other classes/majors/school
  

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Profile Screen/Home
* Creation Screen
* Search Screen 

**Flow Navigation** (Screen to Screen)

* Login Screen / Registration screen
=> Profile (home screen)
If no account, registration screen. Home screen will have profile and the different options to pick from
* Registration Screen
=> Home
* Stream Screen (Profile Screen/Home) 
=> Chat Creation Screen 
* Creation Screen
=> Home (after you finish making study group)
* Search Screen
=>  Home

## Wireframes

<img src="https://github.com/yasminsenior02/Studifed/blob/main/20211115_180940.jpg" width=600>


## Schema 
### Models
#### User

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | userId        | String   | unique id for the user (default field) |
   | groupmemberId | Pointer to User to Studygroup| studygroups user is member of |
   | imageId       | File (Pointer to User) | user profile image |
   | school        | String   | school of user |
   | major         | String   | major of user|
   | classification| String   | classification of user |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
   
#### Study Group

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | groupId       | String   | unique id for the group (default field) |
   | groupmemberId | String   | unique id for the user as part of a specific group (default field) |
   | groupname     | String   | name of study group |
   | groupimageId  | File (Pointer to Group) | group profile image |
   | groupsubjcet  | String   | subjcet studied in group |
   | groupclassname| String   | name of class group members are in (optional) |
   | groupteacher  | String   | teacher of class group memebers are part of (optional)|
   | description   | String   | description of study group (optional) |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
   ### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all studygroups where user is member
         ```swift
         let query = PFQuery(className:"StudyGroup")
         query.whereKey("member", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         ```
      - (Create/StudyGroup) Create a new study groups
      - (Delete) Delete existing study groups
   - Create Study Group Screen
      - (Create/StudyGroup) Create a new text
   - Profile Screen
      - (Read/GET) Query logged in userId
      - (Update/PUT) Update user profile image
 - Group Detail Screen
      - (Read/GET) Query logged in group
      - (Update/PUT) Update group profile image 
      - (Create/StudyGroup) Create/Add new member
      - (Delete) Delete existing study groups

#### [OPTIONAL:] Existing API Endpoints
##### StudyGroupFind

   HTTP Verb | Endpoint | Description
   ----------|----------|------------
    `GET`    | /studygroups | gets all groups
    `GET`    | /studygropus/byId/:id | gets specific studygroup by :id
    `GET`    | /school | get all school
    `GET`    | /school/byId/:id | get specific school by :id
    `GET`    | /major   | get all major
    `GET`    | /major/?name=name | return specific major by name
    `GET`    | /class | gets all classes
    `GET`    | /class/byId/:id | gets specific class by :id
    `GET`    | /teacher | get all teacher
    `GET`    | /teacher/?name=name | return specific teacher by name
    `GET`    | /studygroup/subject/:name | gets a studygroup's subject with a given name
    `GET`    | /studygroup/class/:name | gets a studygroup's class with a given name
    `GET`    | /studygroup/teacher/:name | gets a studygroup's teacher with a given name
