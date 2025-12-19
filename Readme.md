🐳 WordPress Two-Tier Deployment Using Docker on AWS EC2
=
📘 Project Overview
=
This project showcases how Docker revolutionizes the deployment process of a two-tier WordPress application — comprising WordPress as the frontend (web tier) and MySQL as the backend (database tier).

Initially, the same setup was deployed manually, which involved complex, time-consuming steps like package installation, configuration, and troubleshooting. Later, the Dockerized version achieved the same outcome with just two simple commands and minimal setup time — all within minutes.

.

🏗 Traditional (Manual) Deployment Approach
=
Before Docker, deploying WordPress involved:

1.Provisioning an EC2 instance or any Linux VM

2.Installing and configuring MySQL manually

3.Installing Apache, PHP, and WordPress

4.Setting up permissions, PHP extensions, and virtual hosts

5.Connecting WordPress to the database manually

6.Managing updates and service restarts

❌ Challenges:
=
✅ Lengthy and error-prone process

✅ Version compatibility issues between PHP/MySQL

✅High maintenance effort

✅ Not easily replicable across environments


🚀 Dockerized Deployment (Modern Approach)
=
Using Docker, the same setup can be launched in under 2 minutes with only two containers.


🧩 Step 1: Switch to Root User
=
sudo -i

(Avoids adding sudo to every Docker command.)



🐬 Step 2: Deploy MySQL Container
=
docker run -d --name mydb   -e MYSQL_ROOT_PASSWORD=root@123   -e MYSQL_DATABASE=wordpressdb   mysql


Note: The MYSQL_ROOT_PASSWORD variable is mandatory — without it, the container will start and exit immediately.

<img width="1867" height="356" alt="Screenshot 2025-12-13 163351" src="https://github.com/user-attachments/assets/59bbb283-8984-40d1-87a8-c257ca3d066d" />

🌐 Step 3: Deploy WordPress Container
=
docker run -d --name wordpressapp -p 80:80   -e WORDPRESS_DB_HOST=mydb   -e WORDPRESS_DB_USER=root   -e WORDPRESS_DB_PASSWORD=root@123   -e WORDPRESS_DB_NAME=wordpressdb   --link mydb:mysql   wordpress

💡About --link:

✅ Creates a secure bridge between containers (WordPress ↔ MySQL)

✅ Allows automatic hostname resolution between linked containers

✅ Injects environment variables for connectivity

⚠️ While --link works fine for small setups, Docker Networks are preferred for production environments.
<img width="1883" height="608" alt="Screenshot 2025-12-13 163512" src="https://github.com/user-attachments/assets/81a60cec-3191-422e-af0c-8dae637ca302" />

🔍 Step 4: Verify Running Containers
=

docker ps

You should see both mydb (MySQL) and wordpressapp (WordPress) running successfully.
<img width="1238" height="90" alt="Screenshot 2025-12-13 163535" src="https://github.com/user-attachments/assets/f2d2aa32-bef1-49d7-b8ec-4a8a9888774e" />

🌏 Step 5: Access WordPress in Browser
=
Visit:


http:// <EC2-Public-IP>


Complete the initial WordPress setup (language, admin user, password), and you’ll reach the WordPress Dashboard 🎉

<img width="1787" height="839" alt="Screenshot 2025-12-13 163724" src="https://github.com/user-attachments/assets/bb096692-5000-475f-acd8-4848002dcaba" />

📦 Role of Docker Hub
=
Both MySQL and WordPress images were pulled directly from Docker Hub:

1.Ready-to-use, pre-built images maintained by the community

2.Quick, consistent deployments with zero manual setup

3.Reduces dependency errors and setup time

4.Enables seamless updates and version control

<img width="1891" height="895" alt="Screenshot 2025-12-13 164215" src="https://github.com/user-attachments/assets/33c84378-9b6d-4447-8603-c37919ba9d5a" />


🧠 Key Takeaways
=

| Aspect        | Traditional Deployment | Dockerized Deployment        |
|---------------|------------------------|------------------------------|
| Setup Time    | ~30–45 minutes         | < 2 minutes                  |
| Complexity    | High                   | Very Low                     |
| Portability   | Manual migration       | Easily replicable            |
| Consistency   | Prone to errors        | Same environment every time  |
| Maintenance  | Tedious                | Simplified                   |


🏁 Conclusion
=
By containerizing the WordPress + MySQL stack:

✅ Deployment time was drastically reduced.

✅ Configuration became portable and reproducible.

✅ Application updates are simpler and safer.

✅ Docker has completely transformed traditional deployments — turning multi-step setups into a single-line operation.

“What once took hours, now takes minutes — that’s the power of containerization.” 🚀



