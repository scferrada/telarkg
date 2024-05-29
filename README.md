# TelarKG

TelarKG is a Knowledge Graph that archives the political discussions and social media data related to the Chilean Constitutional Process of 2021-2021.
This document presents all the types of nodes, edges and properties present in TelarKG. In the following image, you may find a summary of the schema of the knowledge graph:

![Schema of TelarKG](https://github.com/scferrada/telarkg/blob/main/telarkg.png)

## Nodes

For each node label, we provide a brief description of the meaning of the label, and all available property names.

### ConventionMember

A node with label **ConventionMember** represents one of the people elected to the Constitutional Convention of 2021-2022. For instance, the node with id *pers_loncon_elisa* represents Elisa Loncón, the first president of the Constitutional Convention.

The properties that nodes with label **ConventionMember** have are:

- **name**: The first and last name of the Convention member.
- **inVoteName**: The name under which the Convention member appeared on the ballot. It may include their middle name and the last name of the mother.
- **occupation**: The current job occupation of the Convention member. 
- **description**: A short bio of the Convention member. 
- **electoralPact**: The pact under which the Convention member was elected. A pact is usually a group of political parties, or independently organized people.
- **age**: The age the Convention member had in 2021.
- **patrimony**: The declared owned patrimony of the Convention member at the time of election.
- **web**: The official website of the Convention member.
- **wikidata**: The Wikidata entity referring to the Convention member.
- **resignation**: A boolean value indicating if the Convention member resigned or not.

### Commission

The work to draft a new Constitution was organized in commissions. Each commission was in charge of a given set of topics such as Fundamental Rights, Indigenous Peoples, Environment, etc. Each commission was composed of several Convention members.

The properties that nodes with label **Commission** have are:

- **id**: an internal id to represent the commission.
- **name**: the name of the topic the commission works on.

### CommissionSession

A Commission had several sessions on which its members discussed and voted on different materials. A Commission Session only has an id.

### CommissionMaterial

A **CommissionMaterial** is a piece of text that is proposed to be included in the draft of the new Constitution that is related to the topic of the corresponding **Commission**. Materials are subject to vote by the members of the Commission, and thus can be approved or rejected. Approved materials are later discussed in a Plenary Session, and are voted again by all members of the Convention.

The properties that nodes with label **CommissionMaterial** have are:

- **material**: the proposed text to be included in the draft.
- **date**: the date the material was voted.
- **totalInFavor**: the number of votes in favor of the material
- **totalAgainst**: the number of votes against the material.
- **totalAbstention**: the number of commission members that abstained from voting.

### VoteResult

Nodes with label **VoteResult** model the possible outcomes of the vote on a material, and are thus constant. There are 4 nodes with this label and these are _vr_Aprobado_ for approved materials, _vr_Rechazado_ for rejected materials, _vr_Empate_ for materials with ties in the vote, and _vr_Sin_resultado_ for materials that were withdrawn by their authors before vote.

### PlenarySession

Nodes with label **PlenarySession** represent the sessions in which all the Convention members discussed and voted on the materials approved by the different commissions and, if approved in the plenary session, then the materials become part of the draft of the new Constitution.

**PlenarySession** nodes only have an internal id.

### PlenaryMaterial

Nodes with label **PlenaryMaterial** represent materials that were approved by a **Commission** and are to be discussed and voted in a **PlenarySession**.

The properties that nodes with label **PlenaryMaterial** have are:

- **material**: a summary of the subject that is being discussed and voted.
- **sessionAccount**: a complete account of the discussions and deliberations of the plenary session.
- **table**: the brief version of the agenda for the session.
- **detailTable**: the details of the agenda for the session.
- **totalInFavor**: the number of votes in favor of the material
- **totalAgainst**: the number of votes against the material.
- **totalAbstention**: the number of commission members that abstained from voting.
- **date**: the date the session was held.
- **materialKeywords**: keywords related to the material text.
- **sessionKeywords**: keywords related to the session proceedings.
- **url**: the URL pointing to the official archive of voting records of the Convention.
- **voteId**: the identifier of the vote on the Chilean Library and Archive.


### Video

Most of the commission and plenary sessions were live-streamed and recorded. We provide nodes with label **Video** to store the links to these videos.

The properties that nodes with label **Video** have are:

- **video**: a link to the recording of the session on YouTube.
- **duration**: the duration of the video.
- **videoName**: the title of the video on YouTube.

### Speech

On any given session, one or more Convention members gave speeches during the discussion of a material. Nodes with label **Speech** store information on these interventions with respect to the video of the session.

The properties that nodes with label **Speech** have are:

- **startYoutube**: the timestamp the speech starts on the YouTube video of the session.
- **endYoutube**: the timestamp the speec ends on the YouTube video of the session.
- **startTime**: the time of the day when the speech started.
- **text**: the (automatically generated) text version of the speech.

### Transcription

We extracted the YouTube transcription of all the videos and store them in nodes with label **Transcription**.

The properties that nodes with label **Transcription** have are:

- **text**: the full text of the transcription
- **date**: the date of the video

### Chat

We captured the live-chat archive of the live-streams of the sessions on YouTube. Each individual message is stored in a node with label **Chat**.

The properties that nodes with label **Chat** have are:

- **text**: the text of the message.
- **timeYoutube**: the timestamp when the chat was sent, relative to the start of the YouTube video.
- **date**: the date of the message.
- **user**: the public name of the user who sent the message.

### Gender, Party, Pact, District, and PoliticalGroupConvention

These labels model simple nodes stating the **Gender** of a Convention member, the political **Party**, the Electoral **Pact** (property **name**), and the **PoliticalGroupConvention** the Convention member is affiliated to, and the **District** that elected the Convention member. The nodes with these labels only have a **name** property.

### FacebookAccount

Nodes with label **FacebookAccount** represent the Facebook profiles or pages used by the Convention members, during their work in the Convention.

The properties that nodes with label **FacebookAccount** have are:

- **url**: the URL of the Facebook account.
- **name**: the public name of the Facebook account.
- **createdAt**: the date of creation of the account.
- **pageDescription**: the user-provided description of the account.
- **verified**: if the account is Facebook verified or not.
- **subscriberCount**: the number of subscribers to the account at the time of capture.
- **profileImage**: the URL of the profile image of the account.
- **handle**: the optional handle of the account.
- **accountType**: the type of account, whether it is a fan page or a personal profile.
- **pageAdminTopCountry**: the ISO code of the country of the admin. Usually CL (Chile).
- **platformId**: the Facebook id of the account.

### FacebookPost

We capture each post of the Facebook accounts of the Convention members in nodes with label **FacebookPost**.

The properties that nodes with label **FacebookPost** have are:

- **message**: the text of the post.
- **postUrl**: the URL to the post.
- **createdAt**: the date and time the post was uploaded.
- **updatedAt**: the date and time the post was updated.
- **score**: a score of the post provided by Facebook.
- **link**: if the post shares a link, it appears here.
- **title**: the title of the website the link points to.
- **description**: the description of the website the link points to.
- **caption**: the caption of the website the link points to.
- **subscriberCount**: the number of subscribers to the account at the time of posting.

### InstagramAccount

Nodes with label **InstagramAccount** represent the Instagram profiles used by the Convention members, during their work in the Convention.

The properties that nodes with label **InstagramAccount** have are:

- **handle**: the handle of the account.
- **name**: the name in the profile.
- **followersCount**: the number of followers at time of capture.
- **url**: the url to the Instagram profile.
- **profileImage**: the url to the profile image.
- **verified**: whether the account is verified or not
- **platformID**: the Instagram id of the account.
<!--id,platform-->

### InstagramPost

We capture each post of the Instagram accounts of the Convention members in nodes with label **InstagramPost**.

The properties that nodes with label **InstagramPost** have are:

- **postUrl**: the URL of the post.
- **description**: the caption of the post.
- **imageTex**: the automatically extracted text on the image.
- **createdAt**: the date and time the post was uploaded.
- **updatedAt**: the date and time the post was updated.
- **subscriberCount**: the number of subscribers of the account at the time of posting.
- **likeAndViewCountsDisabled**: whether the number of likes and views of the post is disabled or not.
- **score**: an Instagram provided score for the post.

<!--id,,,,,,legacyId,,score,-->

### TwitterAccount

Nodes with label **TwitterAccount** represent the X/Twitter profiles used by the Convention members, during their work in the Convention.

The properties that nodes with label **TwitterAccount** have are:

- **screenName**: the handle of the account.
- **name**: the public name of the account.
- **description**: the bio in the account's profile.
- **verified**: whether it is a verified account or not.
- **url**: the URL pointing to the account.
- **followersCount**: the number of followers at the time of capture.
- **favouritesCount**: the number of tweets marked as favorite by the account, at the time of capture.
- **statusesCount**: the number of tweets posted by the account, at the time of capture.
- **listedCount**: the number of lists the account belongs to, at time of capture.
- **createdAt**: the date and time of the creation of the account.
- **protected**: whether the account is private or not.
- **location**: the location declared in the bio.
- **profileBannerUrl**: URL to the banner image of the profile.
- **profileImageUrlHttps**: URL to the profile picture.
- **defaultProfileImage**: whether the profile has the default profile image or not.
- **defaultProfile**: whether the bio has the default value or not.

<!--id,strId,-->

### Tweet

Tweets were captured from Twitter during the timeframe of the Convention using keyword capturing provided by the Twitter API. Nodes with label **Tweet** have attributes corresponding to the JSON attributes obtained with the API, such as:

- **text**: the text of the tweet [currently removed due to X's policy].
- **createdAt**: the timestamp in which the tweet was posted.
- **id**: the tweet identifier on X.
- **retweeted**: whether the tweet was retweeted or not.
- **replyCount**: the number of replies at the time of capture.
- **favorited**: whether the tweet has been favorited/liked or not at the time of capture.
- **favoriteCount**: the number of times the tweet has been favorited/liked at the time of capture.
- **retweetCount**: the number of times the tweet has been retweeted at the time of capture.
- **quoteCount**: the number of times the tweet has been quoted, at the time of capture.
- **isQuoteStatus**: whether the tweet quotes another tweet or not.
- **inReplyToStatusId**: if the tweet is a reply to another tweet, the original tweet id is here.
- **inReplyToUserIdStr**: if the tweet is a reply to another tweet, the original tweet's user handle is here.
- **inReplyToUserId**: if the tweet is a reply to another tweet, the original tweet's user id is here.
- **inReplyToScreenName**: if the tweet is a reply to another tweet, the original tweet's user screen name is here.
- **isRetweet**: whether the tweet is a retweet or not.
- **withheldScope**: whether the tweet has limited visibility or not.
- **withheldCopyright**: whether the text copyright has been withheld or not.
- **possiblySensitive**: whether the tweet has been flagged as possibly sensitive or not.
- **truncated**: whether the text is truncated to 260 characters or not.

### Language

Social media posts have language metadata associated with them. This information is captured in nodes with label **Language**.

The properties that nodes with label **Language** have are:

- **name**: the name of the language.
- **wikidata**: the wikidata entity representing the language.
- **code**: the ISO code of the language.


### TypeContent

Social media posts come in a variety of media forms, like reels, photos, live streams etc. Nodes with label **TypeContent** capture this variety, with an attribute called **name** that describes this content type.

## Edges

For each edge label in TelarKG, we explain its meaning, its type(s) of source nodes, its type(s) of target nodes, and its properties if the edges have any.

### District

Edges with label **district** connect each **ConventionMember** node with the **District** node of the Chilean district the member represents.


### Gender

Edges with label **gender** connect each **ConventionMember** node with the **Gender** node of the gender of the member.

### PoliticalGroupConvention

Edges with label **politicalGroupConvention** connect each **ConventionMember** node with the **PoliticalGroupConvention** node of the political affinity group the member belongs to.

### Party

Edges with label **party** connect each **ConventionMember** node with the **Party** node of the political party the member belongs to.

### Pact

Edges with label **pact** connect a **Party** node with the **Pact** node if the political party belongs to a given electoral pact.


### Author

Edges with label **author** represent the authorship relation between a Convention member (a **ConventionMember** node) and a Commission material (a **CommissionMaterial** node).

### CommissionSession

Edges with label **commissionSession** connect each **CommissionMaterial** to the **CommissionSession** the material was discussed and voted on.

### Commission

Edges with label **commission** connect each **CommissionMaterial** to the **Commission** the material is related to on.

### PlenarySession

Edges with label **plenarySession** connect each **PlenaryMaterial** to the **PlenarySession** the material was discussed and voted on.

### Vote

Edges with label **vote** model the voting of each **ConventionMember** on a given **CommissionMaterial** or **PlenaryMaterial**. These edges have a property **voteWord** which stores the option selected by the **ConventionMember**.

### Result

Edges with label **result** connect **CommissionMaterial** and **PlenaryMaterial** nodes with the corresponding **VoteResult** node, depending on the result of the voting of the material.

### Video

Edges with label **video** connect each **Video** with the **PlenarySession**, or **Speech** recorded on the video. 

### Transcription

Edges with label **transcription** connect each **Video** node with their corresponding **Transcription** node.

### Chat

Edges with label **chat** connect each **Video** node with the **Chat** nodes representing chat messages of that video.

### Speaker

Edges with label **speaker** connect each **Speech** node with the node of the **ConventionMember** giving the speech.

### HasAccount

Edges with label **hasAccount** connect **ConventionMember** nodes with their social media accounts, either **InstagramAccount**, **FacebookAccount**, and/or **TwitterAccount**.

### PostedBy

Edges with label **postedBy** connect social media posts with the social media accounts that made them: **InstagramPost**s with **InstagramAccount**s, **FacebookPost**s with **FacebookAccount**s, and **Tweet**s with **TwitterAccount**s.

### Language

Edges with label **language** connect social media posts (nodes with label **InstagramPost**, **FacebookPost**, and **Tweet**) with the **Language** node corresponding to the language detected in the post.

### TypeContent

Edges with label **typeContent** connect social media posts from Instagram and Facebook (**InstagramPost** and **FacebookPost** nodes) with the **TypeContent** node that represents the content type of the post.

### InReplyTo/QuotingTo

Edges with labels **inReplyTo** or **quotingTo** connect **Tweet** nodes with other **Tweet** nodes they reply to or quote.
