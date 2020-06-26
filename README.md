Conference App in a Box
This is the React Native CLI version. To view the Expo version, click here.

This repo goes along with my Dev.to post titled "Introducing Conference App in a Box"

Deploy a full stack & cross-platform mobile app for your next event in minutes.
🛠 Built with React Native, GraphQL, AWS Amplify, & AWS AppSync

Follow me on Twitter at @dabit3 to keep up with my future projects as well as updates and new features added to this one! If you need any help launching this app, please reach out to me I'd be happy to help.

Features
⚡️ Real-time chat
👾 Themeable & customizable
👮‍♂️ Authentication & Profile view
🔥 Serverless back end
🚀 GraphQL
💻 Deploy back end in minutes

  

Deploy the back end and run the app
Clone the repo & install the dependencies
~ git clone https://github.com/dabit3/conference-app-in-a-box.git

~ cd conference-app-in-a-box

~ npm install
Initialize and deploy the Amplify project
~ amplify init

? Enter a name for the environment: dev (or whatever you would like to call this env)
? Choose your default editor: <YOUR_EDITOR_OF_CHOICE>
? Do you want to use an AWS profile? Y

~ amplify push

? Are you sure you want to continue? Y
? Do you want to generate code for your newly created GraphQL API? N

> We already have the GraphQL code generated for this project, so generating it here is not necessary.
Start the app
~ react-native run-ios

# or

~ react-native run-android
To populate the database with your conference speakers
Sign up in the app after following the previous steps

Open the AppSync console:

~ amplify console api
Click on Queries to open the GraphiQL Editor. When prompted to "Login with User Pools", you can login with your new username and use the aws_user_pools_web_client_id located in aws-exports.js for the ClientId.

Create a new talk with the following GraphQL mutation:

mutation createTalk {
  createTalk(input: {
    name: "Performance In React Native",
    summary: "In this talk, we will look at the various tips and tricks for taking full advantage of React Native and using the performance attributes of the new architecture.",
    speakerName: "Ram Narasimhan",
    speakerBio: "Software Engineer at Facebook",
    time: "9:00 AM - 9:30 AM",
    timeStamp: "1573491600",
    date: "November 10",
    location: "Armory",
    speakerAvatar: "https://pbs.twimg.com/profile_images/875450414161772544/UjefWmmL_400x400.jpg"
  }) {
    id name speakerBio speakerName speakerAvatar location date time timeStamp
  }
}
Query for all talks with the following GraphQL query:
query listTalks {
  listTalks {
    items {
      name
      summary
      speakerName
      speakerBio
      time
      timeStamp
      date
      location
      speakerAvatar
    }
  }
}
Update a talk with the following GraphQL mutation:
mutation updateTalk {
  updateTalk(input: {
    id: "<TALK_ID>"
    name: "Performance in React Native & GraphQL"
  }) {
    id name
  }
}
Delete a talk with the following GraphQL mutation:
mutation deleteTalk {
  deleteTalk(input: {
    id: "<TALK_ID>"
  }) {
    id
  }
}
To customize with your theme and logo
Open src/theme.js and replace the highlight & primary colors.

Replace src/assets/logo.jpg with your logo.

To customize the GraphQL schema
This schema can be edited. If your event needs additional fields, you can update the backend by doing the following:

Update the schema (located at amplify/backend/api/rnconfinabox/schema.graphql).

Redeploy the back end:

~ amplify push
