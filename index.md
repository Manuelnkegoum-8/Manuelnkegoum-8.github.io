---
layout: default
title: "About"
---

<section id="about" class="about section">
  <img src="{{ '/assets/images/profile.jpg' | relative_url }}" alt="Profile Picture">
  <div>
    <h1>{{ site.author.name }}</h1>
    <p>PhD Candidate in Computer Vision. My research focuses on <strong>Few-shot Multispectral Object Detection</strong>. My work is supervised by Minh-Tan PHAM (IRISA, Univ. UBS), Sébastien LEFÈVRE (IRISA, Univ. UBS), ÉLisa FROMONT(IRISA, Univ. Rennes) and Bruno AVIGNON (ATERMES, Paris). Based at <em>IRISA, Vannes - FRANCE</em>.</p>

    <p>
      <a href="https://github.com/{{ site.social.github }}" target="_blank">GitHub</a> |
      <a href="https://scholar.google.com/citations?user={{ site.social.scholar_id }}" target="_blank">Google Scholar</a> |
      <a href="https://www.linkedin.com/in/{{ site.social.linkedin }}" target="_blank">LinkedIn</a> |
      <a href="https://orcid.org/{{ site.social.orcid }}" target="_blank">ORCID</a>
    </p>
  </div>
</section>

<section id="research" class="section">
            <h2>Research Interests</h2>
            <p>My primary research interests include:</p>
            <ul>
                <li>Deep Learning Architectures and Optimization</li>
                <li>Image Processing and Computer Vision</li>
                <li>Multimodal Learning (text, vision, audio)</li>
                <li>Generative Models and Transfer Learning</li>
            </ul>
</section>

<section id="publications" class="publications section">
  <h2>Selected Publications</h2>
  <ul>
    {% for p in site.data.publications %}
      <li><strong>{{ p.authors }}</strong> ({{ p.year }}). {{ p.title }}. <em>{{ p.venue }}</em>. {% if p.url %}<a href="{{ p.url }}" target="_blank">[PDF]</a>{% endif %}</li>
    {% endfor %}
    {% if site.data.publications == empty %}
      <li>No publications listed yet. Add entries in <code>_data/publications.yml</code>.</li>
    {% endif %}
  </ul>
</section>

<section id="projects" class="projects section">
  <h2>Projects</h2>
  <ul>
    {% for proj in site.data.projects %}
      <li>
        {% if proj.url %}<a href="{{ proj.url }}" target="_blank"><strong>{{ proj.name }}</strong></a>{% else %}<strong>{{ proj.name }}</strong>{% endif %}: {{ proj.description }}
      </li>
    {% endfor %}
    {% if site.data.projects == empty %}
      <li>No projects listed yet. Add entries in <code>_data/projects.yml</code>.</li>
    {% endif %}
  </ul>
</section>

<section id="blog" class="section">
  <h2>Blog</h2>
  <p><a href="{{ '/blog/' | relative_url }}">View my blog posts</a></p>
</section>

<section id="contact" class="contact section">
  <h2>Contact</h2>
  <p>If you'd like to get in touch, please email me at <a href="mailto:{{ site.author.email }}">{{ site.author.email }}</a>.</p>
</section>
