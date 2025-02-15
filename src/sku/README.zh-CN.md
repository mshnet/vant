# Sku 商品规格

### 引入

```javascript
import Vue from 'vue';
import { Sku } from 'vant';

Vue.use(Sku);
```

## 代码演示

### 基础用法

```html
<van-sku
  v-model="show"
  :sku="sku"
  :goods="goods"
  :goods-id="goodsId"
  :quota="quota"
  :quota-used="quotaUsed"
  :hide-stock="sku.hide_stock"
  :message-config="messageConfig"
  @buy-clicked="onBuyClicked"
  @add-cart="onAddCartClicked"
/>
```

```js
export default {
  data() {
    return {
      show: false,
      sku: {
        // 数据结构见下方文档
      },
      goods: {
        // 数据结构见下方文档
      },
      messageConfig: {
        // 数据结构见下方文档
      }
    };
  }
}
```

### 自定义步进器

```html
<van-sku
  v-model="show"
  :sku="sku"
  :goods="goods"
  :goods-id="goodsId"
  :quota="quota"
  :quota-used="quotaUsed"
  :hide-stock="sku.hide_stock"
  :custom-stepper-config="customStepperConfig"
  @buy-clicked="onBuyClicked"
  @add-cart="onAddCartClicked"
/>
```

### 高级用法

```html
<van-sku
  v-model="show"
  stepper-title="我要买"
  :sku="sku"
  :goods="goods"
  :goods-id="goodsId"
  :quota="quota"
  :quota-used="quotaUsed"
  :hide-stock="sku.hide_stock"
  show-add-cart-btn
  reset-stepper-on-hide
  :initial-sku="initialSku"
  @buy-clicked="onBuyClicked"
  @add-cart="onAddCartClicked"
>
  <!-- 自定义 sku-header-price -->
  <template slot="sku-header-price" slot-scope="props">
    <div class="van-sku__goods-price">
      <span class="van-sku__price-symbol">￥</span><span class="van-sku__price-num">{{ props.price }}</span>
    </div>
  </template>

  <!-- 自定义 sku actions -->
  <template slot="sku-actions" slot-scope="props">
    <div class="van-sku-actions">
      <van-button
        square
        size="large"
        type="warning"
        @click="onPointClicked"
      >
        积分兑换
      </van-button>
      <!-- 直接触发 sku 内部事件，通过内部事件执行 onBuyClicked 回调 -->
      <van-button
        square
        size="large"
        type="danger"
        @click="props.skuEventBus.$emit('sku:buy')"
      >
        买买买
      </van-button>
    </div>
  </template>
</van-sku>
```

## API

