GroupGate

==>INTRODUCTION:

GroupGate is a web application that helps its users to find team members 
for their group projects. After the group project is finished, the user has
an option to rate the team members performance on the project.


==>INSTALLATION:

Pre-requisites: Git, Vagrant and VirtualBox installed on your machine 

1) in terminal: git clone git@github.com:otaxar/groupgate.git

2) in terminal: cd GG-final

3) in terminal: vagrant up

4) In web browser: http://localhost:3000

NOTE: Please allow some time after the server starts.


==>FEATURES:

1) Sign up
2) Login
3) Logout

4) MyProfile > Basic Info > Edit (Username and About Me)

5) MyProfile > Courses > Add, Delete: 
     —> A) When adding, the course name is uppercased and white space removed.
            B) Validation for empty field
            C) Validation for already existing course

6) MyProfile > Reference profiles > Add, Delete:
      —> NOTE: The profile link must be in the format http://www.webname...

7) Groups > Groups w/ Admin rights > Add/Edit/Delete
     —> NOTE: once there are group members added to the group, it is possible to rate the group members
     —> indication about the status of the group rating: (No members yet, ‘Rate members’ button, Members rated)
     —> indication who is the group admin and group members

8) Other users
     —> List of current users
     —> Options: Details —> View users details (profile, avg rating for each sub-category)
                          Invite —> Invite user to a group

      Issues/Room for improvement:
       A) pagination feature needs to be implemented: once there is a lot of records displayed, it will be tedious to scroll down/up

9) Invitations
     —> List of Invitations sent: 
                      Each invitation status (pending, accepted, declined)
                      Current user can cancel his/her invitation only while it is still in ‘Pending’ status
     —> List of invitations received:
                      Each invitation has its status (pending, accepted, declined)
                      Current user can Accept or Decline the invitation
                      History of invitations 

      Issues/Room for improvement:
        A) 2 tabs could be implemented to display only invitations sent or only invitation received to avoid screen cluttering
        B) pagination feature needs to be implemented: once there is a lot of records displayed, it will be tedious to scroll down/up


           
==>CURRENT ISSUES:

1) After the first Login in the production build, the browser must be refreshed to display the User info. After that the info is displayed OK.
    This does not happen in the Dev version. 
    Probably related to the async nature of setState().
    Possible solution(s): a) callback function to parent component
                          b) use Redux to store state

2) Some API calls get ‘unauthorized’ response when used for the first time, but working the next time.
    - not sure if is is caused by the ACL not being granular enough, or by the async nature of setState()

3) various small glitches in the system, most likely caused by the asynch nature of setState()
    - possible solution: some of the errors were eliminated when calling the callback functions of the parent component from within the setState() fn. Introduce Redux package and handle the states in Redux.
   
4) App currently does NOT  auto-logout the user if browser window is closed, or history cleared, creates a problem at the next reopen.

5) In general, somewhat “naive” implementation. I doubt it would scale up well with large number of users. 
    Originally started with Rails API and was able to get all user info at once at the App level and pass the info down to various pages.
    Then encountered some issues with update, that could not be quickly resolved, so I fell back on Loopback and the “component” loading, because the ease of setup.

6) Vagrant halt currently does not work (throws error). Using vagrant suspend and resume (or reload) instead.  
 

==>LIVE DEMO at: http://csil-cpu00.cs.surrey.sfu.ca:7105/
(might get deleted via regular delete maintenance)

==> SCREENCAST DEMO: 
https://www.youtube.com/watch?v=LWQqMRZ7CV8&t=841s


==> TODO:
1) Rework the token handling and security in general, remove token when browser window closed. 
2) Implement Redux
3) Implmenent Rails API (Load all user in single API Call after login)
4) Rework the rating logic (more granular approach, allow selecting individual group members only)
5) Add new status 'Completed', allow feedback only after this status is selected.
