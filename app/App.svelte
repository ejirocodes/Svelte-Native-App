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
  }

  onMount(async () => {
    await getUsers();
  });
</script>

<page>
  <actionBar title="List of Users" />

  <!-- <button text="See more" on:tap={onItemTap} /> -->

  <!-- <textField bind:text={textFieldValue} hint="Enter your name" /> -->

  <flexboxLayout>
    <listView items={users} on:itemTap={onItemTap} row="1" colSpan="2">
      <Template let:item>
        <flexboxLayout>
          <label text="Name:" textWrap="true" class="first" />
          <label text={item.name} textWrap="true" class="name" />
        </flexboxLayout>
        <flexboxLayout>
          <label text="Username:" textWrap="true" class="first" />
          <label
            text={"@" + item.username.toLowerCase()}
            textWrap="true"
            class="last"
          />
        </flexboxLayout>
        <flexboxLayout>
          <label text="Email:" textWrap="true" class="first" />
          <label text={item.email} textWrap="true" class="first" />
        </flexboxLayout>
      </Template>
    </listView>
  </flexboxLayout>
</page>

<style scoped>
  ListView {
    background-color: #f5f5f5;
    color: #4831d4;
  }
  TextField {
    border-width: 2;
    border-color: #4831d4;
    border-style: solid;
    border-radius: 5;
    padding: 10;
  }
  Button {
    background-color: #4831d4;
    color: #f5f5f5;
    padding: 20;
    vertical-align: middle;
    font-weight: 400;
    font-size: 18;
    border-radius: 8;
  }
</style>
