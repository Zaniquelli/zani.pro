<script lang="ts">
  interface Contact {
    label: string;
    value: string;
    link: string;
  }
  
  export let contacts: Contact[];
</script>

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