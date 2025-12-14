---
layout: page 
permalink: /contact/ 
title: contact 
description: Feel free to reach out 
nav: true nav_order: 4
---
<!-- Custom Styling for this page -->

<style>
.contact-list {
font-size: 1.25rem; /* Adjustable font size /
font-weight: 400;   / Adjustable font weight /
}
.contact-item {
margin-bottom: 1.5rem; / Space between items /
display: flex;
align-items: center;
}
.contact-icon {
width: 2.5rem;      / Width of the icon column /
text-align: center;
margin-right: 0.5rem;
font-size: 1.5rem;  / Icon size /
color: var(--global-theme-color); / Uses your theme color /
}
.contact-item a {
color: inherit;     / Inherits the font color/weight from .contact-list /
text-decoration: none !important; / Forces no underline /
}
.contact-item a:hover {
color: var(--global-theme-color); / Changes color on hover /
text-decoration: none !important; / Forces no underline on hover */
}
</style>

<div class="contact-list">

<!-- Email -->

<div class="contact-item">
<span class="contact-icon"><i class="fa-solid fa-envelope"></i></span>
<a href="mailto:cl.friedman@berkeley.edu">cl.friedman@berkeley.edu</a>
</div>

<!-- LinkedIn -->

<div class="contact-item">
<span class="contact-icon"><i class="fa-brands fa-linkedin"></i></span>
<a href="https://www.linkedin.com/in/clara-friedman-od-b1b8631b1/" target="_blank" rel="noopener noreferrer">Connect with me on LinkedIn</a>
</div>

<!-- Google Scholar -->

<div class="contact-item">
<span class="contact-icon"><i class="ai ai-google-scholar"></i></span>
<a href="https://scholar.google.com/citations?user=3AfiygwAAAAJ&hl=en" target="_blank" rel="noopener noreferrer">Google Scholar Profile</a>
</div>

</div>
