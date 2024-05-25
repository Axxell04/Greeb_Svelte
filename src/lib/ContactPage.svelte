<script>
  import { slide } from "svelte/transition";
  import { sineInOut } from "svelte/easing";
  import Notification from "./Notification.svelte";
  import { URLServer } from "../stores/store";

  let inputEmail = document.getElementById("email");

  let notificationVisible = false;
  let notificationType = "";
  let notificationTitle = "";
  let notificationMessage = "";

  let alertValidationEmail = false;
  let alertValidationMessage = false;

  const validateInputs = (inputEmail, inputMessage) => {
    if (!inputEmail.value) {
      alertValidationEmail = true;
    }
    if (!inputMessage.value) {
      alertValidationMessage = true;
    }
    if (!alertValidationEmail && !alertValidationMessage) {
      return true;
    }
    return false;
  };

  const showNotification = (type="", title="", message="") => {
    notificationType = type;
    notificationTitle = title;
    notificationMessage = message;
    notificationVisible = true;
    setTimeout(() => {
      notificationVisible = false;
    }, 5000);
  };

  const enter = (inputEmail, inputMessage) => {
    if (validateInputs(inputEmail, inputMessage)) {
      sendMessage(inputEmail, inputMessage);
    }
  };

  const sendMessage = async (inputEmail, inputMessage) => {
    try {
      const res = await fetch(`${$URLServer}/api/send_mail`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          contact_mail: inputEmail.value,
          message: inputMessage.value,
        }),
      });
      
      if (res.ok) {
        showNotification("Success", "Mensaje enviado", "¡Nos contactaremos con usted muy pronto!");
      } else {
        showNotification("Error", "Error al enviar el mensaje", "¡Vuelva a intentarlo!");
      }
      inputEmail.value = "";
      inputMessage.value = "";
      
    } catch (error) {
      showNotification("Error", "Error al enviar el mensaje", "¡Vuelva a intentarlo!");
    }
  };
</script>

{#if notificationVisible}
  <div
    transition:slide={{
      delay: 250,
      duration: 1000,
      easing: sineInOut,
      axis: "y",
    }}
  >
    <Notification
      type={notificationType}
      title={notificationTitle}
      message={notificationMessage}
    />
  </div>
{/if}
<div class="flex flex-col py-4 px-4 place-items-center sm:px-28 xl:px-52">
  <div
    class="bg-slate-800 py-3 px-3 rounded-md flex flex-col gap-4 place-items-stretch min-w-full"
  >
    <div class="flex flex-col gap-2 place-items-stretch">
      <label for="" class="text-lime-200"
        >Ingrese su correo <span class="text-red-500"
          >{alertValidationEmail ? "¡Debe llenar el campo!" : ""}</span
        ></label
      >
      <input
        id="email"
        type="email"
        class="px-2 rounded"
        on:input={(e) => (alertValidationEmail = false)}
      />
      <label for="" class="text-lime-200"
        >Escriba su mensaje <span class="text-red-500"
          >{alertValidationMessage ? "¡Debe llenar el campo!" : ""}</span
        ></label
      >
      <textarea
        name="mensaje"
        id="message"
        class="px-2 rounded"
        on:input={(e) => (alertValidationMessage = false)}
      ></textarea>
    </div>
    <button
      class="text-lime-200 py-3 px-3 rounded-md outline outline-lime-400 outline-1 hover:opacity-70"
      on:click={() => {
        const inputEmail = document.getElementById("email");
        const inputMessage = document.getElementById("message");
        enter(inputEmail, inputMessage);
      }}>Enviar</button
    >
  </div>
</div>
