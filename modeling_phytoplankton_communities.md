---
layout: page
title: Introduction to Modelling Phytoplankton Communities in R
image: 
---

<h2>Introduction</h2>

<p>In 2021, I was asked to do a guest lecture on modelling in R. I created a presentation and a lab exercise from scratch. If you are interested, the following walk through explains how to develop a theoretical model. This is the basis of some of my modeling work such as that seen in <a href = "{{ 'Smith&Edwards-2019.html' | absolute_url }}">Smith and Edwards (2019). <i>Oikos</i></a>. <br />
There are a number of different types of models but here I am mostly focusing on theoretical modeling of phytoplankton communities which involves, as I understand it, developing mathematical equations or frameworks based on fundamental principles and assumptions to describe and predict the behavior of a system. Here, I walk through how to build a basic NPZ (Nutrient-Phytoplankton-Zooplankton) model from scratch first starting with a very simple model of the biomass accumulation of a single bacterial taxa growing in culture.</p>


<h2>A simple model</h2>
<p>The basic steps in developing any theoretical model is to start with understanding the theory(ies) that describe the system you are trying to model and then determining the equations that best represent that system. For example, the basic theory in this simple model is that you can calculate or predict changes in microbial population abundance over time if you know the growth rate. The basic equation here is: ${{{dP \over dt}} = Pr}$ where <i>P</i> stands for population, <i>t</i> stands for time, and <i>r</i> stands for growth rate. Obviously this is not how natural systems really operate but if conditions are perfect and there are no outside influences, then populations will continue to increase as fast as they can grow. </p>






