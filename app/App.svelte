<script lang="javascript">
  import { onMount } from "svelte";
  import { Template } from "svelte-native/components";

  let users = [];

  const getUsers = async () => {
    try {
      let res = await fetch("https://randomuser.me/api/?results=30");
      let { results } = await res.json();
      users = results;
      isReady = true;
    } catch (err) {
      console.log(err);
    }
  };

  function onItemTap() {
    console.log("tap");
  }

  onMount(async () => {
    await getUsers();
    users.forEach((user) => console.log(user.email));
  });
</script>

<page>
  <actionBar title="Svelte Native App" />
  <flexboxLayout>
    <listView items={users} on:itemTap={onItemTap} row="1" colSpan="2">
      <Template let:item>
        <flexboxLayout>
          <label text={item.name.first} textWrap="true" class="first" />
          <label text={item.name.last} textWrap="true" class="last" />
        </flexboxLayout>
      </Template>
    </listView>
  </flexboxLayout>
</page>

<style>
</style>
