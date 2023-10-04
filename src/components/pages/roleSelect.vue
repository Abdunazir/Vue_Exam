<template>
  <div >
    <AppModal  v-model="dialog">
      <div class="asos px-5">
        <h1 class="text-center">Select Role</h1>
        <form class="px-3 ">
          <select v-model="role" class="form-control py-2 select">
            <option class="bb" v-for="item in forms" :key="item" :value="item">
              {{ item }}
            </option>
          </select>
        </form>
        <Button class="btn d-block " :title="'success'" @click="yes(role)">Submit</Button>
        <Button class="btn d-block " @click="no">Back</Button>
      </div>
    </AppModal>
  </div>
</template>

<script setup>
  import Button from "@/components/ui/Button";

  import AppModal from "../ui/app-modal.vue";
  import { ref, watch } from "vue";
  import Notification from "@/plugins/Notification";
  import http from "@/plugins/api";
  import { useRouter } from "vue-router";
  const router = useRouter();
  const dialog = ref(false);

  const role = ref("");
  const forms = ref({
    roles: "",
  });

  watch(dialog, (value) => {
    if (!value) {
      forms.value = {};
    }
  });

  const openModal = (value) => {
    if (!value) {
      forms.value = {};
    } else if (value) forms.value = { ...value };

    dialog.value = true;
  };

  const yes = (item) => {
    console.log(item);
    http
      .post(`/api/admins/set-role`, { role: item })
      .then((res) => {
        router.push({ name: item });
      })
      .catch((error) => {
        Notification(error);
      });
  };

  const no = (e) => {
    e.preventDefault();
    localStorage.removeItem("token");
    localStorage.removeItem("roles");
    location.reload();
    dialog.value = false;
  };

  defineExpose({ openModal });
</script>

<style lang="scss" scoped>
.input {
  padding: 5px 30px;
}

h1{
  color: rgba(255, 255, 255, 0.70);
font-family: Inria Serif;
font-size: 60px;
font-style: normal;
font-weight: 700;
line-height: normal;
}

// .select {
// // background: rgba(49, 49, 59, 0.29);
// }

.bb{
  background: transparent;
}

// .asos{
//   border-radius: 10px;
// background: rgba(69, 69, 83, 0.29);
// box-shadow: 0px -5px 60px 0px rgba(0, 0, 0, 0.50);
// }
</style>
