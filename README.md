# Problem Statement
Develop a high level design of a robust and user-centric video streaming service that offers a vast library of TV shows, and movies, delivering a seamless, and personalized viewing experience across multiple platforms on subscription basis.


# Agenda
This document aims to develop the high level design of the said system, while describing the principles of high level design.


# What is System Design?
System design is the process of defining the architecture, components, modules, and interfaces of a software system to ensure it meets the specified requirements. It involves breaking a complex system down into smaller, manageable parts while considering factors like performance, scalability, maintainability, and security.

### Key aspects of system design
- Architectural patterns: Selecting appropriate architectural styles (e.g., layered, microservices, event-driven) based on the system's requirements and goals.
- Component design: Designing individual components or modules within the system, defining their responsibilities and interactions.
- Data flow: Modeling how data flows through the system, including input, processing, and output.
- Interface design: Specifying how components communicate with each other, including the data exchanged and the protocols used.
- Non-functional requirements: Considering factors like performance, scalability, security, and maintainability during the design process.

### Phases in system design
System design is typically performed in 2 phases,
1. High level design (HLD): Provides a conceptual averview of the system's architecture, focusing on the major components and their interactions.
2. Low level design (LLD): Defines the detailed design of individual components, including data structures, algorithms, and interfaces.

### How to select the appropriate architectural pattern for the system?
The concept of logical separation is used to achieve this. Logical separation in system design refers to the process of dividing a system into distinct functional units or modules based on their logical relationships and responsibilities. This separation helps to,
- Improve modularity: Each module can be developed, tested, and maintained independently, enhancing code organization and reusability.
- Enhance maintainability: Changes to one module are less likely to impact other parts of the system, reducing the risk of unintended side effects.
- Promote reusability: Well-defined modules can be reused in other projects, saving development time and effort.
- Improve understandability: The system becomes easier to understand and reason about when it is logically separated into cohesive units.

Common techniques for logical separation are,
- Layered architecture: The system is divided into layers based on their logical functions, such as presentation, business logic, and data access. Each layer is responsible for specific tasks, promoting separation of concerns and improving maintainability.
- Microservices architecture: The system is broken down into small, independently deployable services, each focused on a specific business capability. This approach emphasizes logical separation and enables scalability and flexibility.
- Component based architecture: The system is built from reusable components that provide specific functionalities. These components are designed to be independent and can be combined in different ways to create various applications, promoting logical separation and code reuse.


# What is High Level Design?
High level design (HLD) is a conceptual representation of a software system's architecture, focusing on the overall structure, components, and their interactions. It provides a blueprint for the system's design, outlining the key modules, their responsibilities, and how they communicate with each other.

HLD serves as a foundation for the detailed design phase, providing a clear direction for the development team. It helps in,
- Understanding the system as a whole.
- Identifying dependencies between different modules.
- Evaluating different architectural design alternatives.
- Communicating design decisions with all the stake holders.

HLD is essentially a bridge between the problem domain and the detailed design. It helps in laying down a roadmap for building a robust and efficient software system

### Key elements of HLD
- System architecture: The overall structure and organization of the system, often depicted using diagrams like UML (Unified Modeling Language) component diagrams.
- Module identification: Breaking down the system into logical components or modules, each with a specifci purpose.
- Module relationships: Defining how modules interact with each other, including data flow and control flow.
- Interfaces: Specifying the communication points between modules including the data exchanged and the protocols used.
- Non-functional requirements: Considering factors like performance, security, scalability, and maintainability.


# Functional Requirements of a Video Streaming Platform

### Content library
- Extensive catalog of movies, TV shows, docuseries, and other video content.
- Ability to categorize content by genre, release year, rating, and other relevant criteria.
- Support for different languages and subtitles.

### User profiles
- Allow users to create personalized profiles with viewing history, recommendations, and watchlists.
- Support for multiple profiles within a single account.

### Video playback
- High-quality video playback with adaptive streaming to adjust to varying network connections.
- Support for multiple resolutions and frame rates.
- Ability to pause, resume, rewind and fast-forward videos.

### Search and discovery
- Efficient search functionality to find specific content.
- Personalized recommendations based on viewing history and preferences.
- Curated collections and playlists.

### Offline viewing
- Support to download content for offline viewing on compatible devices.

### Social features
- Users should have an option to like, comment, and rate content.
- Social sharing options to share content with friends and family.

### Payment support
- Support should be available for most of the popular payment methods (Debit Card, Credit Card, UPI, etc.).

### Parental controls
- Restricted profiles to limit content access for childern.
- PIN protection for parental controls.