### Props

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|------|------|------|------|------|
| v-model | 是否显示sku | *boolean* | `false` | - |
| sku | 商品sku数据 | *object* | - | - |
| goods | 商品信息 | *object* | - | - |
| goods-id | 商品 id | *string \| number* | - | - |
| price-tag | 显示在价格后面的标签 | *string* | - | - |
| hide-stock | 是否显示商品剩余库存 | *boolean* | `false` | - |
| hide-quota-text | 是否显示限购提示 | *boolean* | `false` | - |
| hide-selected-text | 是否隐藏已选提示 | *boolean* | `false` | - |
| stock-threshold | 库存阈值。低于这个值会把库存数高亮显示 | *boolean* | `50` | - |
| show-add-cart-btn | 是否显示加入购物车按钮 | *boolean* | `true` | - |
| buy-text | 购买按钮文字 | *string* | `立即购买` | - |
| add-cart-text | 加入购物车按钮文字 | *string* | `加入购物车` | - |
| quota | 限购数，0 表示不限购 | *number* | `0` | - |
| quota-used | 已经购买过的数量 | *number* | `0` | - |
| reset-stepper-on-hide | 隐藏时重置选择的商品数量 | *boolean* | `false` | - |
| reset-selected-sku-on-hide | 隐藏时重置已选择的 sku | *boolean* | `false` | - |
| disable-stepper-input | 是否禁用步进器输入 | *boolean* | `false` | - |
| close-on-click-overlay | 是否在点击遮罩层后关闭 | *boolean* | `false` | - |
| stepper-title | 数量选择组件左侧文案 | *string* | `购买数量` | - |
| custom-stepper-config | 步进器相关自定义配置 | *object* | `{}` | - |
| message-config | 留言相关配置 | *object* | `{}` | - |
| get-container | 指定挂载的节点，可以传入选择器，<br>或一个返回节点的函数 | *string \| () => Element* | - | - |
| initial-sku | 默认选中的 sku，具体参考高级用法 | *object* | `{}` | - |
| show-soldout-sku | 是否展示售罄的 sku，默认展示并置灰 | *boolean* | `true` | - |
| safe-area-inset-bottom | 是否开启底部安全区适配，[详细说明](#/zh-CN/quickstart#di-bu-an-quan-qu-gua-pei) | *boolean* | `false` | 2.2.1 |

### Events

| 事件名 | 说明 | 回调参数 |
|------|------|------|
| add-cart | 点击添加购物车回调 | skuData: object |
| buy-clicked | 点击购买回调 | skuData: object |
| stepper-change | 购买数量变化时触发 | value: number |
| sku-selected | 切换规格类目时触发 | { skuValue, selectedSku, selectedSkuComb } |
| open-preview | 打开商品图片预览时触发 | data: object |
| close-preview | 关闭商品图片预览时触发 | data: object |

### 方法

通过 ref 可以获取到 sku 实例并调用实例方法

| 方法名 | 说明 | 参数 | 返回值 |
|------|------|------|------|
| getSkuData | 获取当前 skuData | - | skuData |

### Slots

Sku 组件默认划分好了若干区块，这些区块都定义成了插槽，可以按需进行替换。区块顺序见下表：

| 名称 | 说明 |
|------|------|
| sku-header | 商品信息展示区，包含商品图片、名称、价格等信息 |
| sku-header-price | 自定义 sku 头部价格展示 |
| sku-header-origin-price | 自定义 sku 头部原价展示 |
| sku-header-extra | 额外 sku 头部区域 |
| sku-body-top |  sku 展示区上方的内容，无默认展示内容，按需使用 |
| sku-group | 商品 sku 展示区 |
| extra-sku-group | 额外商品 sku 展示区，一般用不到 |
| sku-stepper | 商品数量选择区 |
| sku-messages | 商品留言区 |
| sku-actions | 操作按钮区 |

### sku 对象结构

```javascript
sku: {
  // 所有sku规格类目与其值的从属关系，比如商品有颜色和尺码两大类规格，颜色下面又有红色和蓝色两个规格值。
  // 可以理解为一个商品可以有多个规格类目，一个规格类目下可以有多个规格值。
  tree: [
    {
      k: '颜色', // skuKeyName：规格类目名称
      v: [
        {
          id: '30349', // skuValueId：规格值 id
          name: '红色', // skuValueName：规格值名称
          imgUrl: 'https://img.yzcdn.cn/1.jpg' // 规格类目图片，只有第一个规格类目可以定义图片
        },
        {
          id: '1215',
          name: '蓝色',
          imgUrl: 'https://img.yzcdn.cn/2.jpg'
        }
      ],
      k_s: 's1' // skuKeyStr：sku 组合列表（下方 list）中当前类目对应的 key 值，value 值会是从属于当前类目的一个规格值 id
    }
  ],
  // 所有 sku 的组合列表，比如红色、M 码为一个 sku 组合，红色、S 码为另一个组合
  list: [
    {
      id: 2259, // skuId，下单时后端需要
      price: 100, // 价格（单位分）
      s1: '1215', // 规格类目 k_s 为 s1 的对应规格值 id
      s2: '1193', // 规格类目 k_s 为 s2 的对应规格值 id
      s3: '0', // 最多包含3个规格值，为0表示不存在该规格
      stock_num: 110 // 当前 sku 组合对应的库存
    }
  ],
  price: '1.00', // 默认价格（单位元）
  stock_num: 227, // 商品总库存
  collection_id: 2261, // 无规格商品 skuId 取 collection_id，否则取所选 sku 组合对应的 id
  none_sku: false, // 是否无规格商品
  messages: [
    {
      // 商品留言
      datetime: '0', // 留言类型为 time 时，是否含日期。'1' 表示包含
      multiple: '0', // 留言类型为 text 时，是否多行文本。'1' 表示多行
      name: '留言', // 留言名称
      type: 'text', // 留言类型，可选: id_no（身份证）, text, tel, date, time, email
      required: '1', // 是否必填 '1' 表示必填
      placeholder: '' // 可选值，占位文本
    }
  ],
  hide_stock: false // 是否隐藏剩余库存
}
```

### initialSku 对象结构

```javascript
{
  // 键：skuKeyStr（sku 组合列表中当前类目对应的 key 值）
  // 值：skuValueId（规格值 id）
  s1: '30349',
  s2: '1193',
  // 初始选中数量
  selectedNum: 3
}
```

### goods 对象结构

```javascript
goods: {
  // 商品标题
  title: '测试商品',
  // 默认商品 sku 缩略图
  picture: 'https://img.yzcdn.cn/1.jpg'
}
```

### customStepperConfig 对象结构

```javascript
customStepperConfig: {
  // 自定义限购文案
  quotaText: '每次限购xxx件',
  // 自定义步进器超过限制时的回调
  handleOverLimit: (data) => {
    const { action, limitType, quota, quotaUsed } = data;

    if (action === 'minus') {
      Toast('至少选择一件商品');
    } else if (action === 'plus') {
      // const { LIMIT_TYPE } = Sku.skuConstants;
      if (limitType === LIMIT_TYPE.QUOTA_LIMIT) {
        let msg = `单次限购${quota}件`;
        if (quotaUsed > 0) msg += `，你已购买${quotaUsed}`;
        Toast(msg);
      } else {
        Toast('库存不够了');
      }
    }
  },
  // 步进器变化的回调
  handleStepperChange: currentValue => {},
  // 库存
  stockNum: 1999,
  // 格式化库存
  stockFormatter: stockNum => {},
}
```

### messageConfig Data Structure

```javascript
messageConfig: {
  // 图片上传回调，需要返回一个promise，promise正确执行的结果需要是一个图片url
  uploadImg: () => {
    return new Promise((resolve) => {
      setTimeout(() => resolve('https://img.yzcdn.cn/upload_files/2017/02/21/FjKTOxjVgnUuPmHJRdunvYky9OHP.jpg!100x100.jpg'), 1000);
    });
  },
  // 最大上传体积 (MB)
  uploadMaxSize: 3,
  // placeholder 配置
  placeholderMap: {
    text: 'xxx',
    tel: 'xxx',
    ...
  }
}
```

### 添加购物车和点击购买回调函数接收的 skuData 对象结构

```javascript
skuData: {
  // 商品 id
  goodsId: '946755',
  // 留言信息
  messages: {
    message_0: '12',
    message_1: ''
  },
  // 另一种格式的留言，key 不同
  cartMessages: {
    '留言1': 'xxxx'
  },
  // 选择的商品数量
  selectedNum: 1,
  // 选择的 sku 组合
  selectedSkuComb: {
    id: 2257,
    price: 100,
    s1: '30349',
    s2: '1193',
    s3: '0',
    stock_num: 111
  }
}
```
