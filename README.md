# CST8915 – Lab 4 Submission (Full-stack Cloud-native Development)

## Student
- Name: Ilyas Zazai
- Course: CST8915 – Full-stack Cloud-native Development
- Lab: Lab 4

---

## Demo Video
- https://www.youtube.com/watch?v=_6O_Qa7-BXs

---

## Reflection Questions
### 1. What are the main differences between a Docker image and a Docker container?
A Docker image is a read-only template that contains everything needed to run an application likr the code, dependencies, libraries, and configuration. A Docker container is the running instance of the image. The image stays unchanged, but the container can run, stop, and create temporary changes while it is executing.

### 2. Explain how Docker's layered architecture improves efficiency.
Docker uses layers to build images where each Dockerfile instruction creates a separate layer. This improves efficiency because Docker can reuse unchanged layers instead of rebuilding the whole image every time. It saves storage space, speeds up the build process, and also makes image sharing faster because only the missing or changed layers need to be downloaded. This is very useful when updating an application because small code changes do not require rebuilding everything from the beginning.

### 3. Why does each container get its own writable layer?
Each container gets its own writable layer so it can make runtime changes without modifying the original image or affecting other containers. This gives isolation between containers, even if they are created from the same image. For example, if one container creates or changes a file, that change stays only inside that container’s writable layer. The other containers continue using the original read-only image layers, which keeps the application more consistent and reliable.

### 4. What are the benefits of using Docker Compose over running containers individually?
Docker Compose makes it easier to manage multi-container applications by defining everything in one `docker-compose.yml` file. Instead of writing many separate `docker run` commands, we can start all services, networks, and volumes together with one command such as `docker compose up -d`. This makes the setup more organized, repeatable, and easier to maintain. It is especially useful for applications that need more than one service, such as a web application connected to Redis or a database.

## Notes About Setup Challenges or Lessons Learned
One important lesson I learned from this lab is that Docker becomes much easier to manage when the commands and structure are understood step by step. I also learned that images, containers, and layers are closely connected, and understanding their roles helps avoid confusion. Another useful point was seeing how Docker Compose simplifies multi-container applications, because managing services in one YAML file is much cleaner than starting each container manually.