### Multi-device support
- Compatibility with various devices, including smartphones, tablets, computers, and smart TVs.


# Non-Functional Requirements for a Video Streaming Platform
Non-functional requirements (NFRs) define the quality attribute of a system, ensuring it meets user expectations and operates effectively.

### Performance
- Response time: Ensure quick response times for user actions, such as searching, playing and pausing videos.
- Throughput: Handle a large number of concurrent users and streams without significant degradation in performance.
- Scalability: The system should be able to scale up or down to accomodate changes in user demand.
- Buffering: Minimize buffering during video playback, especially over slower etwork connections.

### Reliability
- Uptime: Maintain high availability and minimize downtime.
- Data integrity: Ensure data consistency and accuracy, including user profiles, viewing history, and content metadata.
- Error handling: Implement robust error handling mechanisms to gracefully handle exceptions and prevent system crashes.

### Security
- Data privacy: Protect user data, including personal information and viewing history from unauthorized access.
- Content protection: Prevent unauthorized copying, distribution or privacy of content.
- Secure authentication: Implement secure authentication and authorization mechanisms to protect user accounts.
- Compliance: Adhere to relevant data privacy regulations (e.g., GDPR, CCPA).

### Usability
- User interface: Design an intuitive and user-friendly interface that is easy to navigate.
- Accessibility: Ensure the platform is accessible to users with disabilities.
- Localization: Support multiple languages and regions to cater to a global audience.

### Maintainability:
- Modularity: Design the system with well-defined modules to facilitate maintenance and updates.
- Documentation: Provide comprehensive documentation for developers and administrators.
- Testability: Ensure the system is testable with automated testing tools and frameworks.

### Cost
- Cost-effectiveness: Optimize resource utilization and minimize operational costs.
- Scalability: The system should be scalable to accommodate growth without excessive cost.


# Assumptions About the Video Streaming Platform
1. The platform has atleast 1 billion users, and out of those atleast 200 million are active users.
2. The has atleast 1 million videos.
3. The platform sees atleast 1000 videos being uploaded everyday.
4. The platform witnesses at least 1 billion requests per day (12000 requests per day).


# Data Model (ER Diagram) for the Video Streaming Platform
The following is a mock ER diagram showing the different possible entities that a database of a video streaming platform can have,

```mermaid
erDiagram
    a["Users"] {
        int user_id
        string user_name
        string user_email
        string address
        int phone_number
        string password
        datetime joined_date
        int plan_id
        bool is_active
        int payment_id
    }
    b["Shows"] {
        int show_id
        string show_description
        string show_type
        int genre_id
        int length
        datetime release_date
        bool is_downloadable
        bool subtitle_available 
        bool audio_description_available
    }
    c["Sessions"] {
        int session_id
        int user_id
        int show_id
        int device_id
        datetime playback_start_timestamp
        datetime playback_end_timestamp
        datetime paused_time
        datetime session_time
        datetime pause_time
    }
    d["Genre"] {
        int genre_id
        string genre_type
        bool is_active
    }
    e["Devices"] {
        int device_id
        string device_type
        bool is_active
    }
    f["Plans"] {
        int plan_id
        string plan_name
        int streaming_limit
        int plan_base_rate
        datetime plan_start_date
        bool is_active
    }
    g["Payments"] {
        int payment_id
        int user_id
        datetime payment_date
        string payment_method
        int total_amount
        int transaction_id
        bool payment_status
    }
    a ||--|{ c : "can have"
    a ||--|{ g : "can make"
    b ||--|{ c : "can have"
    e ||--|{ c : "can have"
    f ||--|{ a : "can be assigned"
    d }|--|{ b : "can have"
    a ||--|{ e : "can own"
```

An ER (Entity-Relationship) diagram shows the different entities in a database and the relationship between them.


# What is a Database?
When designing a video streaming platform, the choice of database system is crucial for efficiently storing and managing large amounts of data, handling real-time operations, and scaling to meed growing user demands. There are 2 primary categories of databases,
1. SQL (Relational)
2. NoSQL (Non-Relational)

### SQL databases
SQL databases, like MySQL, PostgreSQL, and Oracle, are well-suited for structured data with defined schemas. They organize data into tables with rows and columns, enforcing relationships between data elements through primary and foreign keys.

Advantages of SQL databases,
- Structured data: Ideal for storing well-defined data with clear relationships.
- ACID properties: Ensure data integrity and consistency through atomicity, consistency, isolation and durability.
- Query language: Powerful SQL language for querying, manipulating, and analyzing data.
- Maturity: Well established and mature technology with extensive tooling and support.

