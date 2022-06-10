# Letmeask
A application similar to slido that let users create Q&A rooms with upvote functionalities.

### Figma layout
<a href="https://www.figma.com/file/DdiDUFXs9lec5qKaVfBeo0/Letmeask-(Community)?node-id=0%3A1">
https://www.figma.com/file/DdiDUFXs9lec5qKaVfBeo0/Letmeask-(Community)?node-id=0%3A1
</a>

### Firebase setup
Create a new Firebase project with Google authentication and realtime database.
<br>
Use the project keys to create a .env.local file in the root of your project.
#### Root file: .env.local
```
REACT_APP_API_KEY="your_api_key"
REACT_APP_AUTH_DOMAIN="your_auth_domain"
REACT_APP_DATABASE_URL="your_database_url"
REACT_APP_PROJECT_ID="your_project_id"
REACT_APP_STORAGE_BUCKET="your_storage_bucket"
REACT_APP_MESSAGING_SENDER_ID="your_sender_id"
REACT_APP_APP_ID="your_app_key"
```
#### Realtime database rules
```json
{
  "rules": {
    "rooms": {
      ".read": false,
      ".write": "auth != null",
      "$roomId": {
        ".read": true,
        ".write": "auth != null && (!data.exists() || data.child('authorId').val() == auth.id)",
        "questions": {
          ".read": true,
          ".write": "auth != null && (!data.exists() || data.parent().child('authorId').val() == auth.id)",
          "likes": {
            ".read": true,
            ".write": "auth != null && (!data.exists() || data.child('authorId').val() == auth.id)",  
          }
        }
      }
    }
  }
}
```