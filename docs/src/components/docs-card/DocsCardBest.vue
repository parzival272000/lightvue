<template>
  <div class="best__demo__wrapper" :id="computedId">
    <div class="wrapper__header">
      <h5 class="component__header" @click="$router.push({ hash: `#${computedId}` })"># {{ title }}</h5>
      <i class="light-icon-adjustments-horizontal dy-props__toggle-drawer" @click="showOptions()"></i>
    </div>
    <div class="dy-pg__wrap">
      <div class="dy-pg__left">
        <div class="dy-comp__wrap light-scrollbar">
          <slot></slot>
        </div>
        <div class="dy-code__wrap light-scrollbar">
          <CopyButton :text="getMarkup" />
          <slot name="code"></slot>
        </div>
      </div>
      <div class="dy-props__wrap" :class="`${showPorpsOptions ? '--mobile-show' : ''}`">
        <div class="dy-props__header">All Props</div>
        <div class="dy-props__body light-scrollbar">
          <slot name="props"></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CopyButton from '@/components/docs-card/CopyButton';
export default {
  data() {
    return {
      showPorpsOptions: false,
    };
  },
  props: {
    title: String,
    id: String,
    file: String,
  },
  computed: {
    computedId() {
      return this.$props.id ? this.$props.id : this.title.split(' ').join('-').toLowerCase();
    },
  },
  methods: {
    showOptions() {
      this.showPorpsOptions = !this.showPorpsOptions;
    },
    getMarkup() {
      return this.$el.querySelector('.dy-code__wrap').innerText;
    },
  },
  components: {
    CopyButton,
  },
};
</script>

<style lang="scss">
.best__demo__wrapper {
  box-shadow: 0px 0px 2px 1px rgba(0, 0, 0, 0.15);
  background: #ffffff;
  margin-bottom: 30px;
  width: 100%;
  position: relative;
}
.dy-pg__wrap {
  display: flex;
  justify-content: space-between;
  position: relative;
  /* margin-bottom: ; */
  /* border: 1px solid #cccccc; */
  /* justify-content: space-between; */
}

.dy-pg__left {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  max-height: 60vh;
  align-items: stretch;
  overflow: hidden;
}

.dy-props__wrap {
  width: 300px;
  max-height: 60vh;
  background: #ffffff;
  /* padding: 20px; */
  transition: all 0.2s ease-in-out;
  border-left: 2px solid #edf2f6;
  .dy-props__header {
    padding: 22px;
    border-bottom: 1px solid #edf2f6;
    font-weight: 600;
    font-size: 1em;
    color: #008080;
  }

  .dy-props__body {
    padding: 20px;
    overflow-y: scroll;
    height: calc(100% - 62px);
    background: #ffffff;
    //   height: 350px;
  }
}

.wrapper__header {
  display: flex;
  width: 100%;
  padding: 10px;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #edf2f6;
  .component__header {
    padding: 20px;
    color: teal;
    font-size: 18px;
    font-weight: bold;
    border: 1px solid #edf2f6;
    margin: 0px;
    white-space: nowrap;
    margin-left: -22px;
    padding: 8px 16px 8px 24px;
    background: #dfe7eb;
    color: #607b89;
    position: relative;
    cursor: pointer;
    border-radius: 6px 20px 20px 0;
    box-shadow: 1px 2px 4px -1px rgba(0, 0, 0, 0.4);
  }
  h5::after {
    content: '';
    position: absolute;
    top: 100%;
    left: 0;
    width: 0;
    height: 0;
    border: 0 solid transparent;
    border-top-color: #bdc7cf;
    border-width: 10px 0 0 12px;
    z-index: -1;
    margin: 0px;
  }
}

.dy-comp__wrap {
  flex-grow: 1;
  min-height: 200px;
  // display: flex;
  overflow-y: auto;
  justify-content: center;
  width: 100%;
  padding: 48px;
  background: #ffffff;
}

.dy-props__toggle-drawer {
  display: none;
  cursor: pointer;
}

.dy-code__wrap {
  display: flex;
  flex-direction: column;
  line-height: 1.5;
  overflow: auto;
  position: relative;
  // padding: 5px;
  pre {
    color: #2f9c0a;
    span {
      color: #1990b8;
    }
  }
  .dy-code-row {
    &.--tag-row {
      color: #c92c2c;
      padding-left: 16px;
    }
    &.--empty-row {
      height: 20px;
      min-height: 4px;
    }
    &:nth-child(even) {
      background-color: #f6f9fc;
    }
    &:nth-child(odd) {
      background-color: #ffffff;
    }
  }
}

@media (max-width: 975px) {
  .dy-props__wrap {
    display: none;
    &.--mobile-show {
      position: absolute;
      z-index: 900;
      display: block;
      height: 100%;
      width: 100%;
    }
  }

  .dy-comp__wrap {
    padding: 16px;
  }

  .dy-props__toggle-drawer {
    display: block;
  }
}
</style>