Potential challenges for video streaming,
- Schema rigidity: Can be less flexible for handling rapidly evolving data structures or unstructured data.
- Performance: May face performance bottlenecks when dealing with large datasets and high-concurrency workloads.

### NoSQL databases
NoSQL databases, like MongoDB, Cassandra, and Redis, are designed to handle unstructured or semi-stuctured data that doesn't fit well into a traditional relational schema. They offer flexible data models, horizontal scalability, and high performance.

Advantages of NoSQL databases,
- Flexible data models: Accommodate a variety of data structures, including key-value pairs, document-oriented, columnar, and graph databases.
- Scalability: Can scale horizontally to handle large datasets and high-concurrency workloads.
- Performance: Often provide better performance for certain use cases, such as real-time data processing and analytics.
- Schema flexibility: Allow for schema evolution without downtime.

Potential challenges for video streaming,
- Data consistency: May require additional measures to ensure data consistency and integrity, especially in distributed environments.
- Complexity: Can be more complex to manage and query compared to SQL databases.

### How to choose the right database?
The optimal choice between SQL and NoSQL databases depends on the specific requirements of the video streaming platform. The following point can be considered during deciding the database type for the platform,
- Data structure: If the data is highly structured and predictable, SQL databases might be suitable.
- Scalability: For handling large datasets and high-concurrency, NoSQL databases can offer advantages.
- Performance: The choice between SQL and NoSQL can impact performance based on specific workloads and query patterns.
- Flexibility: If the data structure is likely to evolve or contain unstructured elements, NoSQL databases might be more flexible.
 
In many cases, a hybrid approach combining SQL and NoSQL databases can be beneficial. For example, SQL databases can be used for storing structured metadata about users, videos, and plans, while NoSQL database can handle real-time data like viewing history, recommendations, and analytics.

### What are the other options other than databases?
1. File Systems:
    - Local File Systems: Data is stored on a physical disk or storage device.
    - Network File Systems (NFS): Data is shared across a network.
    - Distributed File Systems (DFS): Data is distributed across multiple servers for scalability and fault tolerance.
2. Databases:
    - Relational Databases: Data is organized into tables with rows and columns, enforcing relationships between data elements.
    - NoSQL Databases: Designed to handle unstructured or semi-structured data, offering flexible data models and scalability.
3. Object Storage:
    - Stores data as individual objects, each with a unique key and metadata.
    - Suitable for storing large amounts of unstructured data, such as images, videos, and documents.
4. Cloud Storage:
    - Data is stored on remote servers managed by a cloud provider.
    - Offers scalability, durability, and cost-effectiveness.
5. In-Memory Databases:
    - Data is stored in the computer's main memory for faster access.
    - Suitable for real-time applications with high performance requirements.
6. Distributed Data Stores:
    - Data is distributed across multiple nodes for scalability and fault tolerance.
    - Examples include Apache Cassandra, Apache HBase, and Riak.
7. Data Warehouses:
    - Specialized databases designed for storing and analyzing large amounts of historical data.
    - Used for business intelligence and reporting.
8. Data Lakes:
    - Unstructured data storage repositories that can store any type of data in its raw format.
    - Used for data exploration, machine learning, and big data analytics.


# What is Object Storage?
Object storage is a type of data storage that stores data as individual objects, each identified by a unique key and associated metadata. This differs from traditional file systems, which store data in a hierarchical structure of folders and files.

### Key characteristics of object storage
- Object-based: Data is stored as individual objects, each with a unique identifier (key) and metadata (information about the object).
- Scalability: Object storage systems can scale to store massive amounts of data without requiring significant infrastructure changes.
- Durability: Data is replicated across multiple data centers to ensure high durability and availability.
- Cost-effective: Object storage is often more cost-effective than traditional file systems for storing large amounts of data.
- Metadata: Metadata associated with each object provides information about the data, such as content type, size, and access permissions.

### Common use cases for object storage
- Data backup and archiving: Storing backups of critical data and long-term archives.
- Content delivery: Distributing large files and content to users worldwide.
- Big data analytics: Storing and processing large datasets for analytics purposes.
- IoT applications: Storing data from IoT devices.
- Media and entertainment: Storing and managing large media files.

### Examples of object storage services
- Amazon S3: A popular object storage service offered by Amazon Web Services.
- Google Cloud Storage: Object storage from Google Cloud Platform.
- Microsoft Azure Blob Storage: Object storage service offered by Microsoft Azure.


# How to Deal with the Computational Requirements of a Video Streaming Platform?
As the load increases, there would certainly be an increase in computational requirements by the platform.

