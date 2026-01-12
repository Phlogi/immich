# Concept Proposal for more flexible Permissions, Access Controls and Shared Metadata

## Ressources and "input" with short summary

Note: The summaries are generated with an LLM. This is intended as a warm-up and to consolidate all previous discussions and thoughts on the topic. Please note that not all ideas and wishes are addressed with the concept later.
Date cutoff: 2025-01-09

<details>

<summary>Click to open links with summaries.</summary>

[Github: Better sharing in Immich (feature freeze)](https://github.com/immich-app/immich/issues/12614)

- Immich is currently undergoing a feature freeze on sharing-related changes to internally plan a more robust sharing system.
- The desired 'better solution' for sharing in Immich should encompass albums, stacks, shared links, partner sharing, library sharing, and asset data like tags and people.
- Users desire the ability to share albums collectively, for instance, by selecting multiple albums at once when sharing with a specific user.
- Integration of smart search within shared albums, especially for shared links, is a requested feature to enable users without Immich accounts to search within shared content.
- There's a clear distinction desired between 'sharing' (read-only viewing) and 'collaboration' (maintaining a library with full access to all data).
- Key feature requests include nested albums, user groups for easier access management, and the ability to create albums based on tags.
- Sharing of asset data, including tags and recognized people/faces, is a highly sought-after feature across different sharing mechanisms like partner sharing and shared albums.
- Users are looking for more granular control over sharing, such as sharing only a subset of photos or creating specific shared spaces for partners or family.
- The current sharing model is often seen as counterintuitive, leading to errors and a lack of clarity on what actions are possible with shared assets.
- There's a strong desire for shared facial recognition data, allowing users to search for people across all shared photos, which is currently a significant limitation and a reason for using single shared accounts.

[Discord Discussion: Family/Group space or Shared Account](https://discord.com/channels/979116623879368755/1026327300284887111/threads/1145363766825988146)
The implementation of Google Photos is preferred for its elegant and sensible approach compared to using special user classes. It allows photos to back up to personal accounts, ensuring privacy. Users can share only selected photos in a shared album, and the original uploaders are identified for better tracking. Participants can save only the photos they like to their timeline, preventing clutter from unwanted images. A "save to my timeline" feature is suggested, allowing users to associate preferred photos with their account while retaining the original photographer's note.

[Global/Local People: Improve facial recognition and open the door to sharing people with a partner](https://discord.com/channels/979116623879368755/1026327300284887111/threads/1212062614306299944)
The proposal suggests implementing a hierarchy in facial recognition for the immich app. Instead of each user having independent people, it would have global people connected to local persons for each user, improving facial recognition precision, sharing manual clustering work, and allowing shared people data across partners. Concerns include potential information leaks between users, but the proposed system aims to mitigate this with admin settings and careful clustering. This change would primarily affect the server side and facilitate partner sharing of people data.

[https://github.com/immich-app/immich/issues/12614](https://github.com/immich-app/immich/issues/12614) Title: [META] Better sharing in Immich

- **Current Limitations of Sharing**: Users find the existing photo and video sharing features in Immich to be confusing and limited, prompting a need for a comprehensive redesign.
- **Feature Freeze**: The development team has decided to implement a feature freeze on sharing-related changes to reassess and plan for future improvements.
- **User Suggestions**: Multiple users have suggested enhancements, including the ability to share albums collectively rather than individually, which is currently tedious.
- **Facial Recognition Limitations**: Users expressed frustration that facial recognition features do not extend to partner-shared photos, limiting search capabilities.
- **Collaborative Library Management**: There is a strong desire among users for features that allow multiple individuals to manage and tag shared libraries collaboratively, enhancing the overall user experience.
- **Nested Albums and Group Sharing**: Requests for nested albums and the ability to share access with groups (e.g., family, friends) highlight the need for more organized sharing options.
- **External Library Ownership**: Users want the ability to have external libraries owned by multiple accounts to streamline the process of managing shared content without repetitive thumbnail generation.
- **Granular Permissions**: There is a call for more granular permission settings, enabling users to control who can view, tag, or modify shared content.

[https://github.com/immich-app/immich/discussions/7038](https://github.com/immich-app/immich/discussions/7038) Title: The definition of partner sharing · immich-app/immich · Discussion #7038
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

[https://github.com/immich-app/immich/discussions/1587](https://github.com/immich-app/immich/discussions/1587) Title: [Feature]: "Add to Library" · immich-app/immich · Discussion #1587

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

## Pain points from user perspective

- **Roles and permissions don’t match real-world collaboration.**
  Users need clearly differentiated roles (e.g., _contributor can upload but can’t delete_, _editor can manage and share_) but the current permission model is too limited and makes team/family workflows brittle.

- **Sharing feels confusing and unpredictable.**
  Users often can’t tell what they’re allowed to do on shared vs owned assets. Actions fail without clear guidance, so sharing becomes trial-and-error instead of obvious and reliable.

- **Sharing at scale is painfully manual.**
  Sharing many albums (especially via partner sharing) requires repetitive, tedious selection. There’s no efficient “share all” or comparable bulk flow for large libraries.

- **Metadata sharing is unclear and contentious.**
  Some users expect “if you can see the photo, you can see its derived metadata,” while others require privacy controls (e.g., share without metadata, selectively share people names). Current behavior doesn’t make the rules or tradeoffs explicit.

- **Shared assets behave like second-class items in the product.**
  As a user of an album shared to me, I can’t meaningfully _use_ those assets: I can’t add them to other albums (owned or shared), can’t rate/favorite them, and they don’t appear in my timeline—making shared content hard to organize, rediscover, and integrate into my experience.

## Initial situation

This section describes all the current solutions as of January 2025. It summarizes all aspects relevant for the concept and solution designs.

### Assets

There are two types of assets in Immich: Photos and Videos. Assets are owned by exactly one user and can be shared through albums.

### Album

A user of a shared album can have one of three roles:

- Owner (only exactly one)
- Editor
- Disallow edits

Partner share allows impersonation of another user with some default limits applied, e.g. cannot manage assets being part of albums.

#### Public Links on albums

Relevant permission options allow the _public user_ to:

- download
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

As an Immich logged-in user organizing a wedding, I want to share a photo album with a **Public User with Temporary Rights** (e.g., the best man) so they can upload and view photos from the event through a shared link in a mobile browser (mobile web). This user will help manage the collection of all wedding photos, ensuring they are uploaded to the album for everyone to see later.

#### Event Photo Sharing with Many Guests

As an Immich logged-in user, I want to share photos from a party or event with many guests who are **Untrusted Public Users**. These guests should have the ability to view the shared album through a public link in a mobile browser (mobile web), but they should not be able to edit or delete any of the content. This allows all guests to view photos from the event without compromising my control over the photos.

#### Project Album Collaboration with Subcontractors or Employees

As an Immich logged-in user managing project photos, I want to share a project album with other Immich users who can upload and help curate content, but who must not be able to remove any photos from the album or delete any assets. This supports team workflows while avoiding accidental or unauthorized removal actions.

## Solution Concepts

## Persona

We distinguish between four types. These are described from the asset owner perspective:

**Very Close Person**: A trusted individual, like a life partner. You can collaborate on almost everything without hesitation, as there is complete trust.

**Known User in Immich**: Someone you know but don't fully trust with everything. You collaborate but limit access to sensitive features like broad content removal and irreversible operations. This user has an Immich account.

**Public User with Temporary Rights**: A user with time-limited collaboration rights. They can upload content for a set period and participate in a limited collaboration experience through a shared link. This user has no Immich account.

**Untrusted Public User**: A user you don't trust much and have no reason to collaborate with. They have minimal read-only access to your content through a shared link and again no Immich account.

## Base Permission model

We suggest introducing an RBAC model into Immich for following reasons:

- well known standard way of handling permissions
- scales well with future needs
- easy mass role assignments on multiple users
- granular access control

We keep the number of roles simple in the beginning and do not expose technical roles towards the users. Instead we abstract the internal roles for users along a level of trust defined by the persona. The persona-to-role mapping is a default recommendation and can be adjusted per share.

The internal roles are used for:

- authenticated users (Immich accounts) collaborating inside the system
- unauthenticated users (public links) collaborating with limited rights and optional time restrictions

### Persona Summary with Trust Levels

| **Persona**                           | **Trust Level** | **Default Mapped Internal Role** | **Permissions (Summarized)**                                                                             |
| ------------------------------------- | --------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Instance Admin**                    | 0               | **Instance Admin**               | System operations only. No access to user asset content or metadata.                                     |
| **Very Close Person**                 | 1               | **Collaborator**                 | Full collaboration on shared objects (including editing and removal actions) but no system-level access. |
| **Known User in Immich**              | 2               | **Curator**                      | Collaborative editing and organization without broad content removal actions by default.                 |
| **Public User with Temporary Rights** | 3               | **Contributor**                  | Add-only collaboration (upload/add) with optional time limits. No removal actions.                       |
| **Untrusted Public User**             | 4               | **Viewer**                       | Read-only access (view albums/assets) through a link. No ability to modify or manage content.            |

If more flexible permissions are needed, the internal role can be exposed and relevant permissions can be toggled in a collapsed section.

### Permission Scopes

To reduce ambiguity and make permissions enforceable, we distinguish scopes:

- **Album-scoped permissions**: upload to album, remove assets from album, edit album metadata, manage membership/roles on the album, manage share settings on the album
- **Asset-scoped permissions**: move asset to trash, restore, permanently delete, replace image, refresh metadata/faces, edit shared asset metadata fields
- **Per-user overlay permissions**: personal metadata that can be applied by each authenticated user independently on any visible asset (e.g., favorites, star rating, person naming, “save to timeline”)

Some UI actions combine scopes. In those cases the server must enforce the strictest required permission and the UI should disable or hide actions when the user lacks permission.

### Ownership and Upload Model (short)

Uploads into shared albums should not create "one-sided" access. The model is therefore:

- An upload always creates a persistent asset identity.
- The uploader must retain access to what they uploaded (asset ownership).
- The album owner must retain stable access and management rights for the shared collection (collection management rights via album role).
- Other participants only get access via album or library permissions.
  This is described in more detail below.

### Objects and Effective Permissions (short)

RBAC is attached to objects and composed into effective permissions:

- Album role grants a baseline of actions (view/upload/curate/remove/manage).
- Asset ownership grants owner-level operations.
- Per-user overlays are always allowed for authenticated viewers on visible assets.
- Public links grant a restricted capability set to unauthenticated users, independent of RBAC roles.
  Effective permissions are computed server-side; UI uses them to enable/disable actions.

### User-Specific Metadata Overlay (short)

Certain metadata is personal and should not leak between users:

- Favorites, star ratings, person naming, and "save to timeline" are per-user overlays.
- Any authenticated user who can view an asset can apply these overlays to that asset for their own account.
- Overlays never modify the underlying shared asset content and never affect what other users see, unless a separate explicit sharing mechanism is introduced.

### Timeline Visibility for Shared Albums

Each authenticated user can control whether assets from a shared album appear in their personal timeline:

- **Per-album preference**: When a user is added to a shared album or accepts an album share, they can choose whether to "Show in Timeline" or "Hide from Timeline" (default can be set based on the album role or share context).
- **Modifiable preference**: Users can change this preference at any time for any album shared with them.
- **No impact on album visibility**: This setting only affects the user's personal timeline view; it does not affect their ability to browse the album directly or search for assets within the album.
- **Use case alignment**: Allows users to integrate close-partner shared content into their timeline while keeping project/event albums separate, addressing the "second-class citizen" pain point for shared assets.

### Objects and Permission Attachment Points

Permissions are attached to objects and evaluated into effective access:

- **Album**: defines who can view, upload, curate, remove-from-album, manage album metadata, manage share settings, manage members/roles.
- **Asset**: has ownership (see below) and supports shared metadata edits depending on effective permissions.
- **Public Link**: a capability wrapper around an album that grants a restricted set of actions to unauthenticated users.
- **Library/External Library**: not required for the first iteration, but compatible with the same RBAC model as an additional attachment point.

Effective permissions are derived by combining:

- album share role (if asset is accessed via an album)
- asset ownership
- per-user overlay rules (authenticated only)
- public-link capability settings (unauthenticated only)

### Asset Ownership and Upload Model

To support collaborative uploads without losing access for either party, we distinguish between **asset ownership** and **collection management rights**:

#### Ownership Model (Authenticated Users)

This section describes ownership for authenticated users with Immich accounts. Public link uploads follow a different model (see Public Links section).

- **Asset Owner**: The authenticated user who uploads an asset owns it exclusively and retains it in their personal library.
- **Album Owner**: Has collection management rights over all assets in their album via the album role, but does not co-own uploaded assets.

#### Access Retention

- **Uploader access**: The uploader retains permanent access to their uploaded asset in their own library, independent of album membership.
- **Album-based access**: The album owner and other participants access the asset only while it remains in the album and while they have album permissions.

#### Operational Implications

- The asset appears in the uploader's personal library (always).
- The asset appears in the album for all participants with appropriate album roles (album-scoped).
- If the uploader is removed from the album or the asset is removed from the album, the uploader still owns and can access their asset in their library.
- The album owner can manage the asset's presence in the album (remove from album, reorder, etc.) based on their album role permissions, but cannot delete the uploader's asset from the uploader's library.
- Asset-level operations (move to trash, permanently delete, replace image) require asset ownership. Album role permissions alone do not grant these rights on assets uploaded by others.

#### Exception for Collaborator Role

Users with the **Collaborator** role on an album may be granted extended asset-level permissions on assets within that album context (e.g., move to trash) as defined in the Operations table. This is a trust-based exception suitable for "Very Close Person" scenarios. These permissions are album-scoped and apply only while the user retains the Collaborator role on that album.

### Partner Sharing (hypothesis)

With this RBAC model, partner sharing as “impersonation” can be removed in the long run. A partner relationship becomes a normal share of a library and/or albums with the **Collaborator** role (or other roles as needed). This consolidates all collaboration and access logic into one permission system and avoids having two parallel authorization models.

### Persona Counts

To get a better understanding, here are typical numbers of persona per Immich user.

| **Persona**                           | **Count per user** | **Reasoning**                                                                                                                   |
| ------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| **Instance Admin**                    | 1                  | Typically, there's only one main admin responsible for managing the entire instance, ensuring proper operations and governance. |
| **Very Close Person**                 | 1-3                | Represents a highly trusted individual, such as a life partner or close family members.                                         |
| **Known User in Immich**              | 5-10               | Small number of users who collaborate, but typically with restrictions on removal/irreversible actions.                         |
| **Public User with Temporary Rights** | 5-10               | Often users temporarily given limited rights for an event or project, typically via links.                                      |
| **Untrusted Public User**             | 1 to 1'000s        | Public users can be many, especially with public sharing, requiring simple and safe defaults.                                   |

## Metadata

## Metadata of assets

Shows an overview of all metadata associated with an asset. The last column categorizes metadata into different types with a base scope category.

| **Name**                     | **Description**                                                       | Editable | Base Scope |
| ---------------------------- | --------------------------------------------------------------------- | -------- | ---------- |
| **File Information**         | File name, extension, size, and type (image/video).                   | n        | A          |
| **Media Type**               | Differentiates between image, video, or live photo.                   | n        | A          |
| **Camera Details**           | Make, model, lens type, and settings (e.g., aperture, shutter speed). | n        | A          |
| **GPS Coordinates**          | Location data embedded in the file (latitude, longitude).             | y        | A          |
| **Date and Time**            | Original capture date and time of the media file.                     | y        | E          |
| **Description**              | Custom text or notes about the media.                                 | y        | E          |
| **Star Rating**              | One to five star rating of asset.                                     | y        | U          |
| **Tags**                     | Non hierarchical labels for categorization.                           | y        | E          |
| **Album Membership**         | Association between assets and albums (membership/placement).         | y        | S          |
| **Person Identity (Naming)** | Per-user naming/mapping of recognized faces to persons.               | y        | U          |
| **Objects**                  | Recognized objects in the media via machine learning.                 | n        | A          |
| **Favorites**                | Marked as a favorite by the user.                                     | y        | U          |
| **Archived Status**          | Whether the media is archived.                                        | y        | U          |

Legend for **Base Scope**:

- A: Close to immutable metadata of an asset with the exception of the date and time.
- E: Metadata that is shared and allows for collaborative edits by multiple users.
- S: Shared metadata is intended for use by multiple users beyond the asset's owner and remains the same for everyone. It is not personalized or user-specific but is shared uniformly across all users.
- U: Per-user overlay metadata intended to be controlled solely within an individual user’s scope. For authenticated users this can be applied to any visible asset; for unauthenticated link users it is not stored.

### Motivation for separation of metadata types

Some metadata should remain private per-user even when the asset is shared.

**Example and reasoning in the people context:**
User A names a person in their collection “Dad”. User B, who sees the same face in shared photos, might know this person as “Claude”. The identity mapping and naming is personal and should not leak between users.

Therefore:

- Face detection/recognition can run per asset (shared computation).
- The mapping/naming (“Person Identity”) is a per-user overlay and remains private.
- Each user can benefit from shared visibility of the asset without forcing naming alignment.

## Permissions Tables

### Metadata Types

This table proposes default and sane permissions for metadata categories for authenticated users. Unauthenticated public-link users are governed by link capabilities and do not get per-user overlay metadata storage.

| **Name**                     | **Editable** | **Base Scope** | **Instance Admin** | **Collaborator** | **Curator** | **Contributor** | **Viewer** |
| ---------------------------- | ------------ | -------------- | ------------------ | ---------------- | ----------- | --------------- | ---------- |
| **File Information**         | n            | A              | X                  | R                | R           | R               | R          |
| **Media Type**               | n            | A              | X                  | R                | R           | R               | R          |
| **Camera Details**           | n            | A              | X                  | R                | R           | R               | R          |
| **GPS Coordinates**          | y            | A              | X                  | R/W              | R/W         | R               | R          |
| **Date and Time**            | y            | E              | X                  | R/W              | R/W         | R               | R          |
| **Description**              | y            | E              | X                  | R/W              | R/W         | R/W (own)       | R          |
| **Star Rating**              | y            | U              | X                  | R/W              | R/W         | R/W             | R/W        |
| **Tags**                     | y            | E              | X                  | R/W              | R/W         | R/W             | R          |
| **Album Membership**         | y            | S              | X                  | R/W              | R/W         | R               | R          |
| **Person Identity (Naming)** | y            | U              | X                  | R/W              | R/W         | R/W             | R/W        |
| **Objects**                  | n            | A              | X                  | R                | R           | R               | R          |
| **Favorites**                | y            | U              | X                  | R/W              | R/W         | R/W             | R/W        |
| **Archived Status**          | y            | U              | X                  | R/W              | R           | X               | X          |

Notes:

- "Viewer" in this table refers to authenticated viewers. Unauthenticated public viewers do not have stored per-user overlays.
- "Album Membership" edits are primarily expressed via album-scoped operations. Contributors can see membership but do not broadly modify it (except indirectly by uploading to an album, which creates membership for the uploaded asset).
- **R/W (own)** means the role can edit this metadata only on assets they own (uploaded themselves). This allows Contributors to correct mistakes on their own uploads without broader edit access.

### Operations

Proposed list of operations and their permissions based on the abstracted roles.

| **Permission / Operation**              | **Collaborator** | **Curator** | **Contributor** | **Viewer** |
| --------------------------------------- | ---------------- | ----------- | --------------- | ---------- |
| **Move Asset to Trash**                 | y                | n           | n               | n          |
| **Restore from Trash**                  | y                | n           | n               | n          |
| **Permanently Delete Asset**            | y                | n           | n               | n          |
| **Download Assets**                     | y                | y           | y               | y/n        |
| **Upload Assets to Album**              | y                | y           | y               | n          |
| **Remove Asset from Album**             | y                | y           | n               | n          |
| **Replace with New Image**              | y                | n           | n               | n          |
| **Trigger Metadata Refresh**            | y                | y           | n               | n          |
| **Trigger Face Detection/Recognition**  | y                | y           | n               | n          |
| **Duplicate Handling**                  | y                | y           | n               | n          |
| **Edit Album Title/Description**        | y                | y           | n               | n          |
| **Manage Album Members and Roles**      | y                | n           | n               | n          |
| **Manage Public Link Settings (Album)** | y                | y           | n               | n          |

Notes:

- The instance admin is excluded from these operations because they have no access to user asset data/metadata; they only manage system operations.
- The owner(s) of an asset have all operations on that asset by default.
- **Metadata editing vs. computational operations**:
  - *Editing metadata values* (Description, Tags, Date/Time, GPS) is governed by the Metadata Types table and can be done by roles with R/W access to that metadata type.
  - *Triggering computational operations* (Refresh Metadata, Refresh Faces) requires explicit operation permissions as shown above. These operations re-process or re-extract data and are more expensive/impactful than simple edits.
  - Example: A Curator can edit a tag value (R/W on Tags) but cannot trigger a full metadata refresh on an asset they don't own.

## Public Links

Public links are intended for external access and do not require accounts. They are governed by link capabilities.

### Public Link Capability Options

A public link can be configured to allow:

- **view**
- **download**
- **upload**
- **remove own uploads** (optional, default off)

### Conceptual Model for "Remove Own Uploads"

The "remove own uploads" capability grants temporary, session-scoped deletion rights to unauthenticated public link users for assets they upload.

#### Ownership Model for Public Link Uploads

- **Public link users have temporary asset ownership**: When an unauthenticated user uploads an asset through a public link, they become the temporary owner of that asset within the context of that link session.
- **Session-scoped ownership**: Unlike authenticated users whose ownership is permanent and account-bound, public link ownership is bound to a transient session identity.
- **No persistent library**: Public link users have no personal library; their uploaded assets exist only in the album.

#### Permission Scope and Constraints

The "remove own uploads" capability is governed by the following conceptual constraints:

**Scope boundaries:**
- **Link-scoped**: Only works for assets uploaded through this specific public link (not across different links to the same album).
- **Session-scoped**: Only the session that uploaded the asset can delete it (requires session identity mechanism).
- **Album-context-bound**: Deletion only works within the album context where upload occurred.

**Time and lifecycle constraints:**
- **Time-limited capability**: The delete capability expires after a reasonable time window (concept: multiple days, not indefinite).
- **Link expiry revokes capability**: When the public link expires or is revoked, all associated delete capabilities are immediately revoked.
- **No trash management**: Public link users cannot move assets to trash or restore from trash. "Remove own uploads" performs permanent deletion.

**Interaction with authenticated user actions:**
- **Escalation constraint**: If an authenticated user takes action on a public-uploaded asset (adds to another album, favorites, tags with shared metadata), the public user's delete capability may be revoked to prevent interference with authenticated curation work.
- **Album owner retains ultimate control**: The album owner can always remove assets from the album or disable the "remove own uploads" capability entirely.

#### Edge Case Behaviors

| **Scenario** | **Behavior** | **Rationale** |
|--------------|--------------|---------------|
| Public user uploads, then link expires | Delete capability immediately revoked | Link owner retains control; link expiry ends all public capabilities |
| Asset added to second album by authenticated user | Delete capability revoked (optional policy) | Prevents anonymous deletion of curated content |
| Public user uploads duplicate (same file hash) | Creates new asset instance; user owns this instance | Each upload is independent; deduplication handled separately |
| Asset has been favorited/tagged by authenticated user | Delete capability revoked (optional policy) | Protects authenticated user's curation work |
| Public user deletes asset accidentally | No restore mechanism (permanent deletion) | Public users have no trash management; keeps model simple |
| Session identity lost (cookie cleared, browser switch) | Delete capability lost for previous uploads | Session-bound capability; no recovery mechanism |

#### Relationship to Permission Model

"Remove own uploads" fits into the overall permission model as:

- **Not an RBAC role**: Public link capabilities operate outside the role-based permission system (unauthenticated users have no roles).
- **Capability-based permission**: The public link grants specific capabilities (view, download, upload, remove own uploads) independent of roles.
- **Ownership-based constraint**: Follows the ownership model where uploaders own their assets, but for public users this ownership is temporary and session-scoped.
- **Consistent with asset-scoped permissions**: Deletion is an asset-scoped operation, but in this case scoped to the link/session context.

#### User Experience Expectations

The UI must clearly distinguish between "your uploads" and other content to avoid confusion:

- **Visual distinction**: Public users must be able to identify which assets they uploaded and can delete.
- **Capability visibility**: Delete actions should only be available on eligible assets (session-owned, within time window, not escalated).
- **Feedback on constraints**: If delete capability is revoked (link expired, time window passed, asset escalated), the UI should explain why.
- **Warning on first use**: Users should be informed that delete capability is temporary and session-bound (not recoverable if session is lost).

Public link users interact through mobile web (shared link opened in a browser). No mobile app experience is assumed.

## Examples

### Example 1: Subcontractor uploads to a project album

- Album owner shares album with subcontractor (authenticated Immich user) with role **Contributor**.
- Subcontractor can upload assets to the album.
- Subcontractor owns the assets they upload and can access them in their personal library.
- Subcontractor cannot remove any assets from the album and cannot move any asset to trash or permanently delete (Contributor role restrictions).
- Subcontractor can favorite/rate any visible asset for their own private curation (per-user overlays).
- Subcontractor can edit descriptions on assets they own (R/W (own) permission).
- Album owner can manage the asset's presence in the album (remove from album, reorder) but cannot delete the subcontractor's assets from the subcontractor's library.

### Example 2: Wedding guests upload via public link

- Album owner creates a public link with **upload enabled** and **remove own uploads enabled** (7-day window).
- Guests upload via mobile web.
- Guests can view uploads and existing album content as allowed by the link.
- Guests cannot edit shared metadata and cannot remove others' assets.
- Guests can delete only their own uploads within the 7-day window and only from the same browser session.
- If a guest uploads a wrong photo and realizes it immediately, they can delete it (permanent deletion, no trash).
- If the album owner adds a guest's photo to a separate "Best Photos" album, the guest can no longer delete it (escalation constraint).
- Once the link expires, all guests lose delete capability even if the 7-day window hasn't passed.

### Example 3: Partner collaboration without partner sharing impersonation

- User A shares their library/albums with User B with role **Collaborator**.
- User B chooses to show these shared assets in their timeline (per-album timeline visibility preference).
- User B can curate shared metadata (tags, descriptions) and remove assets where allowed.
- Per-user overlays remain private (favorites, ratings, person naming).

## Measures to Avoid Accidental Mass Removal and Metadata Issues

**Non-removal defaults for limited-trust roles:**

- Measure: Curator and Contributor are non-removal by default.
- Mitigation: Prevents accidental deletion/removal in common collaboration scenarios (family, teams, subcontractors). Owners can grant Collaborator where full trust exists.

**Clear separation of removal actions:**

- Measure: Distinguish between:
  - remove from album (album-scoped)
  - move to trash (asset-scoped, reversible)
  - permanent delete (asset-scoped, irreversible)

- Mitigation: Enables safer defaults and clearer UX/authorization.

**Trash visibility and recovery:**

- Measure: When an asset is moved to trash, it is treated as removed from shared views unless explicitly included.
- Mitigation: Prevents confusion and supports recovery workflows.

**Confirmation dialogs for irreversible or high-impact actions:**

- Measure: Implement confirmation dialogs or multi-step verification for actions such as bulk removal, move-to-trash, and permanent delete.
- Mitigation: Users must explicitly confirm their actions, reducing the likelihood of accidental modifications or removals.

## Enforcement and UX Guidance

- The server is the source of truth for authorization. UI prevention is a usability feature, not a security control.
- If the user lacks permission:
  - Prefer disabling or hiding the action with a short explanation.
  - If the action is attempted (race conditions, stale UI), return a specific error describing what is missing and how to resolve it (e.g., “Ask the album owner for Curator access”).
