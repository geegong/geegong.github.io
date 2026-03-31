---
layout: single
title: "Resume"
permalink: /resume/
author_profile: false
---

<style>
.resume-section { margin-bottom: 2em; }
.resume-section h2 {
  border-bottom: 2px solid #7a8288;
  padding-bottom: 0.3em;
  margin-bottom: 0.8em;
}
.resume-entry { margin-bottom: 1.2em; }
.resume-entry .title-line {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.resume-entry .role { font-weight: bold; font-size: 1.05em; }
.resume-entry .period { color: #7a8288; font-size: 0.9em; }
.resume-entry .org { color: #aaa; font-size: 0.95em; margin-bottom: 0.4em; }
.skills-grid {
  display: flex;
  flex-direction: column;
  gap: 0.8em;
}
.skill-category {
  display: flex;
  align-items: baseline;
  gap: 0.8em;
  flex-wrap: wrap;
}
.skill-category-label {
  font-size: 0.8em;
  font-weight: 600;
  color: #7a8288;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  min-width: 9em;
  flex-shrink: 0;
}
.skill-tags {
  font-size: 0.95em;
  color: #ddd;
}
</style>

<div style="text-align:center; margin-bottom: 2em;">
  <h1 style="margin-bottom: 0.2em;">Jiyoung Kim</h1>
  <p style="color: #aaa; margin: 0;">
    📍 South Korea &nbsp;|&nbsp;
    ✉️ <span id="email-copy" onclick="copyEmail()" style="cursor:pointer; text-decoration:underline dotted;" title="Click to copy">shchj66@gmail.com</span> &nbsp;|&nbsp;
    📞 +82)10-2534-8251 &nbsp;|&nbsp;
    <a href="https://geegong.github.io">Blog</a>&nbsp;|&nbsp;
    <a href="https://github.com/geegong">Github</a>
  </p>
</div>

---

<div class="resume-section">
<h2>Professional Summary</h2>
<p>Senior Java Backend Engineer with 10+ years of experience at NHN, specializing in payment systems, checkout flows, and PG/PSP integrations. Experienced in building and maintaining backend services for large-scale payment platforms, with a strong focus on system reliability, legacy modernization, and safe delivery in production environments. Proven ability to work across complex payment domains including checkout, payment authorization, discount logic, and external payment gateway integrations.</p>
</div>

<div class="resume-section">
<h2>Core Skills</h2>
<div class="skills-grid">
  <div class="skill-category">
    <span class="skill-category-label">Backend</span>
    <span class="skill-tags">Java, Spring Boot, REST APIs, SQL</span>
  </div>
  <div class="skill-category">
    <span class="skill-category-label">Cloud / Infra</span>
    <span class="skill-tags">AWS, ECS, ElastiCache, SQS, Lambda, S3</span>
  </div>
  <div class="skill-category">
    <span class="skill-category-label">Payments</span>
    <span class="skill-tags">Payment Systems, Checkout Flows, Payment Gateway Integration</span>
  </div>
  <div class="skill-category">
    <span class="skill-category-label">Engineering</span>
    <span class="skill-tags">Legacy System Maintenance, Production Troubleshooting, Service Stability</span>
  </div>
</div>
</div>

<div class="resume-section">
<h2>Professional Experience</h2>
<div class="resume-entry">
  <div class="title-line">
    <span class="role">Java Backend Engineer</span>
    <span class="period">January 2014 – Present</span>
  </div>
  <div class="org">NHN</div>
  <p>Senior Java Backend Engineer with 10+ years of experience at NHN, specializing in payment systems, checkout flows, and payment gateway integrations. Experienced in building and maintaining backend services in large-scale production environments, with strong expertise in legacy system improvement, external payment integration, and reliable service delivery. Proven ability to work across multiple payment-related projects with a strong focus on stability, maintainability, and operational safety.</p>

  <p><strong>Japanese PSP Integrations via PG Proxy</strong> <em style="color:#7a8288; font-size:0.9em;">(Current Project)</em></p>
  <ul>
    <li>Currently working on integrations with Japanese payment providers through an intermediate PG proxy layer.</li>
    <li>Implement backend functionality based on proxy-defined interfaces rather than direct provider-level APIs.</li>
    <li>Support Japan-focused payment flows within an indirect integration architecture designed to reduce coupling with external providers.</li>
    <li>Develop and operate services in an AWS-based environment, using ECS, ElastiCache, SQS, Lambda, and S3.</li>
    <li>Contribute to the ongoing enhancement and stable operation of payment integration services in production.</li>
  </ul>

  <p><strong>Payment Platform Backend</strong></p>
  <ul>
    <li>Built and maintained backend services for PAYCO, a Korean digital wallet and payment service.</li>
    <li>Supported core payment flows including checkout, payment authorization, and transaction processing.</li>
    <li>Contributed to the stable operation and continuous improvement of production payment services.</li>
  </ul>

  <p><strong>Korean Payment Gateway Integrations</strong></p>
  <ul>
    <li>Implemented and maintained backend integrations with KCP, one of the major payment gateways in South Korea.</li>
    <li>Handled provider-specific request and response mapping, operational edge cases, and troubleshooting.</li>
    <li>Supported reliable payment processing by adapting backend systems to external provider requirements.</li>
  </ul>

  <p><strong>Legacy Coupon / Discount Engine Improvement</strong></p>
  <ul>
    <li>Worked on improving a legacy coupon and discount engine in an older payment system.</li>
    <li>Addressed maintainability issues caused by business rules being distributed across multiple parts of the system.</li>
    <li>Focused on making changes safely in a regression-sensitive environment with high operational impact.</li>
  </ul>
</div>
</div>

<div class="resume-section">
<h2>Education</h2>
<div class="resume-entry">
  <div class="title-line">
    <span class="role">Bachelor's Degree in Electronic Engineering</span>
  </div>
  <div class="org">Soongsil University · Seoul, Korea</div>
</div>
</div>

<div class="resume-section">
<h2>Languages</h2>
<ul>
  <li><strong>Korean</strong> — Native</li>
  <li><strong>English</strong> — Professional working proficiency</li>
</ul>
</div>

<script>
function copyEmail() {
  navigator.clipboard.writeText('shchj66@gmail.com').then(function() {
    var el = document.getElementById('email-copy');
    var original = el.textContent;
    el.textContent = 'Copied!';
    el.style.color = '#7a8288';
    setTimeout(function() {
      el.textContent = original;
      el.style.color = '';
    }, 1500);
  });
}
</script>
