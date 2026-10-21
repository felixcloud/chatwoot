<script>
import FluentIcon from 'shared/components/FluentIcon/Index.vue';

export default {
  components: {
    FluentIcon,
  },
  props: {
    url: {
      type: String,
      default: '',
    },
    isInProgress: {
      type: Boolean,
      default: false,
    },
    widgetColor: {
      type: String,
      default: '',
    },
    isUserBubble: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    title() {
      return this.isInProgress
        ? this.$t('COMPONENTS.FILE_BUBBLE.UPLOADING')
        : decodeURI(this.fileName);
    },
    fileName() {
      return this.url.substring(this.url.lastIndexOf('/') + 1);
    },
    accentStyle() {
      // eyun: 访客气泡改成主题色浅底 + 正文色(见 _conversation.scss): 图标与「下载」的主题色(深色模式提亮)在样式里算,
      // 这里只传主题色变量; 文件名跟正文色走, 不再取对比色白字
      return this.isUserBubble
        ? { '--eyun-widget-color': this.widgetColor }
        : {};
    },
  },
  methods: {
    openLink() {
      const win = window.open(this.url, '_blank');
      win.focus();
    },
  },
};
</script>

<template>
  <div
    class="file flex flex-row items-center p-3 cursor-pointer"
    :style="accentStyle"
  >
    <div class="icon-wrap">
      <FluentIcon icon="document" size="28" />
    </div>
    <div class="ltr:pr-1 rtl:pl-1">
      <div class="m-0 font-medium text-sm text-n-slate-12">
        {{ title }}
      </div>
      <div class="leading-none mb-1">
        <a
          class="download"
          rel="noreferrer noopener nofollow"
          target="_blank"
          :href="url"
        >
          {{ $t('COMPONENTS.FILE_BUBBLE.DOWNLOAD') }}
        </a>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.file {
  .icon-wrap {
    @apply text-[2.5rem] text-n-brand leading-none ltr:ml-1 rtl:mr-1 ltr:mr-2 rtl:ml-2;
  }

  .download {
    @apply text-n-brand font-medium p-0 m-0 text-xs no-underline;
  }
}
</style>
