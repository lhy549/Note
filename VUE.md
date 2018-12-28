## VUE

### VUE 指令
* v-text
* v-html
* v-show
* v-if
* v-else
* v-else-if
* v-for
* v-on
* v-bind
* v-model
* v-pre
* v-cloak
* v-once

### 选项

    new Vue({
        // 数据选项
        data,
        props,
        prosData,
        computed,
        watch,
        methods,
    
        // DOM选项
        el,
        template,
        render,
        rederError,
    
        // 生命周期
        beforeCreate,
        created,
        beforeMount,
        mouted,
        beforeUpdate,
        updated,
        //..
    
        // 资源
        directives,
        filters,
        components,
    
        // 组合关系
        parent,
        mixins,
        extends,
        provice/inject,
    
        // 其他
        name/delimeters/functional/model/inheritAttrs/comments
    });

### 实例属性、方法、事件的使用
    new Vue({
        mounted() {
            // 属性
            console.log(this.$data, $this.props, $this.attrs);
            console.log(this.$slots, $scopedSlots);
            console.log(this.$el, this.$options, this.$listeners, this.$refs);
            console.log(this.$parent, this.$root, this.children);
    
            // 方法
            this.$watch(...);
            this.$set(...);
            this.$delete(...);
    
            // 事件
            this.$on();
            this.$once();
            this.$off();
            this.$emit();
    
            // 触发生命周期
            this.$mount();
            this.$forceUpdate();
            this.$nextTick();
            this.$destroy();
        }
    });