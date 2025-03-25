<script>
  import { onMount } from 'svelte';
   
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
   
  const contacts = [
    {
       label: 'Email',
       value: 'zaniquelli@outlook.com.br',
       link: 'mailto:zaniquelli@outlook.com.br'
    },
    {
       label: 'LinkedIn',
       value: 'linkedin.com/in/zaniquelli',
       link: 'https://www.linkedin.com/in/zaniquelli/'
    },
    {
       label: 'GitHub',
       value: 'github.com/Zaniquelli',
       link: 'https://github.com/Zaniquelli'
    }
  ];
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</svelte:head>

<div id="noise-overlay"></div>

<div class="dos-container">
  <div class="header">
    <div class="header-line">C:\USERS\ZANIQUELLI</div>
    <div class="time-line">{currentTime}</div>
  </div>
   
  <hr class="dos-divider">
   
  <div class="terminal">
    <p class="green-text">
      {typingText}<span class="cursor">_</span>
    </p>
   
    <hr class="dos-divider">
   
    <div class="contact-section">
      <h2>Contact Information:</h2>
      {#each contacts as contact}
        <p class="green-text">
          <strong>{contact.label}:</strong>
          <a
            href={contact.link}
            target="_blank"
            rel="noopener noreferrer"
            class="contact-link"
          >
            {contact.value}
          </a>
        </p>
      {/each}
    </div>
  </div>
</div>
