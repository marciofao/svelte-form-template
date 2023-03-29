<script>
  let email = "";
  let password = "";
  let isloading = false;
  let isSuccess = false;

  export let submit;
  let errors = {};

  const handleSubmit = () => {
    errors = {};

    if (email.length === 0) {
      errors.mail = "Field should not be empty";
    }
    if (password.length === 0) {
      errors.password = "Field should not be empty";
    }

    if (Object.keys(errors).length === 0) {
      isloading = true;
      submit({ email, password })
        .then(() => {
          isSuccess = true;
          isloading = false;
        })
        .catch((err) => {
          errors.server = err;
          isloading = false;
        });
    }
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
  {#if inSuccess}
    <div class="success">
      🔒
      <br />
      You've been successfully Logged In.
    </div>
  {:else}
    <h1><img src="img/login.png" alt="login image" /></h1>
    <!-- svelte-ignore ally-label-has-associated-control-->
    <label for="email">Email</label>
    <input name="email" placeholder="name@example.com" bind:value={email} />
    <!-- svelte-ignore ally-label-has-associated-control -->
    <label for="password">Password</label>
    <input type="password" bind:value={password} />
    <button type="submit">
      {#if isloading}
        Logging in...
      {:else}
        Log in 🔒
      {/if}
    </button>
    {#if Object.keys(errors).length > 0}
      <ul class="errors">
        {#each Object.keys(errors) as field}
          <li>{field}: {errors[field]}</li>
        {/each}
      </ul>
    {/if}
  {/if}
</form>

<style>
  form {
    background: #fff;
    padding: 50px;
    width: 250px;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-shadow: 0px 20px 14px 8px rgba(0, 0, 0, 0.58);
  }
  label {
    margin: 10px 0;
    align-self: flex-start;
    font-weight: 500;
  }
  input {
    border: none;
    border-bottom: 1px solid #ccc;
    margin-bottom: 20px;
    transition: all 300ms ease-in-out;
  }
</style>
