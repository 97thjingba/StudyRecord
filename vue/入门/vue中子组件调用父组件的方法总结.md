-   $emit
-   $parent
-   prop
-   vuex（vuex代码比较麻烦，不写了，说下步骤吧 dispatch：actions=>commit:mutations）

### $parent方法

**父组件**

```
<template>
  <div>
    <child></child>
  </div>
</template>
<script>
  import child from '@/components/child';
  export default {
    components: {
      child
    },
    methods: {
      fatherMethod() {
        console.log('father组件');
      }
    }
  }
</script>
复制代码
```

**子组件**

```
<template>
  <div @click="activeBtn"> </div>
</template>
<script>
  export default {
    methods: {
      activeBtn() {
        this.$parent.fatherMethod()
      }
    }
  }
</script>
复制代码
```

### $emit方法

**父组件**

```
<template>
  <div>
    <child @callFather="activeSon"></child>
  </div>
</template>
<script>
  import child from '@/components/child';
  export default {
    components: {
      child
    },
    methods: {
      fatherMethod() {
        console.log('father组件');
      },
      activeSon(){
        this.fatherMethod()
      }
    }
  }
</script>
复制代码
```

**子组件**

```
<template>
  <div @click="activeBtn"> </div>
</template>
<script>
  export default {
    methods: {
      activeBtn() {
        this.$emit("callFather")
      }
    }
  }
</script>
复制代码
```

### $prop方法

**父组件**

```
<template>
  <div>
    <child :activeSon="fatherMethod()"></child>
  </div>
</template>
<script>
  import child from '@/components/child';
  export default {
    components: {
      child
    },
    methods: {
      fatherMethod() {
        console.log('father组件');
      }
    }
  }
</script>
复制代码
```

**子组件**

```
<template>
  <div @click="activeBtn"> </div>
</template>
<script>
  export default {
  props:{
    activeSon:  {
        type: Function,
        default: null
      }
  },
    methods: {
      activeBtn() {
        this.activeSon()
      }
    }
  }
</script>
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ0ODI2Mzc2MV19
-->