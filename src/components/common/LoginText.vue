<template>
    <div>
        <van-field
        :label="label"
        :type="type"
        :placeholder="placeholder"
        v-model="content"
        />
    </div>
</template>

<script>
export default {
  data () {
    return {
      content: ''
    }
  },
  props: ['label', 'type', 'placeholder', 'rule'],
  // 判断传入数据是否满足正则
  methods: {
    handlerulg () {
      const rue = new RegExp(this.rule)
      if (rue.test(this.content)) {
        this.$emit('inputChange', this.content)
      }
    }
  },
  watch: {
    content () {
      this.handlerulg()
    }
  }
}
</script>

<style>

</style>
