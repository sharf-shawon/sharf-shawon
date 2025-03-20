---
layout: "page"
title: "Contact Me"
description: "Get in touch with me for collaboration, inquiries, or professional opportunities."
tags: ["contact", "software engineer", "full stack developer"]
seo_keywords: "Sharfuddin Shawon, Portfolio, Contact, Software Engineer, Full Stack Developer"
ShowShareButtons: false
hideMeta: true
hideDescription: true
hideTags: true
disableShare: true
# canonicalURL: 'https://shawon.me/posts/{{ replace .File.ContentBaseName "-" " " | title }}'
# aliases: ["/{{ .Slug }}"]
# slug: "{{ .Slug }}"
# cover:
#     image: "<image path/url>" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
---
I’m always excited to hear from you, whether you have a project in mind, need advice, or just want to chat about tech. Feel free to reach out using the form below, and I’ll get back to you as soon as I can!

## How Can I Help?
- **Collaboration**: Interested in working together on a project? Let’s talk!
- **Inquiries**: Have a question or want to learn more about my work? Ask away!
- **Feedback**: I’d love to hear your thoughts on my portfolio website.

Drop me a message, and I’ll be in touch soon!

## Let's Connect!

{{< rawhtml >}}
<link rel="stylesheet" href="https://s.pageclip.co/v1/pageclip.css" media="screen">

<style>
    .contact-form-container {
        max-width: 800px;
        margin: 0 auto;
        padding: 1.5rem;
        position: relative;
    }

    .form-group {
        margin-bottom: 1.5rem;
    }

    label {
        display: block;
        margin-bottom: 0.5rem;
        color: var(--primary);
        font-weight: 500;
    }

    .form-input {
        width: 100%;
        padding: 0.4rem;
        border: 1px solid var(--border);
        border-radius: 4px;
        background-color: var(--entry);
        color: var(--primary);
        transition: border-color 0.3s ease;
    }

    .form-input:focus {
        border-color: var(--primary);
        outline: none;
    }

    .form-submit {
        background-color: var(--code-bg);
        color: var(--primary);
        padding: 0.5rem 2rem;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: all 0.3s ease;
        display: flex;
        align-items: center;
        gap: 0.5rem;
    }

    .form-submit:hover {
        opacity: 0.9;
        transform: scale(1.02);
    }

    .form-messages {
        margin-top: 1rem;
        text-align: center;
    }

    .success-message,
    .error-message {
        padding: 1rem;
        border-radius: 4px;
        display: none;
        opacity: 0;
        transform: translateY(-10px);
        transition: opacity 0.5s ease, transform 0.5s ease;
    }

    .success-message {
        background-color: var(--code-bg);
        color: var(--primary);
        border: 1px solid var(--border);
    }

    .error-message {
        background-color: #ffe3e3;
        color: #c92a2a;
        border: 1px solid #ffc9c9;
    }

    @media (prefers-color-scheme: dark) {
        .error-message {
            background-color: #2b0b0b;
            color: #ff8787;
            border-color: #862e2e;
        }
    }

    .pageclip-form__submit:disabled {
        opacity: 0.7;
        cursor: not-allowed;
    }

    .fade-out {
        opacity: 0;
        transform: translateY(-50px);
        transition: opacity 2s ease, transform 2s ease;
    }

    .fade-in {
        opacity: 1 !important;
        transform: translateY(0) !important;
        transition: opacity 2s ease, transform 2s ease;
    }
</style>

<section class="contact-form-container">
    <form action="https://send.pageclip.co/iJNdBLUjsnlzNR2XTcYk7dEKT1VBKJ8Y/ContactForm" 
        class="pageclip-form" method="post">
        <div class="form-group">
            <label for="name">Name</label>
            <input type="text" id="name" name="name" required class="form-input">
        </div>
        <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" name="email" required class="form-input">
        </div>
        <div class="form-group">
            <label for="subject">Subject</label>
            <input type="text" id="subject" name="subject" required class="form-input">
        </div>
        <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" name="message" rows="5" required class="form-input"></textarea>
        </div>
        <input type="hidden" id="x_source_url" name="x_source_url" value="" >
        <button type="submit" class="pageclip-form__submit form-submit">
            <span>Send Message</span>
        </button>
    </form>
    <div class="form-messages">
        <div class="success-message">
            Thank you. 🎉
            <br>
            Your message has been sent successfully!
        </div>
        <div class="error-message">Error sending message. Please try again.</div>
    </div>
</section>

<script src="https://s.pageclip.co/v1/pageclip.js" charset="utf-8"></script>
<script>
    document.addEventListener("DOMContentLoaded", function () {
        // Set the x_source_url field to the current URL
        document.getElementById('x_source_url').value = window.location.href;
        
        var form = document.querySelector('.pageclip-form');
        var successMessage = document.querySelector('.success-message');
        var errorMessage = document.querySelector('.error-message');
        Pageclip.form(form, {
            onSubmit: function () {
                },
            onResponse: function (error, response) {
                form.classList.add('fade-out');
                form.style.display = "none";
                if (error) {
                    errorMessage.style.display = "block";
                    errorMessage.classList.add('fade-in');
                    form.classList.remove('fade-out');
                    form.style.display = "block";
                    form.classList.add('fade-in');
 
                } else {
                    setTimeout(() => {
                        successMessage.style.display = "block";
                        successMessage.classList.add('fade-in');
                    }, 100);
                }
            }
        });
    });
</script>
{{< /rawhtml >}}
