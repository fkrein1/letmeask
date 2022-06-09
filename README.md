# Letmeask

## Firebase Setup
### .env.local Root File
```
REACT_APP_API_KEY="your_api_key"
REACT_APP_AUTH_DOMAIN="your_auth_domain"
REACT_APP_DATABASE_URL="your_database_url"
REACT_APP_PROJECT_ID="your_project_id"
REACT_APP_STORAGE_BUCKET="your_storage_bucket"
REACT_APP_MESSAGING_SENDER_ID="your_sender_id"
REACT_APP_APP_ID="your_app_key"
```
### Realtime Database Rules
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