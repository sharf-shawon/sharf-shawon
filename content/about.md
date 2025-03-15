---
date: '2025-01-30T19:36:22-06:00'
draft: false
title: 'About Me'
canonicalURL: 'https://shawon.me/about'
---

![Sharfuddin Shawon - Banner](/banner.png)
## Hi, I'm **Sharfuddin Shawon**!

I'm a **Computer Science undergrad** with a passion for **software engineering, artificial intelligence, self-hosting and homelabs**. I love designing **scalable systems**, optimizing performance, and exploring innovative solutions in **big data, networking, and automation**.

---

## 💻 Programming & Development

I specialize in **full stack software development**, focusing on **backend engineering, AI-driven workflows, and distributed systems**. Some of the technologies I frequently work with:

- **Programming Languages:** Python, Java, JavaScript, C++
- **Frameworks & Tools:** Flask, FastAPI, Node.js, Express, Pandas, PySpark, TensorFlow
- **Databases:** PostgreSQL, MySQL, MongoDB, Redis
- **Cloud & DevOps:** Docker, Kubernetes, Nginx Proxy Manager, Apache Hadoop, CI/CD Pipelines

I also enjoy contributing to **open-source projects**, writing **efficient algorithms**, and optimizing systems for **high performance**.

---

{{< rawhtml >}}

<style>

    .certifications-list {
  display: grid;
  gap: 2rem;
  margin-top: 1.5rem;
}

.certification-item {
  display: flex;
  gap: 1.5rem;
  align-items: start;
  padding: 1rem;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
}

.cert-badge img {
  width: 150px;
  height: auto;
  border-radius: 4px;
}

.cert-info {
  flex: 1;
}

.cert-info h3 {
  margin: 0 0 0.5rem 0;
  color: #1e293b;
}

.cert-info p {
  margin: 0.3rem 0;
  color: #64748b;
}

.cert-info a {
  display: inline-block;
  margin-top: 0.8rem;
  color: #3b82f6;
  text-decoration: none;
}
</style>

<section class="certifications">
  <h2>My Certifications</h2>
  <div id="certifications-container" class="certifications-list">
    <!-- Certifications loaded here dynamically -->
  </div>
</section>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const container = document.getElementById('certifications-container');
  
  fetch('https://pocketbase.domain.me/api/collections/certifications/records')
    .then(response => response.json())
    .then(data => {
      if (!data.items || data.items.length === 0) {
        container.innerHTML = "<p>No certifications found.</p>";
        return;
      }

      data.items.forEach(cert => {
        const certElement = document.createElement('div');
        certElement.className = 'certification-item';

        // Badge image with thumbnail
        const badgeUrl = `https://pocketbase.domain.me/api/files/${cert.collectionId}/${cert.id}/${cert.badge}?thumb=150x0`;
        
        // Certificate image
        const certUrl = `https://pocketbase.domain.me/api/files/${cert.collectionId}/${cert.id}/${cert.certificate}`;

        certElement.innerHTML = `
          <a href="${cert.url}" target="_blank" class="cert-badge">
            <img src="${badgeUrl}" alt="${cert.name} badge">
          </a>
          <div class="cert-info">
            <h3>${cert.name}</h3>
            <p><strong>Organization:</strong> ${cert.organization}</p>
            <p><strong>Earned:</strong> ${new Date(cert.earned_on).toLocaleDateString()}</p>
            <a href="${certUrl}" target="_blank">View Certificate</a>
          </div>
        `;

        container.appendChild(certElement);
      });
    })
    .catch(error => {
      console.error('Error:', error);
      container.innerHTML = "<p>Error loading certifications.</p>";
    });
});
</script>

{{< /rawhtml >}}

---
## GitHub Stats

![Github Stats](https://github-readme-streak-stats.herokuapp.com/?user=sharf-shawon&theme=dracula&hide_border=true)

![Most Used Languages](https://github-readme-stats.vercel.app/api/top-langs?username=sharf-shawon&show_icons=true&locale=en&layout=compact&theme=dracula&hide_border=true)

---

## 🏠 Homelab & Self-Hosting

I manage a **hybrid-cloud homelab** with six power-efficient servers across multiple locations, enabling me to **self-host services, experiment with new tech, and optimize network infrastructure**. My homelab, aptly named **Game of Nodes**, features:

- **Virtualized & Containerized Environments** (Proxmox, Docker Swarm, Kubernetes)
- **Encrypted Virtual Overlay Networks** for Secure Communication
- **Cloud & On-Prem Hybrid Infrastructure**
- **Monitoring & Automation** (Prometheus, Grafana, Ansible)

This setup allows me to run critical services efficiently while keeping costs low.

---


## 🚀 Current Projects & Interests

- **Software Engineering Internship (Summer 2025)** – Seeking opportunities to contribute and grow.
- **Machine Learning on Big Data** – Working on **healthcare & fintech** datasets for academic research.

---

## 📫 Get in Touch

I'm always open to new opportunities, collaborations, and tech discussions! Feel free to connect with me:

- **GitHub:** [sharf-shawon](https://github.com/sharf-shawon)
- **LinkedIn:** [in/sharf-shawon](https://www.linkedin.com/in/sharf-shawon/)
- **Email:** [sharf@shawon.me](sharf@shawon.me)