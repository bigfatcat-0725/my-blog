---
title: Todo app I use
description: Todays todo
tags:
  - personal
  - tech
date: 2022-02-18
---

<svelte:head>

  <meta name="description" content={title} />
</svelte:head>

<div class="box">

<h1>{title}</h1>
<p class="date">{new Date(date).toDateString()}</p>

This is First post

</div>

<style>
  * {
    margin: 0 auto;
    text-align: center;
    color: white;
  }
  .box {
    width: 90%;
  }
  h1 {
    font-size: 2rem
  }
  .date {
    text-align: right;
    color: gray;
  }
 
</style>
