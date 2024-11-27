# Vue Components Library By clice 
# Index


# How to Use
## OptionFilter
#### 1. Import the component
```js
import OptionFilter from '@components/OptionFilter.vue';// someday.. it will be at "clice-vue-component"; 
```

#### 2.declare the component
```js
export default {
  name: 'StateManagement',
  components: {
    OptionFilter,
  },
```

don't forget to declare `Select Options`

```js
data() {
    return {
      selectOptions: [
        { value: '11', text: '서울특별시' },
        { value: '21', text: '부산광역시' },
        { value: '22', text: '대구광역시' },
        { value: '23', text: '인천광역시' },
        { value: '24', text: '광주광역시' },

      ],
```


```js
    const selectedState = ref('');

```
#### 3. Use it

```js
 <OptionFilter label="거주 지역" :options="selectOptions" v-model="selectedState" />

```

#### 4. Don't forget to return the name of `v-model` 
```js
export default {
  setup(){
    return {
      selectedState, //선택된 값을 반환하여 다른 메소드에서 접근 가능하도록 함
    };
  },

};
```
