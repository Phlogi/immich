# Concept Proposal for more flexible Permissions, Access Controls and Shared Metadata
## Ressources and "input" with short summary
Note: The summaries are generated with an LLM. This is intended as a warm-up and to consolidate all previous discussions and thoughts on the topic. Please note that not all ideas and wishes are addressed with the concept later. 

<details>

<summary>Click to open links with summaries.</summary>

[Discord Discussion: Family/Group space or Shared Account](https://discord.com/channels/979116623879368755/1026327300284887111/threads/1145363766825988146 )
	The implementation of Google Photos is preferred for its elegant and sensible approach compared to using special user classes. It allows photos to back up to personal accounts, ensuring privacy. Users can share only selected photos in a shared album, and the original uploaders are identified for better tracking. Participants can save only the photos they like to their timeline, preventing clutter from unwanted images. A "save to my timeline" feature is suggested, allowing users to associate preferred photos with their account while retaining the original photographer's note.
	
[Global/Local People: Improve facial recognition and open the door to sharing people with a partner](https://discord.com/channels/979116623879368755/1026327300284887111/threads/1212062614306299944)
	The proposal suggests implementing a hierarchy in facial recognition for the immich app. Instead of each user having independent people, it would have global people connected to local persons for each user, improving facial recognition precision, sharing manual clustering work, and allowing shared people data across partners. Concerns include potential information leaks between users, but the proposed system aims to mitigate this with admin settings and careful clustering. This change would primarily affect the server side and facilitate partner sharing of people data.
	
https://github.com/immich-app/immich/issues/12614 Title: [META] Better sharing in Immich
- **Current Limitations of Sharing**: Users find the existing photo and video sharing features in Immich to be confusing and limited, prompting a need for a comprehensive redesign.
- **Feature Freeze**: The development team has decided to implement a feature freeze on sharing-related changes to reassess and plan for future improvements.
- **User Suggestions**: Multiple users have suggested enhancements, including the ability to share albums collectively rather than individually, which is currently tedious.
- **Facial Recognition Limitations**: Users expressed frustration that facial recognition features do not extend to partner-shared photos, limiting search capabilities.
- **Collaborative Library Management**: There is a strong desire among users for features that allow multiple individuals to manage and tag shared libraries collaboratively, enhancing the overall user experience.
- **Nested Albums and Group Sharing**: Requests for nested albums and the ability to share access with groups (e.g., family, friends) highlight the need for more organized sharing options.
- **External Library Ownership**: Users want the ability to have external libraries owned by multiple accounts to streamline the process of managing shared content without repetitive thumbnail generation.
- **Granular Permissions**: There is a call for more granular permission settings, enabling users to control who can view, tag, or modify shared content.

https://github.com/immich-app/immich/discussions/7038 Title: The definition of partner sharing · immich-app/immich · Discussion #7038
The GitHub discussion on partner sharing within the Immich app highlights several key insights and user needs:
- **One-Way vs. Two-Way Sharing**: Users express concerns about how ownership and access to shared person objects are managed, particularly in one-way versus two-way partner sharing scenarios.
- **Global Face Recognition**: There is a strong desire for a global state for people and face matching, allowing users to identify individuals across different accounts without duplication.
- **Permissions and Editing**: Users are frustrated by limitations in editing capabilities across shared accounts, suggesting a need for clearer permissions and consent processes for proposed changes.
- **Read-Only Access**: There is a demand for read-only access options for shared accounts, particularly for users with difficulties navigating technology, to prevent accidental deletions or changes.
- **Shared Library Functionality**: Users wish for the ability to share entire libraries, including associated persons and albums, while maintaining control over personal libraries.
- **Metadata Ownership**: The discussion includes considerations about ownership of machine-generated metadata, suggesting a need for flexibility in how shared information is managed.
- **Hierarchical Tagging System**: A proposal for a tagging system that allows for more granular control over shared content and associations between users is put forward.
- **Family Archivist Role**: The potential market for family archivists is recognized, emphasizing the importance of features that cater to users managing shared family memories.
- **Feature Development Feedback**: Users are eager for updates on the development of partner sharing features, particularly regarding face recognition capabilities and ease of use for shared content.

https://github.com/immich-app/immich/discussions/1587 Title: [Feature]: "Add to Library" · immich-app/immich · Discussion #1587
- The discussion revolves around the proposed feature "Add to Library" for the Immich app, aimed at enhancing user experience with shared albums.
- Users express a strong desire for functionality similar to Google Photos, highlighting its usefulness for families who share photos across different accounts.
- The feature would allow users to add photos from shared albums directly to their personal albums without the need to download and re-upload, streamlining the process.
- Users emphasize the importance of being able to view shared photos in their personal timeline, which would improve accessibility to family photos.
- The discussion includes concerns about ownership and management of shared photos, particularly regarding deletion and editing rights.
- Users propose the need for facial recognition capabilities for shared albums to enhance organization and identification of individuals in photos.
- A preference for a straightforward implementation that simply copies assets into a user's library is voiced, prioritizing simplicity over complex features.
- One user shares a personal story highlighting the emotional significance of being able to curate shared photos for memorial purposes.
- Overall, there is a consensus on the potential benefits of the "Add to Library" feature, with users eager for its development and implementation.

</details>

## Main Pain Point
As a user of a **shared-to-me** album i cannot put those shared assets into other albums that i own or that are shared to me. Furthermore I cannot rate or favorite those assets nor display any of them in my timeline. 
# Initial situation
This section describes all the current solution as of January 2025. It summarizes all aspects relevant for the concept and solution designs. 
## Assets
There are two types of assets in immich Photos and Videos. Assets are owned by exactly one user and can be shared through albums.
## Album
A user of a shared album can have one of three roles:
- Owner (only exactly one)
- Editor
- Disallow edits

Partner share allows impersonation of another user with some default limits applied, e.g. cannot manage assets being part of albums.
#### Public Links on albums
Relevant permission options are allow *public user* to:
- download,
- upload
assets.
## Requirements
These requirements set the scope for this concept. 
### Use Cases
#### Sharing Family Photos with a Trusted Partner
As an Immich logged-in user, I want to share family photos with a **Very Close Person** (e.g., my partner) so that both of us can add new photos, edit existing ones, and tag people within the Immich app. My partner should also be able to see these shared photos in their timeline by default, allowing seamless viewing and management of our shared memories.
#### Finding All Assets of My Children
As an Immich logged-in user, I want to find all photos and videos of my children by using tags or face recognition within the Immich app. I should be able to use the names I chose myself while also benefiting from tags added by a **Known User in Immich** who has shared these assets with me.
#### Advanced Sharing with a Party Organizer or Best Man at a Wedding
As an Immich logged-in user organizing a wedding, I want to share a photo album with a **Public User with Temporary Rights** (e.g., the best man) so they can upload and view photos from the event within the Immich app. This user will help manage the collection of all wedding photos, ensuring they are uploaded to the album for everyone to see later.
#### Event Photo Sharing with Many Guests
As an Immich logged-in user, I want to share photos from a party or event with many guests who are **Untrusted Public Users** . These guests should have the ability to view the shared album through a public link in the Immich app, but they should not be able to edit or delete any of the content. This allows all guests to view photos from the event without compromising my control over the photos.
## Solution Concepts
## Persona
We distinguish between four types. These are described from the assets owner perspective:

**Very Close Person**: A trusted individual, like a life partner. You can collaborate on almost everything without hesitation, as there is complete trust.

**Known User in Immich**: Someone you know but don't fully trust with everything. You collaborate but limit access to sensitive features like metadata changes. This user has an account on immich.

**Public User with Temporary Rights**: A user with time-limited collaboration rights. They can perform specific actions like adding or removing photos, or other actions for a set period. This user has no account on immich. 

**Untrusted Public User**: A user you don't trust much and have no reason to collaborate with. They have minimal read-only access to your content and again no immich account. 
## Base Permission model 
We  suggest introducing RBAC model into immich for following reasons:
- well known standard way of handling permissions
- scales well with future needs
- easy mass role assignments on multiple users
- granular access control

We'd however would keep the number of roles simple from the beginning on not exposing technical roles towards the users. Instead we further abstract the internal roles to the users along a level of trust defined by the persona.
### **Persona Summary with Trust Levels**

| **Persona**                           | **Trust Level** | **Mapped Internal Role** | **Permissions (Summarized)**                                                                                                            |
| ------------------------------------- | --------------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| **Instance Admin**                    | 0               | **Instance Admin**       | No access to metadata of assets, user management, changes on internal roles, role assignments, etc.                                     |
| **Very Close Person**                 | 1               | **Collaborator**         | Full access to all shared assets (view, edit, upload, collaborate) but no system-level access (no role/user management).                |
| **Known User in Immich**              | 2               | **Curator**              | Limited access to selected shared assets (view, edit, upload, collaborate without destructive actions).                                 |
| **Public User with Temporary Rights** | 3               | **Contributor**          | Limited to adding content (upload images) and collaborating within a set time period, without access to sensitive metadata or deletion. |
| **Untrusted Public User**             | 4               | **Viewer**               | Very limited access, primarily read-only (view images/albums). No ability to modify or manage content.                                  |

We give sane default permissions in detail along the level of trust and the introduced internal roles. This abstraction simplifies the selection of access for the user, as the user knows the relationship to the other person. 
If more flexible permissions are needed, we'd be able to expose the internal role to the user and select/de-select specific permissions for their use case. Not recommended to implement from the beginning. Just show the actual and relevant permissions in a collapsed section.

### Persona Counts
To get a better understanding, here are typical numbers of persona per immich user. 

| **Persona**                           | **Count per user** | **Reasoning**                                                                                                                                                                      |
| ------------------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Instance Admin**                    | 1                  | Typically, there's only one main admin responsible for managing the entire instance, ensuring proper user permissions and overall system governance.                               |
| **Very Close Person**                 | 1-3                | Represents a highly trusted individual, such as a life partner or family member, where complete collaboration is needed without any reservations.                                  |
| **Known User in Immich**              | 5-10               | Represents a small number of users who are familiar and somewhat trusted. They require access to collaborate but with some limitations to maintain control over sensitive aspects. |
| **Public User with Temporary Rights** | 5-10               | Usually represents users who are temporarily given certain rights, often for specific events or projects, suggesting there are typically a couple of such interactions.            |
| **Untrusted Public User**             | 1 to 1'000s        | Public users who are not trusted could be many, especially in scenarios involving large events or public sharing, hence the need for a more flexible count.                        |
## Metadata
## Metadata of assets
Shows an overview of all metadata associated with an asset. The last column is introduced here for categorizing the metadata into different types with a base scope category. 
table:

| **Name**             | **Description**                                                       | Editable | Base Scope |
| -------------------- | --------------------------------------------------------------------- | -------- | ---------- |
| **File Information** | File name, extension, size, and type (image/video).                   | n        | A          |
| **Media Type**       | Differentiates between image, video, or live photo.                   | n        | A          |
| **Camera Details**   | Make, model, lens type, and settings (e.g., aperture, shutter speed). | n        | A          |
| **GPS Coordinates**  | Location data embedded in the file (latitude, longitude).             | y        | A          |
| **Date and Time**    | Original capture date and time of the media file.                     | y        | E          |
| **Description**      | Custom text or notes about the media.                                 | y        | E          |
| **Star Rating**      | One to five star rating of asset.                                     | y        | U          |
| **Tags**             | Non hierarchical labels for categorization.                           | y        | E          |
| **Albums**           | Association with specific albums in Immich.                           | y        | S          |
| **People**           | Detected or tagged individuals in the media.                          | y        | U          |
| **Objects**          | Recognized objects in the media via machine learning.                 | n        | A          |
| **Favorites**        | Marked as a favorite by the user.                                     | y        | U          |
| **Archived Status**  | Whether the media is archived.                                        | y        | U          |

Legend for **Base Scope**:
- A: Close to immutable metadata of an asset with the exception of the date and time. 
- E: Metadata that is shared and allows for collaborative edits by multiple users.
- S: Shared metadata is intended for use by multiple users beyond the asset's owner and remains the same for everyone. It is not personalized or user-specific but is **S**hared uniformly across all users.
- U: Highly user-specific and personal metadata, intended to be controlled solely by the asset's owner and restricted to an individual user's scope, ensuring it is not viewed nor modified by others.

To explain how this table is read, here are two examples:

**Camera Details Interpretation:** Camera Details are fixed information about the camera used to capture an image or video, including make, model, lens type, and settings like aperture, shutter speed, and ISO. These details are considered immutable (non-editable) and are consistent for all users, making the base scope "Asset-Level" (A). Users cannot change these details within the application as they are a permanent part of the file's metadata. The only exception would be the owner of the asset or the instance admin to refresh or correct the information - but for all users.

**Description Interpretation:** Description metadata allows users to annotate a media file by adding custom text or notes. For example, User A can add a description like "Family Vacation 2025" to a photo, and if this photo is shared with User B, they will see the same description. The base scope is "Editable by Users and Shared" (E), meaning users with the necessary permissions can edit this field to add or update descriptions, making it a collaborative piece of metadata.
### Motivation for separation of metadata types
Some metadata, such as face grouping and naming, should remain private to the owner of the assets, even when shared through an album.

**Example and Reasoning in the face detection context:**  
User A has named a person in their collection "Dad" and assigned this name within the application (e.g., Immich). When User A shares an album containing this person's photos with User B, who is their partner, the person might be known to User B as "Claude." Since this difference is common, it’s important that personalized metadata, like names, is not shared between users.

For User B, the shared person's face will be grouped with other similar faces in their own collection. To enable this, a new face grouping process is triggered specifically for User B. This ensures that each user's face groups remain unique to their preferences and associations.

Note that this face grouping process is distinct from face recognition. Face recognition only runs once per asset, whereas face grouping adapts to the individual user's library and metadata. It's necessary to run it whenever a change happens on shared assets. 

**Sidenote:** The actual clustering of images can differ between users. A user with access to more assets containing the same person's face will generally see better grouping results.

**Discarded alternative solutions:**
For close users with high trust level, share the already named faces. Why discarded: See the above Dad example for one reason, another one is the complexity introduced when a user renames a person. 
## Permissions Tables
### Metadata Types
This table is a proposal for default and sane permissions for each Metadata type:

| **Name**             | **Editable** | **Base Scope** | **Instance Admin** | **Collaborator** | **Curator** | **Contributor** | **Viewer** |
| -------------------- | ------------ | -------------- | ------------------ | ---------------- | ----------- | --------------- | ---------- |
| **File Information** | n            | A              | X                  | R                | R           | R               | R          |
| **Media Type**       | n            | A              | X                  | R                | R           | R               | R          |
| **Camera Details**   | n            | A              | X                  | R                | R           | R               | R          |
| **GPS Coordinates**  | y            | A              | X                  | R/W              | R/W         | R               | R          |
| **Date and Time**    | y            | E              | X                  | R/W              | R/W         | R               | R          |
| **Description**      | y            | E              | X                  | R/W              | R           | R/W             | R          |
| **Star Rating**      | y            | U              | X                  | R/W              | R/W         | R/W             | X          |
| **Tags**             | y            | E              | X                  | R/W              | R/W         | R/W             | R          |
| **Albums**           | y            | S              | X                  | R/W              | R/W         | R/W             | X          |
| **People**           | y            | U              | X                  | R/W              | R/W         | X               | X          |
| **Objects**          | n            | A              | X                  | R                | R           | R               | R          |
| **Favorites**        | y            | U              | X                  | R/W              | R/W         | X               | X          |
| **Archived Status**  | y            | U              | X                  | R/W              | R           | X               | X          |

### Operations 
Proposed list of operations and their permissions based on the abstracted roles:

| **Permission**             | **Collaborator** | **Curator** | **Contributor** | **Viewer** |
| -------------------------- | ---------------- | ----------- | --------------- | ---------- |
| **Trash an Asset**         | y                | y           | n               | n          |
| **Restore from Trash**     | y                | n           | n               | n          |
| **Download Assets**        | y                | y           | y               | y/n        |
| **Upload Assets**          | y                | y           | y               | n          |
| **Replace with New Image** | y                | n           | n               | n          |
| **Refresh Metadata**       | y                | y           | n               | y          |
| **Refresh Faces**          | y                | y           | n               | y          |
| **Duplicate Handling**     | y                | y           | n               | n          |

Note: The Instance Admin does not have any access to those permissions, while the owner of the asset has all of them. They are not listed explicitly. 

The list of operations is not complete, there are more actions in immich that are affected by permissions handling. However it shows how  default permissions can be assigned to them and how to use the proposed solution conceptually. 
### Measures to Avoid Accidental Mass Deletion and Metadata Messing by Shared-to Users

**Assets Moving to Trash of the Owner:**
- **Measure:** When a shared user attempts to delete an asset, the asset moves to the trash bin of the original owner, not the shared user.
- **Mitigation:** This ensures that accidental deletions can be easily reversed by the owner. The owner has a defined period to restore the assets from the trash before permanent deletion.

**Confirmation Dialogs for Critical Actions:**
- **Measure:** Implement confirmation dialogs or multi-step verification for actions such as bulk deletions or metadata changes.
- **Mitigation:** Users must explicitly confirm their actions, reducing the likelihood of accidental modifications or deletions.

