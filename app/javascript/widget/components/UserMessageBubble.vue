<script>
import { useMessageFormatter } from 'shared/composables/useMessageFormatter';

export default {
  name: 'UserMessageBubble',
  props: {
    message: {
      type: String,
      default: '',
    },
    widgetColor: {
      type: String,
      default: '',
    },
  },
  setup() {
    const { formatMessage } = useMessageFormatter();
    return {
      formatMessage,
    };
  },
};
</script>

<template>
  <div
    v-dompurify-html="formatMessage(message, false)"
    class="chat-bubble user"
    :style="{ '--eyun-widget-color': widgetColor }"
  />
</template>

<style lang="scss" scoped>
.chat-bubble.user {
  :deep(p code) {
    @apply bg-n-alpha-2 dark:bg-n-alpha-1 text-n-slate-12;
  }

  :deep(pre) {
    @apply text-n-slate-12 bg-n-alpha-2 dark:bg-n-alpha-1;

    code {
      @apply bg-transparent text-n-slate-12;
    }
  }

  :deep(blockquote) {
    @apply bg-transparent border-n-slate-7 ltr:border-l-2 rtl:border-r-2 border-solid;

    p {
      @apply text-n-slate-11;
    }
  }
}
</style>