The computational requirement can be met in 2 ways,
1. Increase the resources (RAM and CPU) of the existing machine. This is called "Vertical Scaling".
2. Add an additional machine to the existing, such that the load is shared by both the machine (old + new). This is called "Horizontal scaling".

![alt text](images/scaling.png)

### Vertical Scaling
- Upgrading hardware: Involves upgrading the hardware components of a single server, such as increasing CPU cores, RAM, or storage capacity.
- Increased capacity: A single server becomes more powerful.
- Benefits: Simplicity, potentially better performance for certain workloads.
- Limitations: Can be expensive and may reach hardware limits.

### Horizontal Scaling
- Adding more servers: Involves adding more servers to a cluster or distributed system.
- Increased capacity: Each additional server provides additional processing power, memory, and storage.
- Benefits: Scalability, fault tolerance, cost-effectiveness (in some cases).
- Example: A web application can be horizontally scaled by adding more web servers to handle increased traffic.

### How to choose the right scaling strategy?
This depends on the following factors,
- Workload: The nature of the workload (e.g., CPU-intensive, I/O-bound) can influence the most effective scaling approach.
- Cost: Horizontal scaling can be more cost-effective in the long run, especially for large-scale systems.
- Complexity: Vertical scaling is generally simpler to manage, while horizontal scaling can introduce additional complexity.
- Technology constraints: The underlying technology and infrastructure may limit the options for scaling.


# Using AWS for Computation and Orchestration
AWS by far is the most used and easy to understand cloud services in comparison to its competitors. AWS offers a robust suite of services that can be used for various computational and orchestration tasks.

### Computation
- E2C (Elastic Compute Cloud): Provides virtual machines (instances) that can be used for a wide range of computational tasks. You can choose from different instance types based on your needs (e.g., CPU-intensive, memory-intensive, GPU-intensive).
- Lambda: A serverless computing platform that lets you run code without provisioning or managing servers. It's ideal for event-driven applications and microservices.
- Fargate: A serverless compute engine for containers that abstracts away the infrastructure management. It's used in conjunction with ECS or EKS.

### Orchestration
- ECS (Elastic Container Service): A highly scalable service for running and managing containers. It offers two deployment models: Fargate and EC2.
- EKS (Elastic Kubernetes Service): A managed Kubernetes service that simplifies the deployment, management, and scaling of containerized applications.
- Batch: A fully managed batch computing service that helps you run large-scale batch jobs efficiently.

### Storage services
- S3 (Simple Storage Service): A highly scalable and durable object storage service that can be used to store data for your computational tasks.
- RDS (Relational Database Service): Provides managed relational databases (e.g., MySQL, PostgreSQL, Oracle) for your applications.
- DynamoDB: A fully managed NoSQL database service that offers high performance and scalability.

### Use cases
- Data processing: Using EC2 instances or Lambda functions to process large datasets.
- Machine learning: Training and deploying machine learning models on EC2 instances or using managed services like SageMaker.
- Web applications: Running web applications on EC2 instances or using serverless options like Lambda and API Gateway.
- Microservices architecture: Orchestrating microservices using ECS or EKS.
- Batch processing: Running batch jobs using AWS Batch.

### How to deal with the complexity of orchestrating workflows and batch processing?
AWS step functions is a serverless workflow service that helps to coordinate and automate complex distribution applications. It helps in building state machines, which are visual diagrams that define the sequence of steps required to complete a process. Each step in a state machine can be a Lambda function, an AWS task or a custom activity.


# How to Handle the Storage and Delivery of the Video Content?
When dealing with video content, efficient storage and delivery are crucial for providing a smooth user experience. There are 2 ways in which the content can be stored and delivered to the viewers,
1. Pre-Transcoding and Storage:
    - Pre-transcoding: This approach involves creating multiple versions of the video in different resolutions beforehand.
    - Storage: Each pre-transcoded version can be stored in a single location or distributed across multiple locations for redundancy and performance.
    - Pros:
        - Faster delivery: Pre-transcoded videos can be delivered directly to the user without additional processing.
        - Reduced server load: Pre-transcoding can offload the processing burden from servers during peak usage.
    - Cons:
        - Storage overhead: Storing multiple versions of each video can consume significant storage space.
        - Maintenance: Managing and updating multiple versions can be complex.
2. On-The-Fly Transcoding
    - Transcoding: The video is converted to the required resolution and format in real-time based on user device and network conditions.
    - Storage: Only the original video needs to be stored.
    - Pros:
        - Storage efficiency: Only one version of the video needs to be stored.
        - Flexibility: Can adapt to changing user preferences and network conditions.
    - Cons:
        - Higher server load: Transcoding can be computationally intensive, especially for high-resolution videos.
        - Potential latency: Transcoding may introduce latency, especially for slower networks or older devices.


