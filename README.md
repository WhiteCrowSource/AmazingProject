# AmazingProject
https://blog.devgenius.io/11-open-source-saas-killer-selfhost-with-docker-034456653568
用 Docker 自托管 Supabase, Grafana, Uptime Kuma, NocoDB, Dokku, Appwrite, N8N, Redash, Jitsi, Plausible and Nextcloud.SaaS（软件即服务）模式允许用户在线访问软件而无需下载。这是一种基于租赁的模式，即按使用付费，并且您可以随时停止使用。11 个爆款开源 SaaS 在本文中，我们将看到您可以使用的 11 种顶级付费 SaaS 产品的替代品。您只需要一台在云端运行的服务器，在那里您可以托管您的 SaaS 产品。我希望您已经有了；如果没有，您可以使用 ASW、GCP 或 DigitalOcean 进行托管。您可以按照下面的教程在 AWS 中设置 EC2 实例。一旦设置完成，您可以通过 SSH 连接到您的实例并安装您想要的软件。让我们来看看热门 SaaS 产品的替代品——1. Supabase — The…Supabase您可以开始使用 Supabase 来替代 Firebase，它提供了 Firebase 所提供的一切。如果您不想托管，您可以选择自托管模式或其云服务。Supabase欲了解更多信息，请参考 GitHub—— https://github.com/supabase/supabase如何使用 Docker 安装 Supabase——# Get the code
git clone --depth 1 https://github.com/supabase/supabase

# Go to the docker folder
cd supabase/docker

# Copy the fake env vars
cp .env.example .env

# Pull the latest images
docker compose pull

# Start the services (in detached mode)
docker compose up -d2. Grafana——Datadog、NewRelic 的开源替代品GrafanaGrafana 是一个用于数据可视化的平台，允许用户查看来自许多不同来源的指标、日志和跟踪，包括 Prometheus、Loki、Elasticsearch、InfluxDB、Postgres 等等。上传失败，网络异常。重试Github
如何使用 Docker 安装 Grafana——docker run -d -p 3000:3000 --name=grafana grafana/grafana-enterprise更多细节请参考这里https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/
3. Uptime Kuma——Uptime Robot 的开源替代品Uptime Kuma DashboardUptime kuma 是 Uptime Robot 的绝佳替代品，Uptime Robot 是一款用于监测您网站正常运行时间的付费软件。我们可以在我们的服务器上托管 Uptime kuma，并开始使用其出色的功能，没有任何限制。Github如何使用 Docker 安装 Uptime kuma——docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1演示链接https://demo.kuma.pet/start-demo
4. NocoDB——Airtable 的开源替代品NocoDB 是一个无需编码即可开始使用您的数据库的绝佳替代品。它将您的数据库用作电子表格，您可以在其中添加、编辑记录。使用 Docker 安装 NocoDB —# with PostgreSQL
docker run -d --name nocodb-postgres \
-v "$(pwd)"/nocodb:/usr/app/data/ \
-p 8080:8080 \
-e NC_DB="pg://host.docker.internal:5432?u=root&p=password&d=d1" \
-e NC_AUTH_JWT_SECRET="569a1821-0a93-45e8-87ab-eb857f20a010" \
nocodb/nocodb:latest

--------------------------------------------------------

# with SQLite : mounting volume `/usr/app/data/` is crucial to avoid data loss.
docker run -d --name nocodb \
-v "$(pwd)"/nocodb:/usr/app/data/ \
-p 8080:8080 \
nocodb/nocodb:latest5. Dokku——Heroku、Render 的开源替代品Dokku 是基于 Docker 的 PaaS（平台即服务）产品，可用作 Heroku、Render 的替代品来部署您的应用程序。它会自动从应用程序代码中检测技术，并通过 GitHub 提供 CI/CD（持续集成/持续部署）。Github安装教程：https://dokku.com/docs/getting-started/installation/# for debian systems, installs Dokku via apt-get
wget -NP . https://dokku.com/install/v0.34.8/bootstrap.sh
sudo DOKKU_TAG=v0.34.8 bash bootstrap.sh6. Appwrite——Firebase 的开源替代品Appwrite DashboardAppwrite 是 Firebase 的另一个不错的选择，它提供了 SDK 和 API，可在几分钟内将您的应用连接到后端。它有自托管和基于云的模式。Github使用 Docker 安装 Appwrite —docker run -it --rm \
    --volume /var/run/docker.sock:/var/run/docker.sock \
    --volume "$(pwd)"/appwrite:/usr/src/code/appwrite:rw \
    --entrypoint="install" \
    appwrite/appwrite:1.5.107. n8n——Zapier、Make 的开源替代品n8n 工作流具有公平代码许可的工作流自动化解决方案，它是免费和开源的。轻松跨多个服务实现任务自动化。Github使用 Docker 安装 n8n —docker volume create n8n_data

docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n8. Redash：Power BI、tableau、MicroStrategy、Qlik 的开源替代品Redash利用数据组织您的业务。创建仪表板、共享您的数据，并轻松连接到任何数据源。Github使用 Docker 安装 Redash —git clone https://github.com/getredash/redash.git
cd redash
cp .env.example .env

docker-compose -f docker-compose.production.yml up -d9: Jitsi——Zoom、Skype 的开源替代品Jitsi您可以使用 Jitsi Meet——一款安全、用户友好且可扩展的视频会议应用程序——作为独立程序，或者将其集成到您的网站中。Github使用 Docker 安装 Jitsi —// Download
wget $(curl -s https://api.github.com/repos/jitsi/docker-jitsi-meet/releases/latest | grep 'zip' | cut -d\" -f4)

// Unzip the package
unzip <filename>

// Create a .env file by copying and adjusting env.example
cp env.example .env

// Set strong passwords in the security section options of .env file by running the following bash script
./gen-passwords.sh

// Create required CONFIG directories
mkdir -p ~/.jitsi-meet-cfg/{web,transcripts,prosody/config,prosody/prosody-plugins-custom,jicofo,jvb,jigasi,jibri}

// run docker
docker compose up -d

//Access the web UI at https://localhost:8443 (or a different port, in case you edited the .env file).
查看官方文档以获取更多详细信息https://jitsi.github.io/handbook/docs/devops-guide/devops-guide-docker
10. Plausible Analytics——Google Analytics 的开源替代品Plausible Analytics一个不麻烦、开源、小型（< 1 KB）且私密的在线分析工具，可替代 Google Analytics。Github使用 Docker 安装 Plausible Analytics —git clone https://github.com/plausible/community-edition

cd community-edition编辑 `plausible-conf.env`BASE_URL=replace-me
SECRET_KEY_BASE=replace-me
TOTP_VAULT_KEY=replace-me运行 docker composedocker compose up -d11. NextCloud——Google Drive 的开源替代品NextcloudNextcloud 是 Google Drive 的开源替代品，用于在用户之间存储和共享数据。Github使用 Docker 安装 Nextcloud —$ docker run -d \
-v nextcloud:/var/www/html \
