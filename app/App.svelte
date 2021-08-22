<script lang="javascript">
  import { onMount } from "svelte";
  import { Template } from "svelte-native/components";
  import Details from "./pages/Details.svelte";
  import { navigate } from "svelte-native";

  let users = [];

  const getUsers = async () => {
    try {
      let res = await fetch("https://jsonplaceholder.typicode.com/users");
      let data = await res.json();
      users = data;
    } catch (err) {
      console.log(err);
    }
  };

  function onItemTap(args) {
    // console.log(
    //   `Item ${users[args.index].id} at index: ${args.index} was tapped`
    // );
    navigate({
      page: Details,
      props: { user: users[args.index] },
    });
    // navigate({ page: Details });
  }

  onMount(async () => {
    await getUsers();
  });
</script>

<page>
  <actionBar title="List of Users" />
  <button text="To Details directly" on:tap={onItemTap} />

  <flexboxLayout>
    <listView items={users} on:itemTap={onItemTap} row="1" colSpan="2">
      <Template let:item>
        <flexboxLayout>
          <label text={item.name} textWrap="true" class="name" />
        </flexboxLayout>
        <flexboxLayout>
          <label text={"@" + item.username} textWrap="true" class="last" />
        </flexboxLayout>
        <flexboxLayout>
          <label text="Email:" textWrap="true" class="first" />
          <label text={item.email} textWrap="true" class="first" />
        </flexboxLayout>
      </Template>
    </listView>
  </flexboxLayout>
</page>

<style>
</style>
