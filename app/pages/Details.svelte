<script>
  import { onMount } from "svelte";

  export let user;

  function onItemTap() {
    console.log(`User ${user}`);

    // navigate({ page: Details });
  }
  onMount(() => {
    console.log(user);
  });
</script>

<page>
  <stackLayout>
    <flexboxLayout>
      <flexboxLayout>
        <label text={user.name} textWrap="true" class="name" />
      </flexboxLayout>
      <flexboxLayout>
        <label
          text={"@" + user.username.toLowerCase()}
          textWrap="true"
          class="last"
        />
      </flexboxLayout>
      <flexboxLayout>
        <label text="Email:" textWrap="true" class="first" />
        <label text={user.email} textWrap="true" class="first" />
      </flexboxLayout>
      <label text={user.address.city} textWrap="true" class="first" />
      <label text={user.address.street} textWrap="true" class="first" />
      <label text={user.phone} textWrap="true" class="first" />
    </flexboxLayout>
  </stackLayout>
</page>

<style>
  StackLayout {
    width: 300;
    height: 300;
    padding: 10 16;
    background-color: #f0f0f0;
    box-shadow: 0 10px 53px 0 red;
    color: #4831d4;
  }
  label {
    font-size: 18;
    margin: 8 0;
  }
</style>
