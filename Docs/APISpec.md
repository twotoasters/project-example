# Project API Spec

## Version History
- 2-11-11-14 Daniel Hammond - Initial Draft
- 2-11-11-17 Someone Else - Changed /authenticate to follow new oauth based authentication flow

---


## Introduction

This API is going to be used by the iPhone and Android app to sync their data. Eventually a front end will for the web to view the data.

- Authenticate user session
- create new user accounts

## Resources

### User Account

The user endpoint exposes services for manipulating the User's account and also registering and logging in. This client must have a valid session token and is required to be set in the header for access to all protected resources. 

**Questions**

- How do we handle forgot passwords?

#### User Object

- ```id``` (int) GUID for user
- ```email``` (string) Email address that user signed up with (also username)
- ```password``` (string) Password
- ```password_confirm``` (string) Password Confirm
- ```facebook_uid``` (int) GUID for linked Facebook account
- ```name``` (string) First and Last name
- ```gender``` (string) Gender ("male" or "female")
- ```birthday``` (string) Birthday as MM/DD/YYYY
- ```height``` (decimal) Height in centimeters 
- ```weight``` (decimal) Weight in pounds
- ```authentication_token``` a single access token for the user, stateless, must be included in any authorized request

#### POST /authenticate
    Discussion: 
        Attempts to log the user into the remote system via username and password.
    Examples: 
        Client POST { "user": { "username": "user1234", "password": "test123" } }
        Server response { "user": { "authentication_token": "83294873294jhdfksflkdjfa99" } }
    Status Codes:
        • 201 (Created) - Sent when the session was created. Returns a session object containing a session_token.
        • 422 (Unprocessable) - Credientials do not match any records

#### POST /registrations
    Discussion:
        Signs up a new user for the service by creating a new user. Can only happen when the user is not authenticated.
    Examples:
        Client POST { "user": { "email": "scott@twotoasters.com", "password": "new-password", 
						"password_confirm": "new-password", "name": "Scott Penrose",
						"gender": "male", "birthday": "08/10/1985", "height": 190.5, "weight": 180 } }
		Server response { "user": { "email": "scott@twotoasters.com", "password": "new-password", 
						"password_confirm": "new-password", "gender": "male", "birthday": "08/10/1985", 
						"height": 190.5, "weight": 180, "authentication_token": "83294873294jhdfksflkdjfa99" } }
    Status Codes:
        • 201 (Created) - Returned when the user was created successfully.
        • 422 (Unprocessable Entity) - User sign-up failed. Return an error object describing the failure.

#### GET /user/:id
    Discussion:
        Retrieves account details from the server.
    Examples:
        Client GET /user/1
        Server response { "user": { "id": 1, "email": "scott@twotoasters.com", 
					"facebook_uid": 1234, "gender": "male", "birthday": "08/10/1985", 
					"height": 190.5, "weight": 180 }}
    Status Codes:
		• 200 (OK)
		• 404 (Not Found) - Unable to get user as it does not exist.

#### POST /user
    Discussion:
        Reserved for right now to later create a user through an admin interface if ever needed.
        
#### PUT /user/:id
    Discussion:
        Updates account information, such as changing password, gender, birthday, etc. The fields included in the update determine how the request is to be interpreted.
    Examples:
		Client POST { "user": { "email": "scott@twotoasters.com", 
					"password": "new-password", "passwordConfirmation": "new-password" } }`
		Server response { "user": { "id": 1, "email": "scott@twotoasters.com", 
					"facebook_uid": 1234, "gender": "male", "birthday": "08/10/1985", 
					"height": 190.5, "weight": 180 }}
    Status Codes:
		• 200 (OK)
		• 404 (Not Found) - Unable to update user as it does not exist.
		• 422 (Unprocessable Entity) - The updates failed due to an error. Return an error object indicating the failure.
        
#### DELETE /user/:id
    Discussion:
        Delete the user account from the server and terminate service.
    Examples:
        Client DELETE /user/1
    Status Codes:
		• 200 (OK) - Account was deleted successfully.
		• 404 (Not Found) - Unable to delete user as it does not exist.
