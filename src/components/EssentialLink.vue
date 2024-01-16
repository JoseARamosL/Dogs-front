<template>
  <q-item
    clickable
    tag="div"
    :href="link"
  >
    <q-item-section
      v-if="icon"
      avatar
    >
      <q-icon :name="icon" />
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ title }}</q-item-label>
      <q-item-label caption>{{ caption }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script>
import { defineComponent, toRefs } from 'vue';
import { useRouter } from 'vue-router';

export default defineComponent({
  name: 'EssentialLink',
  props: {
    title: {
      type: String,
      required: true
    },

    caption: {
      type: String,
      default: ''
    },

    link: {
      type: String,
      default: '#'
    },

    icon: {
      type: String,
      default: ''
    }
  },
  setup(props) {
    const { link } = toRefs(props);
    const router = useRouter();

    const navigateToLink = () => {
      router.push(link.value);
    };

    return {
      navigateToLink,
    };
  },
})
</script>
