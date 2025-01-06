---
layout: page
title: About
permalink: /about/
---
> I am currently a founding product manager at [Airflip](https://www.airflip.com/), a vendor intelligence platform for enterprise procurement teams. I launched our intial product, leading the development of our vendor research, deal management workflows, and AI-driven spend analytics.
>
> Previously, I was as an Optimization Specialist at Blackrock working on their [Aladdin](https://www.blackrock.com/aladdin/offerings/aladdin-enterprise) risk and trading platform. I was responsible for delivering new optimization use cases, supporting 10+ enterprise clients, and driving optimization adoption for portfolio construction and risk management tools.
>
> I have a BA in Data Science with an emphasis on Cognition and AI from UC Berkeley. While in school, I worked for the [Division of Data Science](https://cdss.berkeley.edu/), where I led a marketing team to promote the launch of the new data science major. I was also the Chief Marketing Officer for [ML@B](https://coral-partners-321934.framer.app/), Berkeley's machine learning club, where I created strategic content showcasing the academic and industry applications of machine learning.

## Contents

&nbsp;&nbsp;&nbsp;&nbsp;[**Portfolio Optimization**](/portfolio-optimization)  
&nbsp;&nbsp;&nbsp;&nbsp; Walkthrough of portfolio optimization, with insights drawn from my work on Aladdin at BlackRock.

&nbsp;&nbsp;&nbsp;&nbsp;[**A/B Testing Project**](/ab-testing-project)  
&nbsp;&nbsp;&nbsp;&nbsp; Designed an A/B test project to analyze a feature's impact on user engagement and conversion rates.

&nbsp;&nbsp;&nbsp;&nbsp;[**Forms for Procurement**](/forms-module)  
&nbsp;&nbsp;&nbsp;&nbsp;Led a cross-functional team at Airflip to design and launch a form builder for procurement teams.

&nbsp;&nbsp;&nbsp;&nbsp;[**Spend Analytics Visuals**](/spend-analytics-visuals)  
&nbsp;&nbsp;&nbsp;&nbsp; Created Python prototypes of spend analytics visuals for Airflip, providing engineering with clear implementation steps.

&nbsp;&nbsp;&nbsp;&nbsp;[**Website Redesign**](/website-redesign)  
&nbsp;&nbsp;&nbsp;&nbsp;Led Airflip's website and product documentation redesign, improving usability and brand alignment.

&nbsp;&nbsp;&nbsp;&nbsp;[**Blogs & Content**](/blogs-content)  
&nbsp;&nbsp;&nbsp;&nbsp;Authored articles on procurement concepts and created content for UC Berkeley Marketing initiatives.

&nbsp;&nbsp;&nbsp;&nbsp;[**Adventures**](/adventures)  
&nbsp;&nbsp;&nbsp;&nbsp;Some photography from my backpacking adventures.

<style>
.image-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1rem;
    padding: 0;
    margin-top: 1rem;
}

.image-item {
    width: 100%;
    height: 200px;
    object-fit: cover;
    cursor: pointer;
    transition: transform 0.3s ease;
}

.image-item:hover {
    transform: scale(1.05);
}

.modal {
    display: none;
    position: fixed;
    z-index: 1000;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.9);
}

.modal-content {
    margin: auto;
    display: block;
    max-width: 90%;
    max-height: 90vh;
    position: relative;
    top: 50%;
    transform: translateY(-50%);
}

.close {
    position: absolute;
    top: 15px;
    right: 35px;
    color: #f1f1f1;
    font-size: 40px;
    font-weight: bold;
    cursor: pointer;
}

.nav-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    color: white;
    font-size: 30px;
    cursor: pointer;
    padding: 16px;
    background-color: rgba(0, 0, 0, 0.5);
    border: none;
    border-radius: 4px;
}

.prev {
    left: 0px;
}

.next {
    right: 20px;
}
</style>

<div class="image-grid">
    <img src="/public/images/collage/1.png" alt="Adventure Image 1" class="image-item" onclick="openModal(this)">
    <img src="/public/images/collage/16.png" alt="Adventure Image 2" class="image-item" onclick="openModal(this)">
    <img src="/public/images/collage/8.png" alt="Adventure Image 3" class="image-item" onclick="openModal(this)">
</div>

<div id="imageModal" class="modal">
    <span class="close" onclick="closeModal()">&times;</span>
    <button class="nav-button prev" onclick="changeImage(-1)">&#10094;</button>
    <img id="modalImage" class="modal-content">
    <button class="nav-button next" onclick="changeImage(1)">&#10095;</button>
</div>

<script>
let currentImageIndex = 0;
const images = document.querySelectorAll('.image-item');
const modal = document.getElementById('imageModal');
const modalImg = document.getElementById('modalImage');

function openModal(img) {
    modal.style.display = "block";
    modalImg.src = img.src;
    currentImageIndex = Array.from(images).indexOf(img);
    document.addEventListener('keydown', handleKeyPress);
}

function closeModal() {
    modal.style.display = "none";
    document.removeEventListener('keydown', handleKeyPress);
}

function changeImage(direction) {
    currentImageIndex += direction;
    if (currentImageIndex >= images.length) {
        currentImageIndex = 0;
    } else if (currentImageIndex < 0) {
        currentImageIndex = images.length - 1;
    }
    modalImg.src = images[currentImageIndex].src;
}

function handleKeyPress(event) {
    if (event.key === "ArrowLeft" || event.key === "h") {
        changeImage(-1);
    } else if (event.key === "ArrowRight" || event.key === "l") {
        changeImage(1);
    } else if (event.key === "Escape") {
        closeModal();
    }
}

modal.addEventListener('click', function(event) {
    if (event.target === modal) {
        closeModal();
    }
});
</script>
