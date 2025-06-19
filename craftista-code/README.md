

### Micro Service 01 - Frontend

**Purpose**: 
Serves as the frontend, acts as a router, integrates with all other services renders the  Graphical Interface.  

**Language**: Node.js  

**Framework**: Express.js  

**Why Express.js**: 
Express.js is a widely adopted and highly versatile web application framework for Node.js, offering several compelling reasons for its use. Its simplicity and minimalistic design make it an excellent choice for both beginners and experienced developers. Express.js provides a robust set of features and middleware, enabling rapid development of web applications and APIs. It excels at handling routes, HTTP requests, and various response types, allowing developers to build scalable and efficient server-side applications. Additionally, its active community and extensive ecosystem of plugins and modules make it easy to integrate with databases, authentication systems, and other technologies, streamlining the development process. Express.js's performance and flexibility, combined with its supportive community, make it a go-to choice for building web applications and APIs in Node.js.  

**Who uses Express.js:** 
Uber, Netflix, PayPal, LinkedIn, Groupon, Mozilla, Trello, Stack Overflow, GitHub, Myntra, Zomato,Trivago  


### Micro Service 02 - Catalogue

**Purpose:** 
Manages the origami showcase, including origami details and images.  

**Language:** Python  

**Framework:** Flask  

**Why Flask:** 
Flask is a lightweight and highly flexible Python web framework, making it an attractive choice for web developers. Its simplicity and minimalist design offer a low learning curve, making it ideal for small to medium-sized projects or when you need to quickly prototype an idea. Flask allows developers the freedom to choose components and libraries, giving them control over the tech stack and allowing for greater customization. It's well-suited for building RESTful APIs and web applications due to its clean and intuitive routing system. Flask also benefits from a supportive community and extensive documentation, ensuring developers have access to valuable resources when facing challenges. Overall, Flask's simplicity, flexibility, and ease of use make it a compelling choice for Python developers looking to build web applications and APIs efficiently and with a high degree of control.  

**Who uses Flask:** 
Netflix, Reddit, Lyft, Airbnb, Pinterest, Twilio, LinkedIn, MIT, Uber, Dropbox, Whitehouse.gov, Coursera  

#### Backing Service 01: catalogue-db  
Phase 1 : JSON File  
Phase 2 : MongoDB  

###  Micro Service 03 - Voting

**Purpose:** 
Handles the voting functionality, allowing users to vote for their favorite origami.  
**Framework:** Spring Boot   
**Why Spring Boot Framework:**
Spring Boot is a powerful and widely adopted Java-based framework that offers numerous advantages for developers. It excels in simplifying the development of production-ready, stand-alone, and enterprise-grade applications. One of its key strengths is convention over configuration, which significantly reduces boilerplate code and allows developers to focus on building features rather than dealing with infrastructure concerns. Spring Boot's comprehensive ecosystem provides support for various modules like data access, security, and messaging, simplifying integration with databases and third-party services. It also includes embedded servers, making it easy to deploy applications without the need for external web servers. Moreover, Spring Boot benefits from a vast and active community, ensuring access to extensive documentation and a wealth of resources. Overall, Spring Boot is a go-to choice for Java developers seeking rapid application development, maintainability, and scalability for a wide range of projects, from microservices to monolithic applications.  
**Who uses Spring Boot:**  
Adobe, Microsoft, Yelp, American Express, Intuit, Vimeo, SoundCloud  

#### Backing Service 02 : voting-db
Phase 1 : H2  
Phase 2 : PostgreSQL  


###  Micro Service 04 - Recommendation 

**Purpose:** 
Selects and presents the daily origami recommendation.    
**Language:** Golang  
**Why Golang:** 
Go, also known as Golang, is a programming language developed by Google. It has gained popularity for its simplicity, performance, and suitability for building scalable and concurrent applications. It's also a compiled language, which makes it more efficient than other languages.Many companies and projects around the world use Go in their tech stack. Golang's performance and flexibility make it a compelling choice for developers looking to build robust and reliable applications. Many DevOps tools are written in Go to take advantage of these benefits.  
**DevOps tools written in Go:**: 
Docker, Kubernetes, Prometheus, Terraform, Consul, Nomad, Packer, Vault, Grafana, etcd, Istio   
**Who uses Go Lang:** 
Google, Dropbox, Uber, Netflix, Twitch, Cloudflare, Heroku, X (Twitter), BBC  


Each service is built using a different technology stack, showcasing polyglot persistence and diverse backend technologies.

---



