<template>
  <docs-page-layout :title="$options.title" :description="$options.description">
    <docs-card-vue title="Shadow styles" file="card/CardShadowDemo" />
    <docs-card-vue title="Border radius" file="card/CardRadiusDemo" />
    <docs-card-vue title="Background color and Padding" file="card/CardPaddingAndBGcolorDemo" />
    <docs-card-vue title="Enabling border" file="card/CardBorderDemo" />
    <template #api>
      <getting-started :package-name="$options.packageName" :component-name="$options.componentName" />
      <docs-all-api :api-data="$options.apiData" />
    </template>
  </docs-page-layout>
</template>

<script>
import DocsPageLayout from '@/components/docs-card/DocsPageLayout.vue';
import DocsCardVue from '@/components/docs-card/DocsCardVue.vue';
import DocsCard from '@/components/docs-card/DocsCard.vue';
import GettingStarted from '@/components/docs-card/GettingStarted.vue';
import DocsAllApi from '@/components/docs-card/DocsAllApi.vue';
import CardAPI from 'lightvueDocs/example/card/CardAPI';

export default {
  components: {
    DocsCardVue,
    DocsCard,
    GettingStarted,
    DocsPageLayout,
    DocsAllApi,
  },
  title: 'Card',
  description: `Card components can be used as flexible containers/wrappers for other UI elements.`,
  packageName: 'card',
  componentName: 'LvCard',
  apiData: CardAPI,
};
</script>
