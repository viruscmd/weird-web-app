<template>
  <nav class="panel" :class="type">
    <p class="panel-heading">
      {{title}}
    </p>
    <div class="panel-block">
      <p class="control has-icons-left">
        <input class="input" type="text" placeholder="Search" v-model.lazy="panelSearchQuery">
        <span class="icon is-left">
          <i class="mdi mdi-magnify" aria-hidden="true"></i>
        </span>
      </p>
    </div>
    <n-link class="panel-block is-active" v-for="(item, key) in filteredItems" :key="key" :to='item.path'>
      {{item.name}}
    </n-link>
  </nav>
</template>

<script>
  export default {
    data() {
      return {
        panelSearchQuery: ''
      }
    },
    props: {
      title: {
        type: String,
        required: true
      },
      items: {
        type: Array,
        required: true
      },
      type: {
        type: String
      }
    },
    computed: {
      filteredItems () {
        if (!this.panelSearchQuery) return this.items

        return this.items.filter(x => x.name.toLowerCase() == this.panelSearchQuery.toLowerCase())
      },
    },
    mounted() {
      this.items = this.items.filter(x => x.name != 'index')
    }
  }

</script>
