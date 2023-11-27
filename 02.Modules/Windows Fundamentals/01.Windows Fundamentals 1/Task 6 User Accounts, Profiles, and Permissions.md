User accounts can be one of two types on a typical local Windows system: **Administrator** & **Standard User**. 

The user account type will determine what actions the user can perform on that specific Windows system. 

- An Administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc. 
- A Standard User can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

You are currently logged in as an Administrator. There are several ways to determine which user accounts exist on the system. 

One way is to click the `Start Menu` and type `Other User`. A shortcut to `System Settings > Other users` should appear. 

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user1.png)  

If you click on it, a Settings window should now appear. See below.

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user.png)  

Since you're the Administrator, you see an option to **Add someone else to this PC**.

**Note**: A Standard User will not see this option.  

Click on the local user account. More options should appear: **Change account type** and **Remove**. 

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user2.png)  

Click on Change account type. The value in the drop-down box (or the highlighted value if you click the drop-down) is the current account type. 

![](https://assets.tryhackme.com/additional/win-fun1/win-other-user3.png)

When a user account is created, a profile is created for the user. The location for each user profile folder will fall under is C:\Users.

For example, the user profile folder for the user account Max will be C:\Users\Max.

The creation of the user's profile is done upon initial login. When a new user account logs in to a local system for the first time, they'll see several messages on the login screen. One of the messages, User Profile Service, sits on the login screen for a while, which is at work creating the user profile. See below.

 ![](https://assets.tryhackme.com/additional/win-fun1/win-profile-service.png)

Once logged in, the user will see a dialog box similar to the one below (again), indicating that the profile is in creation.

![](https://assets.tryhackme.com/additional/win-fun1/win-profile-service2.png)  

Each user profile will have the same folders; a few of them are:

- Desktop
- Documents
- Downloads
- Music
- Pictures

Another way to access this information, and then some, is using **Local User and Group Management**. 

Right-click on the Start Menu and click **Run**. Type `lusrmgr.msc`. See below

![](https://assets.tryhackme.com/additional/win-fun1/win-lusrmgr.gif)  

**Note**: The Run Dialog Box allows us to open items quickly. 

Back to lusrmgr, you should see two folders: **Users** and **Groups**. 

If you click on Groups, you see all the names of the local groups along with a brief description for each group. 

Each group has permissions set to it, and users are assigned/added to groups by the Administrator. When a user is assigned to a group, the user inherits the permissions of that group. A user can be assigned to multiple groups.

**Note**: If you click on **Add someone else to this PC** from **Other users**, it will open **Local Users and Management**. 

Answer the questions below

| Question                                                   | Answer                      |
| ---------------------------------------------------------- | --------------------------- |
| What is the name of the other user account?                | tryhackmebilly              |
| What groups is this user a member of?                      | Remote Desktop Users, Users |
| What built-in account is for guest access to the computer? | Guest                       |
| What is the account status?                                | Account is disabled                            |