The following are some additional strategies that can be considered,

### Storage
- Cloud storage:
    - S3 (Simple Storage Service): AWS's popular object storage service offers high durability, scalability, and cost-effectiveness for storing video files.
    - Azure Blob Storage: Microsoft's equivalent to S3 provides similar features and integrates well with other Azure services.
    - Google Cloud Storage: Google's cloud storage solution offers high performance and global reach.
- Content Delivery Network (CDN):
    - CDNs cache video content closer to end users, reducing latency and improving delivery speeds.
    - Popular CDNs include Cloudflare, Akamai, and Fastly.
- Hybrid Storage:
    - Combine cloud storage with on-premises storage for a hybrid approach, balancing cost, performance, and data sovereignty.

### Delivery
- Streaming Protocols:
    - HTTP Live Streaming (HLS): Apple's adaptive bitrate streaming protocol, widely supported by various devices and platforms.
    - Dynamic Adaptive Streaming over HTTP (DASH): A flexible and efficient streaming protocol supported by major browsers and devices.
    - Progressive Downloading: Suitable for shorter videos or offline viewing, where the entire video is downloaded before playback.
- Transcoding:
    - Convert video files into different formats and resolutions to optimize delivery for various devices and network conditions.
    - Consider using cloud-based transcoding services like AWS Elemental MediaConvert or Azure Media Services.
- Caching:
    - Implement caching at different levels (CDN, server, browser) to reduce load on storage and improve delivery speeds.
- Quality of Service (QoS):
    - Implement mechanisms to ensure consistent video quality and playback experience, even during periods of high traffic or network congestion.
- DRM (Digital Rights Management):
    - Protect your video content from unauthorized access and distribution using DRM technologies.
    - Popular DRM solutions include Widevine, FairPlay, and PlayReady.

### Additional Considerations
- Metadata: Store metadata (e.g., title, description, tags) with your video content to enable search, indexing, and recommendations.
- Analytics: Track video usage metrics (e.g., views, watch time, completion rates) to understand audience behavior and optimize content delivery.
- Security: Implement robust security measures to protect your video content from unauthorized access and breaches.
- Redundancy: Create backups of your video content to ensure data durability and disaster recovery.


# How Video Streaming Works?
Video streaming is a technology that allows users to watch videos in real-time over the internet without having to download the entire file first. This is achieved through a combination of techniques that optimize data delivery and playback.

### Key steps invlved in video streaming
1. Encoding:
    - The original video file is converted into a format suitable for streaming, often using codecs like H.264 or VP9.
    - The video is typically divided into smaller segments (chunks) to facilitate streaming.
    - Adaptive bitrate streaming (ABS) techniques may be used to create multiple versions of the video at different resolutions and bitrates, allowing the player to adjust the quality based on network conditions.
2. Storage:
    - The encoded video segments are stored on a server or a content delivery network (CDN).
    - CDNs distribute the content across multiple servers worldwide, reducing latency and improving delivery speeds.
3. Delivery:
    - When a user requests a video, the streaming server sends the initial video segment.
    - As the user watches the video, subsequent segments are sent in real-time.
    - Adaptive bitrate streaming algorithms dynamically adjust the resolution and bitrate of the video based on the user's network bandwidth and device capabilities.
4. Playback:
    - The user's device (e.g., computer, smartphone, tablet) receives the video segments and decodes them into a playable format.
    - The video is displayed on the screen, with the playback rate synchronized with the incoming data.

### Key technologies and protocols involved in video streaming
- HTTP Live Streaming (HLS): A widely used protocol for adaptive bitrate streaming, developed by Apple.
- Dynamic Adaptive Streaming over HTTP (DASH): Another popular protocol for adaptive bitrate streaming, supported by major browsers and devices.
- Progressive Downloading: A simpler method where the entire video is downloaded before playback, suitable for shorter videos or offline viewing.
- Content Delivery Networks (CDNs): Distribute video content closer to end users, reducing latency and improving delivery speeds.
- Transcoding: Converting video files into different formats and resolutions to optimize delivery for various devices and network conditions.


# How is Content Recommended to the Users on Video Streaming Platform?
A combination of content based filtering and collaborative filtering recommender systems can be built to address this.

Check out the following link to have an in-depth understanding of Recommender Systems are built. Link: https://github.com/vidishsirdesai/dsml_end_to_end_reference/blob/main/rec_sys/rec_sys.ipynb.