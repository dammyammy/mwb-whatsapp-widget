<svelte:options tag="whatsapp-widget" />

<script>
    let open = false;
    let message = '';

    export let name = 'Your Name';
    export let number = '+4489000000000';
    export let avatar = null;
    export let description = "Typically replies within an hour";
    export let welcomeMessage = "Hi there 👋<br><br>How can We help you?";
    export let pattern = "https://res.cloudinary.com/eventbree/image/upload/v1575854793/Widgets/whatsapp-bg.png";

    function getTime() {
      let today = new Date();
      return String(today.getHours()).padStart(2, '0') + ":" + String(today.getMinutes()).padStart(2, '0');
    }

    function toggleWidget() {
        open = !open;
    }

    function sendMessage() {
      var url = !(/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) 
        ? "https://web.whatsapp.com/send?phone=" + number + "&text=" + encodeURIComponent(message)
        : "https://wa.me/" + String(number).replace('+', '') + "?text=" + encodeURIComponent(message)

      window.open(url, "_blank");

      message = '';
      open = false;
    }
       
    $: getName = name ? name : number;
</script>


<div id="app">
    <div id='whatsapp-chat' class={open ? 'show' : 'hide'}>
      <div class='whatsapp-chat-header'>
          <div class='whatsapp-chat-avatar'>
            {#if avatar !== null}
            <img src={avatar} alt={getName + ' Logo'} />
            {:else}
            <svg v-else xmlns="http://www.w3.org/2000/svg" viewBox="0 0 212 212" width="50" height="50"><path fill="#DFE5E7" d="M106.251.5C164.653.5 212 47.846 212 106.25S164.653 212 106.25 212C47.846 212 .5 164.654.5 106.25S47.846.5 106.251.5z"></path><g fill="#FFF"><path d="M173.561 171.615a62.767 62.767 0 0 0-2.065-2.955 67.7 67.7 0 0 0-2.608-3.299 70.112 70.112 0 0 0-3.184-3.527 71.097 71.097 0 0 0-5.924-5.47 72.458 72.458 0 0 0-10.204-7.026 75.2 75.2 0 0 0-5.98-3.055c-.062-.028-.118-.059-.18-.087-9.792-4.44-22.106-7.529-37.416-7.529s-27.624 3.089-37.416 7.529c-.338.153-.653.318-.985.474a75.37 75.37 0 0 0-6.229 3.298 72.589 72.589 0 0 0-9.15 6.395 71.243 71.243 0 0 0-5.924 5.47 70.064 70.064 0 0 0-3.184 3.527 67.142 67.142 0 0 0-2.609 3.299 63.292 63.292 0 0 0-2.065 2.955 56.33 56.33 0 0 0-1.447 2.324c-.033.056-.073.119-.104.174a47.92 47.92 0 0 0-1.07 1.926c-.559 1.068-.818 1.678-.818 1.678v.398c18.285 17.927 43.322 28.985 70.945 28.985 27.678 0 52.761-11.103 71.055-29.095v-.289s-.619-1.45-1.992-3.778a58.346 58.346 0 0 0-1.446-2.322zM106.002 125.5c2.645 0 5.212-.253 7.68-.737a38.272 38.272 0 0 0 3.624-.896 37.124 37.124 0 0 0 5.12-1.958 36.307 36.307 0 0 0 6.15-3.67 35.923 35.923 0 0 0 9.489-10.48 36.558 36.558 0 0 0 2.422-4.84 37.051 37.051 0 0 0 1.716-5.25c.299-1.208.542-2.443.725-3.701.275-1.887.417-3.827.417-5.811s-.142-3.925-.417-5.811a38.734 38.734 0 0 0-1.215-5.494 36.68 36.68 0 0 0-3.648-8.298 35.923 35.923 0 0 0-9.489-10.48 36.347 36.347 0 0 0-6.15-3.67 37.124 37.124 0 0 0-5.12-1.958 37.67 37.67 0 0 0-3.624-.896 39.875 39.875 0 0 0-7.68-.737c-21.162 0-37.345 16.183-37.345 37.345 0 21.159 16.183 37.342 37.345 37.342z"></path></g></svg>
            {/if}
          </div>
          <p>
            <span class="whatsapp-chat-name">{getName}</span>
            <br>
            <small style="float: left;">{description}</small>
          </p>
      </div>

      <div class="whatsapp-chat-body" pattern={pattern} >
        <div class="whatsapp-chat-bubble">
          <div style="opacity: 0;" class="whatsapp-chat-message-loader">
            <div style="position: relative;display: flex;">
              <div class="ixsrax"></div>
              <div class="dRvxoz"></div>
              <div class="kXBtNt"></div>
            </div>
          </div>
          <div style="opacity: 1;" class="whatsapp-chat-message">
            <div class="bMIBDo">{getName}</div>
            <div class="iSpIQi">{@html welcomeMessage}</div>
            <div class="cqCDVm">{getTime()}</div>
          </div>
        </div>
      </div>

      <div class='whatsapp-message-box'>
        <textarea bind:value={message} placeholder='Write a response' maxlength='120' row='1'></textarea> <!-- LOOK INTO -->
        <button type="button" on:click={sendMessage}>
          <svg viewBox="0 0 448 448"><path d="M.213 32L0 181.333 320 224 0 266.667.213 416 448 224z"/></svg>
        </button>
      </div>

      <button type="button" class='close-chat' on:click={toggleWidget}>×</button>
    </div>

    <button class='whatsapp-trigger-chat' on:click={toggleWidget} title='Show Chat'>
      <svg width="18" viewBox="0 0 24 24">
        <path fill="#eceff1" d="M20.5 3.4A12.1 12.1 0 0012 0 12 12 0 001.7 17.8L0 24l6.3-1.7c2.8 1.5 5 1.4 5.8 1.5a12 12 0 008.4-20.3z"/>
        <path fill="#4caf50" d="M12 21.8c-3.1 0-5.2-1.6-5.4-1.6l-3.7 1 1-3.7-.3-.4A9.9 9.9 0 012.1 12a10 10 0 0117-7 9.9 9.9 0 01-7 16.9z"/>
        <path fill="#fafafa" d="M17.5 14.3c-.3 0-1.8-.8-2-.9-.7-.2-.5 0-1.7 1.3-.1.2-.3.2-.6.1s-1.3-.5-2.4-1.5a9 9 0 01-1.7-2c-.3-.6.4-.6 1-1.7l-.1-.5-1-2.2c-.2-.6-.4-.5-.6-.5-.6 0-1 0-1.4.3-1.6 1.8-1.2 3.6.2 5.6 2.7 3.5 4.2 4.2 6.8 5 .7.3 1.4.3 1.9.2.6 0 1.7-.7 2-1.4.3-.7.3-1.3.2-1.4-.1-.2-.3-.3-.6-.4z"/>
      </svg> 
      <span>
      Chat with Us
      </span>
    </button>
  </div>

  <style lang="scss" src="./app.scss"></style><!-- your code here -->
