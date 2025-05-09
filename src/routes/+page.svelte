<script lang="ts">
  import { onMount } from 'svelte';
  import Header from '$lib/components/Header.svelte';
  import ContactSection from '$lib/components/ContactSection.svelte';
  import { contacts } from '$lib/data/contacts';
   
  let currentTime = '';
  let typingText = '';
  const fullText = 'System startup, live long and login';
  let textIndex = 0;
   
  function typeWriter() {
    if (textIndex < fullText.length) {
      typingText += fullText.charAt(textIndex);
      textIndex++;
      setTimeout(typeWriter, 100);
    }
  }
   
  function updateTime() {
    const now = new Date();
    currentTime = now.toLocaleString('en-US', {
      hour: '2-digit',
      minute: '2-digit',
      second: '2-digit',
      day: '2-digit',
      month: '2-digit',
      year: 'numeric'
    });
  }
   
  onMount(() => {
    typeWriter();
    updateTime();
    const timeInterval = setInterval(updateTime, 1000);
    return () => clearInterval(timeInterval);
  });
</script>

<svelte:head>
  <title>Zaniquelli - DOS Portfolio</title>
  <meta name="description" content="Zaniquelli's retro DOS-style portfolio">
  <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</svelte:head>

<div id="noise-overlay"></div>

<div class="dos-container">
  <Header {currentTime} />
   
  <div class="terminal">
    <p class="green-text">
      {typingText}<span class="cursor">_</span>
    </p>
   
    <hr class="dos-divider">
   
    <ContactSection {contacts} />
  </div>
</div>