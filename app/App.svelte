<script lang="typescript">
  import { onMount } from "svelte";

  //   import List from "./components/List.svelte";
  let message: string = "Blank Svelte Native App";
  const onButtonTap = () => {
    alert(message);
  };
  //   "https://api.github.com/users/sveltejs/repos"
  const onChangeText = (endpoint: string) => {
    fetch(endpoint);
  };
</script>

<page>
  <actionBar title="Svelte Native App" />
  <gridLayout>
    <label
      class="info"
      horizontalAlignment="center"
      verticalAlignment="middle"
      textWrap="true"
    >
      <formattedString>
        <span class="fas" text="&#xf135;" />
        <span text=" {message}" />
      </formattedString>
    </label>
  </gridLayout>
</page>

<style>
  .info .fas {
    color: #3a53ff;
  }
  .info {
    font-size: 20;
  }
</style>
