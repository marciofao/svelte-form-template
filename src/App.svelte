<script>
  import Login from "./Login.svelte";
  import { onMount, setContext } from "svelte";

  import {
    key as userContextKey,
    initialValue as userContextInitialValue,
  } from "./userContext";

  onMount(() => {
    setContext(userContextKey, userContextInitialValue);
  });

  const submit = ({ email, passord }) => {
    new Promise((resolve, reject) => {
      setTimeout(() => {
        setContext(userContextKey, {
          name: "Marcio",
          lastName: "Fão",
          email: "ayo@leon.com",
        });
        resolve();
      }, 1000);
    });
  };
</script>

<section>
  <Login {submit} />
</section>

<style>
  section {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: solid black;
  }
</style>
