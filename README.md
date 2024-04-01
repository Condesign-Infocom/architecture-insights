### GOALS

- [x] We want to define our issues and come up with solutions
- [ ] We want a controllable and error-prone way to update our products.
- [ ] We want to eliminate our reliance on Excel files and CSVs.
- [ ] We want to use STRAPI for powering up our product-related flows.

### QUICK ARCHITECTURE MEMO

<!-- TOPIC -->
<br/>
<b>
Here is a quick recap of our architecture.
</b>
<br/>
<br/>


[glasbutiken-server](https://github.com/simonwe-condesign/glasbutiken-server)
This repository should contain the core STRAPI application code, including models, controllers, services, and configurations.

[glasbutiken-backend](https://github.com/simonwe-condesign/glasbutiken-backend/tree/31c8654e6746d8bcbcde4a7011a38f4602d6617a)
This might contain additional back-end logic or functionalities specific to your application that are not handled by STRAPI, like authentication. However it contains implementations that are not following the best practices.

[digitalocean.com/databases](https://cloud.digitalocean.com/databases/57ad4f80-52c4-44ba-84d8-fd25a41ca6a4?i=0a363a)
We have PostgreSQL database deployed on Digital Ocean to store the data managed by our STRAPI application, and we should keep it open only to STRAPI. Right now it is opened all incoming connections.

[glasbutiken-client](https://github.com/Condesign-Infocom/glasbutiken-client)
Our main front-end application which is consumed by clients.

[glasbutiken-admin](https://github.com/simonwe-condesign/glasbutiken-admin)
This contains the code for the interface with our STRAPI application?
It should be used as primary way for administrators to manage content.


### ISSUES

<!-- TOPIC -->
<br/>
<b>
We use local Excel files to manage our products.
</b>
<br/>
<br/>

We should use Stripe to manage our product data instead of manually moving Excel or any local computer files.
This involves creating entries for each product, specifying its attributes, linking relevant resources, editing and other.
Basic approach is to manually enter data into STRAPI dashboard, however it also supports importing data from CSV files.

<!-- TOPIC -->
<br/>
<b>
Our back-end to database flow is confusing and poorly documented.
</b>
<br/>
<br/>

Our project involves a combination of using STRAPI and writing raw SQL queries.
I think that it is beneficial to maintain consistency throughout the application, as it is very hard to debug and share resources for future development.

We should strive for a unified approach, because riting raw SQL queries introduces security risks such as SQL injection vulnerabilities, we also have to be aware of proper input validation, queries, and access controls.

We should discuss the migration strategy from manual SQL queries to STRAPI for all database interactions.

### SOLUTIONS

<!-- TOPIC -->
<br/>
<b>
We better split STRAPI for handling our products, and keep back-end for rest.
</b>
<br/>
<br/>

STRAPI should act as an interface between your back-end and the underlying database.
When you use STRAPI, you do not need to directly write SQL queries in your back-end code, like how we do it now.

We have to spend some time analyzing what data goes where and start a refactor.
Ideally, we should talk to STRAPI API for cases like management of products in the database, for the rest we should use our custom back-end.

I reviewed the application requirements and consider that we should use STRAPI to fulfil all our needs in terms of products. They also support authentication, but I need a deeper dive into that.

In theory we can drop custom back-end all together, as STRAPI abstracts away these details, and starts a server behind the scenes to serve our application.


<!-- TOPIC -->
<br/>
<b>
We should dedicate some time to document things out.
</b>
<br/>
<br/>

Once we are done with refactor, and code migration, we should spend some time to actually build up some documents like this one you are reading, to keep up some insights and gained knowledge.


<!-- TOPIC -->
<br/>
<b>
We need to figure out the access issue.
</b>
<br/>
<br/>


By incorporating STRAPI features such as user-friendly admin panel, CSV import support, and API-based data retrieval we will use its capabilities to their fullest extent, which is essential for efficient development and maintenance.

I am blocked by no access to STRAPI, as we rely on it for majority of our flows.
We need to figure out the way to share access to our https://strapi.io/

