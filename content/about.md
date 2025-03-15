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
<section class="certifications">
    <h2>My Certifications</h2>
    <div id="certifications-container" class="certifications-grid">
        <!-- Certifications loaded here dynamically -->
    </div>
</section>

<style>
.certifications-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    grid-auto-rows: 1fr; /* Ensure equal row heights */
    gap: 1rem;
    margin-top: 1rem;
}

.certification-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0.75rem;
    border: 1px solid var(--border);
    border-radius: 8px;
    background-color: var(--entry);
    transition: transform 0.3s ease;
    min-height: 200px; /* Set minimum height for all cards */
}

.certification-card:hover {
    transform: translateY(-2px);
}

.cert-badge {
    width: 100%;
    height: 120px; /* Fixed height for image container */
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 0.5rem;
}

.cert-badge img {
    width: auto;
    max-width: 100%;
    height: auto;
    max-height: 100px;
    object-fit: contain;
    border-radius: 4px;
}

.cert-text {
    flex: 1;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
}

.cert-title {
    font-size: 0.9rem;
    font-weight: 500;
    text-align: center;
    margin: 0;
    line-height: 1.3;
    display: -webkit-box;
    -webkit-line-clamp: 3; /* Limit to 3 lines */
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
}

.cert-date {
    font-size: 0.75rem;
    text-align: center;
    margin: 0.5rem 0 0 0;
    color: var(--secondary);
}

@media (max-width: 768px) {
    .certifications-grid {
        grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
    }
    
    .certification-card {
        min-height: 180px;
        padding: 0.5rem;
    }
    
    .cert-badge {
        height: 100px;
    }
    
    .cert-badge img {
        max-height: 80px;
    }
    
    .cert-title {
        font-size: 0.8rem;
        -webkit-line-clamp: 2;
    }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const container = document.querySelector('.certifications-grid');
    
    fetch('https://pocketbase.shawon.me/api/collections/certifications/records')
        .then(response => response.json())
        .then(data => {
            if (!data.items || data.items.length === 0) {
                container.innerHTML = "<p>No certifications found.</p>";
                return;
            }

            data.items.forEach(cert => {
                const card = document.createElement('article');
                card.className = 'certification-card';

                const badgeUrl = `https://pocketbase.shawon.me/api/files/${cert.collectionId}/${cert.id}/${cert.badge}?thumb=0x100`;

                const earnedDate = new Date(cert.earned_on);
                const formattedDate = earnedDate.toLocaleDateString('en-US', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric'
                });

                card.innerHTML = `
                    <a href="${cert.url}" target="_blank" rel="noopener" class="cert-badge"
                    title="Certified by ${cert.organization}">
                        <img src="${badgeUrl}" alt="${cert.name} badge">
                    </a>
                    <div class="cert-text">
                        <h3 class="cert-title">${cert.name}</h3>
                        <small class="cert-date">${formattedDate}</small>
                    </div>
                `;

                container.appendChild(card);
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