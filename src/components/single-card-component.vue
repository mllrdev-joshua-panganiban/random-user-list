<template>
  <div
    class="bg-white pt-10 rounded flex flex-col space-y-4 justify-between h-auto border-2 border-black shadow-lg"
  >
    <div class="flex justify-center">
      <img class="rounded-full h-36 w-36" :src="user.picture.large" />
    </div>
    <div>
      <h1 class="text-2xl mt-4 flex justify-center">
        {{ fullName }}
      </h1>
      <h2 class="text-m mb-3 flex justify-center">
        {{ user.email }}
      </h2>
    </div>
    <router-link :to="`/userProfile/` + index">
      <div class="h-16 text-center p-5 border border-gray-300">
        <h1>VIEW PROFILE</h1>
      </div>
    </router-link>
  </div>
</template>

<script lang="ts">
import { IUser } from "@/types/user";
import { computed, defineComponent, PropType, ref } from "vue";

export default defineComponent({
  props: {
    index: {
      type: Number,
      required: true,
    },
    user: {
      type: Object as PropType<IUser>,
      required: true,
    },
  },
  setup(props) {
    const firstName = ref<string>(props.user.name.first);
    const lastName = ref<string>(props.user.name.last);

    const fullName = computed<string>(() => {
      return `${firstName.value} ${lastName.value}`;
    });

    return { fullName };
  },
});
</script>
