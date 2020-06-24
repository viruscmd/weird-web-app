<template>
  <section class="section">
    <div class="columns is-desktop">
      <div class="column">
        <h1 class="subtitle has-text-grey-light">About</h1>
        <h2 class="title">Weird Web Apps</h2>

        <p>
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Earum cum magnam, voluptate dolorem sequi explicabo
          voluptates consequuntur, voluptatem, autem accusamus aliquam laborum maiores totam. Sit est velit et ut
          officia.
        </p>
      </div>
      <div class="column is-size-4-desktop">
        <Panel title="Apps" :items="this.$router.options.routes"/>
      </div>
    </div>
  </section>
</template>

<script>
  import Panel from '~/components/Panel'

  export default {
    name: 'HomePage',

    components: {
      Panel
    }
  }

</script>
