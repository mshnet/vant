<template>
  <demo-section>
    <demo-block :title="$t('basicUsage')">
      <van-button type="primary" @click="show1 = true">{{ $t('buttonText') }}</van-button>
      <van-action-sheet v-model="show1" :actions="simpleActions" @select="onSelect" />
    </demo-block>

    <demo-block :title="$t('status')">
      <van-button type="primary" @click="show2 = true">{{ $t('buttonText') }}</van-button>
      <van-action-sheet v-model="show2" close-on-click-action :actions="statusActions" />
    </demo-block>

    <demo-block :title="$t('title2')">
      <van-button type="primary" @click="show3 = true">{{ $t('buttonText') }}</van-button>
      <van-action-sheet
        v-model="show3"
        :actions="simpleActions"
        close-on-click-action
        :cancel-text="$t('cancel')"
        @cancel="onCancel"
      />
    </demo-block>

    <demo-block :title="$t('title3')">
      <van-button type="primary" @click="show4 = true">{{ $t('buttonText') }}</van-button>
      <van-action-sheet v-model="show4" :title="$t('title')">
        <p>{{ $t('content') }}</p>
      </van-action-sheet>
    </demo-block>
  </demo-section>
</template>

<script>
import { GREEN } from '../../utils/constant';

export default {
  i18n: {
    'zh-CN': {
      buttonText: '弹出菜单',
      title2: '展示取消按钮',
      title3: '展示标题栏',
      status: '选项状态',
      description: '描述信息',
      disabledOption: '禁用选项'
    },
    'en-US': {
      buttonText: 'Show ActionSheet',
      title2: 'ActionSheet with cancel button',
      title3: 'ActionSheet with title',
      status: 'Status',
      description: 'Description',
      disabledOption: 'Disabled Option'
    }
  },

  data() {
    return {
      show1: false,
      show2: false,
      show3: false,
      show4: false
    };
  },

  computed: {
    simpleActions() {
      return [
        { name: this.$t('option') },
        { name: this.$t('option') },
        { name: this.$t('option'), subname: this.$t('description') }
      ];
    },

    statusActions() {
      return [
        { name: this.$t('option'), color: GREEN },
        { loading: true },
        { name: this.$t('disabledOption'), disabled: true }
      ];
    }
  },

  methods: {
    onSelect(item) {
      this.show1 = false;
      this.$toast(item.name);
    },

    onCancel() {
      this.$toast('cancel');
    }
  }
};
</script>

<style lang="less">
@import '../../style/var';

.demo-action-sheet {
  background-color: @white;

  .van-button {
    margin-left: @padding-md;
  }

  p {
    padding: 20px;
  }
}
</style>
