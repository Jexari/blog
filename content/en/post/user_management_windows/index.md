---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "User management in Windows"
subtitle: ""
summary: "Managing local user accounts via lusrmgr.msc and cmd."
authors: []
tags: [Windows, System administrator]
categories: [System administrator]
date: 2022-11-27T21:42:56+03:00
lastmod: 2022-11-27T21:42:56+03:00
featured: true
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
<details class="toc-inpage d-print-none  " open="">
<summary class="font-weight-bold">Content</summary>
<nav id="TableOfContents" class="nav flex-column">
<ul>
<li class="nav-item"><a href="#introduction" class="nav-link"><span class="section-num">1</span> Introduction</a></li>
<li class="nav-item"><a href="#Управление-учетными-записями-через-lusrmgrmsc" class="nav-link"><span class="section-num">2</span> Account management via lusrmgr.msc</a></li>
<li class="nav-item"><a href="#управление-учетными-записями-через-cmd" class="nav-link"><span class="section-num">3</span> Account management via cmd</a></li>
<li class="nav-item"><a href="#conclusion" class="nav-link"><span class="section-num">4</span> Conclusion</a></li>
</ul>
</nav>
</details>

<h2 id='introduction'><span class="section-num"><b>1</span>. Introduction</b></h2>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;An account is a set of data about a user that is necessary to authenticate him and provide access to his personal data and settings. Thus, an account consists of a username and password (or other means of authentication). The password is often encrypted or hashed. An account can store a user's photo or other image, take into account the age of various statistical characteristics of the user's behavior in the system.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;It is not uncommon for several users to work on the same computer. On Linux, it is more convenient to manage users on the command line. In the Microsoft family of operating systems, this feature is also present, as is the GUI (Graphical User Interface).</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Account management is one of the primary responsibilities of a system administrator. It is very convenient to combine users into groups, edit their access rights depending, for example, on their position in the company. This directly affects the security of the information system.</p>

<h2 id='Управление-учетными-записями-через-lusrmgrmsc'><span class="section-num"><b>2</span>. Account management via lusrmgr.msc</b></h2>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Immediately after installing Windows, we start working with Administrator rights. These rights in the OS allow, for example, to create, modify, delete other accounts, perform any operations to configure the system.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The lusrmgr.msc snap-in is used to manage accounts (Fig. 1). We can also open it by entering the name in the "Run" command field, or in the internal system search.</p>
<img align="middle" src="lusrmgr.jpg">
<p align="middle">Figure. 1. lusrmgr.msc window</p>
<p align="justify">In order to create an account, you need to do the following:</p>
<ol><li>Go to the "Users" folder (Fig. 2).</li>
<li>In the menu bar, select "Action", then "New User".</li>
<li>Be sure to fill in the "User" field, the rest if necessary (Fig. 3).</li></ol>

<img align="middle" src="users_in_os.jpg">
<p align="middle">Figure. 2. OS users</p>
<img align="middle" src="user-creation.jpg">
<p align="middle">Figure. 3. User creation</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A user group is a collection of user accounts that have the same rights and security permissions. The user account must be a member of at least one user group.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Different users have different needs, the administrator can allocate the necessary permissions and prohibitions. If we have many users, then it is convenient to distribute rights not individually, but by user groups. Windows has several built-in groups: Administrators, Users, Power Users, Backup Operators, Guests, Remote Desktop Users, DHCP Administrators, DHCP Users, and WINS Users. We can also create our own group. For this:</p>
<ol><li>Go to the "Groups" folder (Fig. 4).</li>
<li>In the menu bar, select "Action", then "Create Group".</li>
<li>Be sure to fill in the "Group Name" field, the rest if necessary (Fig. 5.1 - 5.2).</li></ol>

<img align="middle" src="list_os_all_users.jpg">
<p align="middle">Figure. 4. List of all groups</p>
<img align="middle" src="groups_creation.jpg">
<p align="middle">Figure. 5.1. Create a group</p>
<img align="middle" src="adding_a_user_to_a_group.jpg">
<p align="middle">Figure. 5.2. Adding users to a group</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can view which groups a user belongs to in the Users folder by right-clicking on the user, then selecting Properties, Group Memberships. If we go to the "General" tab, we can manage the user's password, and also, if necessary, disable the account (Fig. 6).</p>
<img align="middle" src="management_in_general.jpg">
<p align="middle">Figure. 6. Management in the "General" tab</p>

<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The administrator can also set password time limits, for this you need to use the gpedit.msc snap-in. Next, go to "Computer Configuration", "Windows Configuration", "Security Settings", "Account Policy", "Password Policy" (Fig. 7).</p>
<img align="middle" src="changing_the_password_expiration_time.jpg">
<p align="middle">Figure. 7. Changing the password expiration time</p>

<h2 id='управление-учетными-записями-через-cmd'><span class="section-num"><b>3</span>. Account management via cmd</b></h2>


<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As mentioned earlier, we can manage accounts through the command line. To begin with, we will write the command whoami and whoami /user (Fig. 8). The first displays information about the current user, the second additionally shows the SID (security identifier). SID is a variable length data structure that identifies a user, group, domain, or computer account. The last 4 digits indicate the object's relative security identifier (RID). 3 sets of numbers before RID is just the SID.</p>
<img align="middle" src="whoami_and_whoami_user.jpg">
<p align="middle">Figure. 8. whoami and whoami /user</p>

<p align="justify">For further account management, we need the net user command. With it, we can:</p>
<ul><li>add an account (net user NAME PASSWORD /ADD) (Fig. 9.1);</li>
<li>add account password (net user NAME PASSWORD) (Fig. 9.4);</li>
<li>rename account (wmic useraccount where name='NAME' rename ‘NEWNAME’) (Fig. 9.2);</li>
<li>view account information (net user NAME) (Fig. 9.3);</li>
<li>change account password (net user NAME NEW_PASSWORD);</li>
<li>disable account (net user NAME /active:no);</li>
<li>delete your account (net user NAME /delete) (Fig. 9.5).</li></ul>

<img align="middle" src="adding_an_account.jpg">
<p align="middle">Figure. 9.1. Adding an account</p>
<img align="middle" src="adding_an_account_2.jpg">
<p align="middle">Figure. 9.2. Adding an account</p>
<img align="middle" src="adding_an_account_3.jpg">
<p align="middle">Figure. 9.3. Adding an account</p>
<img align="middle" src="adding_a_password_to_account.jpg">
<p align="middle">Figure. 9.4. Adding a password to an account</p>
<img align="middle" src="delition_an_account.jpg">
<p align="middle">Figure. 9.5. Deleting an account</p>

<p align="justify">To work with groups, you must use the net localgroup command. For example, with it we can:</p>
<ul><li>list all local groups (net localgroup);</li>
<li>add local group (net localgroup GROUPNAME /add);</li>
<li>add existing user accounts to a group (net localgroup GROUPNAME USERNAME1 USERNAME2 /add /domain);</li>
<li>display a list of users in a local group (net localgroup GROUPNAME).</li></ul>

<h2 id='conclusion'><span class="section-num"><b>4</span>. Conclusion</b></h2>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thus, having become familiar with the basics of user management in the Windows operating system, we can draw the following conclusions:</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Creating an account, changing the account password, and many other actions can be performed both through various snap-ins and through the command line. In the second case, we can use, for example, the net user command. Also with group changes, they can also be done in the two ways described above.</p>
<p align="justify">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To ensure information security, it is necessary to sort their accounts into groups, where you can enter restrictions on their rights (for example, viewing certain folders).</p>
