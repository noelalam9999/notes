## Back-end configuration variables
- Any string constant in your back-end code that contains information which is sensitive (e.g. API keys, database credentials, app secrets and salts, etc.) or shared across different files (e.g. API URLs, pre-defined directory paths, etc.) should be stored in a dedicated configuration file.
- This means you should have at least two configuration files. The one containing private information should be added to .gitignore and not committed to your repo.
- Configuration files in Node can be .js or .json files, that can be imported in your code where needed. Otherwise, you can use the dotenv package to leverage environment variables, which can be accessed through the process.env global object.
- If your app is deployed to production (i.e. it’s accessible to its final users), your configuration files should contain both the development and production settings, and your app logic should pick the correct ones depending on the environment (e.g. use a different db for dev and prod, since you don’t want to affect your real users data when developing your app). 

## Good practices before deploying
- Before running your app in production, it’s a good idea to use a versioning system, enforce code linting, have automated tests, and use an error-tracking platform.
- Any web client code should be minified, and all the app assets should be compressed, to reduce the network transmission time.

## Deployment basics
- Deploying your code means publishing it, so that the final users can consume your app.
- Depending on your app type, this involves serving dynamic and/or static data.
- Data is considered “dynamic” if the response to each request can be different (e.g. an API), which typically involves interacting with a database or other services.
- Data is considered “static” instead if the same request always receives the same response (e.g. an image or video, web client files, or an app package for mobile or desktop).
- A single server can provide dynamic and static data, or you can use separate servers that are optimized for their specific purpose.
- Any assets, to be reachable over the Internet, need to be provided by a server with a public IP address. In most cases, it makes sense to have a domain name that points to such IP address, since it’s easier for users to share and remember.
- Domain names can be obtained from a registrar (e.g. Google Domains). If a domain is still available, you can register it for a yearly fee, and point it to the IP address of the server that contains your assets.

## Hosting options
- Static assets for apps that are made for a specific platform are typically published through a dedicated third-party service (e.g. the App Store for Apple, Google Play for Android, npm for Node, or the packages archive for Linux).
- In all other cases where you need to take care of the server infrastructure instead, these are the main options available:
- In-house. You fully manage your own hardware, software, power supply, and Internet connectivity.
- Third-party dedicated server. You pay monthly or yearly for a company to provide the hardware that you request and keep it connected to a public IP address (but you still need to manage all the software on each machine, including any required updates).
- VPS (virtual private server). Is like a dedicated server, but the same computer is divided into multiple virtual machines and shared by different customers.
- PaaS (platform as a service). You only need to upload your code or assets, and everything else is managed by the service provider (including the operating system, database, and runtime environment).
- Each project is different. The most relevant factors to consider are the hardware and software features you need, together with the cost, scalability, and maintenance requirements.
- Generally speaking, small projects are better suited to a PaaS solution, but at a certain scale it can become too expensive, and having a dedicated server or in-house infrastructure might be a better fit.
- Always use HTTPs in production. A PaaS can provide this for you through a shared domain, but otherwise you need to get an SSL certificate and set up your server to use it.