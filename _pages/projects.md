---
layout: page
title: 项目
permalink: /projects/
description: 具身智能（VLA 基座模型 / 灵巧手 / 人形 loco-manipulation）与脑机接口方向的实习与研究项目。
nav: true
nav_order: 2
display_categories: [工作, 研究]
horizontal: false
---

<style>
  .projects .project-brand-link {
    display: block;
    height: 100%;
    color: inherit;
    text-decoration: none;
  }

  .projects .project-brand-card {
    position: relative;
    overflow: hidden;
    border: 1px solid color-mix(in srgb, var(--brand-accent) 24%, var(--global-divider-color));
    border-top: 4px solid var(--brand-accent);
    border-radius: 1rem;
    background: linear-gradient(155deg, var(--brand-tint) 0%, var(--global-card-bg-color) 46%);
    box-shadow: 0 12px 32px rgb(15 23 42 / 7%);
    transition:
      transform 180ms ease,
      box-shadow 180ms ease,
      border-color 180ms ease;
  }

  .projects .project-brand-logo-panel {
    display: flex;
    min-height: 8.25rem;
    align-items: center;
    justify-content: center;
    padding: 1.35rem 1.5rem;
    background: rgb(255 255 255 / 96%);
    border-bottom: 1px solid color-mix(in srgb, var(--brand-accent) 18%, transparent);
  }

  .projects .project-brand-logo {
    width: 84%;
    max-width: 13rem;
    height: 4.25rem;
    object-fit: contain;
    transition: transform 180ms ease;
  }

  .projects .project-brand-body {
    display: flex;
    flex: 1 1 auto;
    flex-direction: column;
    padding: 1.15rem 1.2rem 1rem;
  }

  .projects .project-brand-kicker {
    align-self: flex-start;
    margin-bottom: 0.55rem;
    padding: 0.22rem 0.58rem;
    border-radius: 999px;
    color: var(--brand-accent);
    background: color-mix(in srgb, var(--brand-accent) 11%, transparent);
    font-size: 0.74rem;
    font-weight: 700;
    letter-spacing: 0.04em;
  }

  .projects .project-brand-card .card-title {
    margin-bottom: 0.65rem;
    color: var(--global-text-color);
    font-size: 1.15rem;
    line-height: 1.35;
  }

  .projects .project-brand-card .card-text {
    margin-bottom: 1rem;
    color: var(--global-text-color-light);
    font-size: 0.91rem;
    line-height: 1.65;
  }

  .projects .project-brand-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: auto;
    padding-top: 0.8rem;
    border-top: 1px solid color-mix(in srgb, var(--brand-accent) 16%, var(--global-divider-color));
    color: var(--global-text-color-light);
    font-size: 0.8rem;
  }

  .projects .project-brand-cta {
    color: var(--brand-accent);
    font-weight: 700;
  }

  .projects .project-brand-link:hover .project-brand-card {
    transform: translateY(-4px);
    border-color: color-mix(in srgb, var(--brand-accent) 52%, var(--global-divider-color));
    box-shadow: 0 18px 44px color-mix(in srgb, var(--brand-accent) 14%, transparent);
  }

  .projects .project-brand-link:hover .project-brand-logo {
    transform: scale(1.035);
  }

  .projects .project-brand-link:focus-visible {
    outline: 3px solid color-mix(in srgb, var(--brand-accent) 55%, transparent);
    outline-offset: 4px;
    border-radius: 1rem;
  }

  html[data-theme="dark"] .projects .project-brand-card {
    background: linear-gradient(
      155deg,
      color-mix(in srgb, var(--brand-accent) 12%, var(--global-card-bg-color)) 0%,
      var(--global-card-bg-color) 48%
    );
    box-shadow: 0 12px 32px rgb(0 0 0 / 24%);
  }

  @media (prefers-reduced-motion: reduce) {
    .projects .project-brand-card,
    .projects .project-brand-logo {
      transition: none;
    }
  }
</style>

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
