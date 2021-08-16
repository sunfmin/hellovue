<template>
  <div class="helloworld">
    <div class="a">
      <input :value="value1" @input="onInput($event)"/>
      {{value1}}
    </div>
    
    <div class="b">
      <input v-model="value2"/>
      {{value2}}
    </div>

    <div class="c">
      <input v-fieldname='"value3"'/>
      {{value3}}
    </div>

    <div class="d">
      <v-text-field v-fieldname='"value4"'/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  directives: {
    fieldname: {
      inserted: function(el, binding, vnode) {
        console.log(el, binding, vnode)
        console.log("vnode.context.$el", vnode.context.$el)
        console.log("vnode.context", vnode.context)
        console.log("this", this)

        vnode.context.$on("test", function(evt) {
          console.log("test evt", evt)
        })

        if (vnode.componentInstance) {
          vnode.componentInstance.$on("input", function(value) {
            console.log("componentInstance evt", value)
          })
        }

      }
    }
  },
  methods: {

    onInput: function(evt) {
      console.log("this", this)

      // console.log("this.$listeners", this.$listeners)
      // console.log("evt", evt)
      this.$emit("input", evt.target.value)
      this.$emit("test", "123")
      // this.value1 = evt.target.value
    },
  },
  data: function() {
    return {
      value1: "123",
      value2: "",
      value3: "",
      value4: "222"
    }
  }
}
</script>
