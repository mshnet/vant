# ActionSheet

### Install

``` javascript
import Vue from 'vue';
import { ActionSheet } from 'vant';

Vue.use(ActionSheet);
```

## Usage

### Basic Usage

Use `actions` prop to set options of action-sheet. 

```html
<van-action-sheet
  v-model="show"
  :actions="actions"
  @select="onSelect"
/>
```

```javascript
export default {
  data() {
    return {
      show: false,
      actions: [
        { name: 'Option' },
        { name: 'Option' },
        { name: 'Option', subname: 'Description' }
      ]
    };
  },

  methods: {
    onSelect(item) {
      this.show = false;
      Toast(item.name);
    }
  }
}
```

### Status

```html
<van-action-sheet
  v-model="show"
  :actions="actions"
/>
```

```javascript
export default {
  data() {
    return {
      show: false,
      actions: [
        { name: 'Option', color: '#07c160' },
        { loading: true },
        { name: 'Disabled Option', disabled: true }
      ]
    };
  }
}
```

### ActionSheet with cancel button

```html
<van-action-sheet
  v-model="show"
  :actions="actions"
  cancel-text="Cancel"
  @select="onSelect"
  @cancel="onCancel"
/>
```

### ActionSheet with title

```html
<van-action-sheet v-model="show" title="Title">
  <p>Content</p>
</van-action-sheet>
```

## API

### Props

| Attribute | Description | Type | Default | Version |
|------|------|------|------|------|
| actions | Options | *Action[]* | `[]` | - |
| title | Title | *string* | - | - |
| cancel-text | Text of cancel button | *string* | - | - |
| overlay | Whether to show overlay | *boolean* | `true` | - |
| round | Whether to show round corner | *boolean* | `false` | 2.0.9 |
| close-on-click-action | Whether to close when click action | *boolean* | `false` | - |
| close-on-click-overlay | Whether to close when click overlay | *boolean* | `true` | - |
| lazy-render | Whether to lazy render util appeared | *boolean* | `true` | - |
| lock-scroll | Whether to lock background scroll | *boolean* | `true` | - |
| duration | Transition duration, unit second | *number* | `0.3` | 2.0.3 |
| get-container | Return the mount node for action-sheet | *string \| () => Element* | - | - |
| safe-area-inset-bottom | Whether to enable bottom safe area adaptation | *boolean* | `true` | - |

### Events

| Event | Description | Arguments |
|------|------|------|
| select | Triggered when click option | item, index |
| cancel | Triggered when cancel click | - |
| click-overlay | Triggered when click overlay | - |
| open | Triggered when open ActionSheet | - |
| opened | Triggered when opened ActionSheet | - |
| close | Triggered when close ActionSheet | - |
| closed | Triggered when closed ActionSheet | - |

### Data Structure of Action

| Key | Description | Type |
|------|------|------|
| name | Title | *string* |
| subname | Subtitle | *string* |
| color | Text color | *string* |
| className | className for the option | *any* |
| loading | Whether to be loading status | *boolean* |
| disabled | Whether to be disabled | *boolean* |
