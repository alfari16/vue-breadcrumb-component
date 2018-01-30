<template>
    <div>
        <router-link to="/" tag="span" title="Home">&#127968;</router-link>
        <router-link tag="span" v-for="(v,i) in path" :to="v.full" :title="v.name" v-if="v.name" :key="i" class="default router-name">{{v.name}}</router-link>
    </div>
</template>

<script>
export default {
  data() {
    return {
      path: []
    };
  },
  watch: {
    $route(to, from) {
      const value = {
        full: to.fullPath,
        name: to.name
      };
      if (!value.name && to.params.name) value.name = to.params.name;
      this.path = this.path.filter(el => {
        return to.fullPath.includes(el.full) && to.fullPath !== el.full;
      });
      this.path.push(value);
    }
  }
};
</script>

<style lang="sass" scoped>
span
  cursor: pointer
  &:not(:first-child)
    &::before
      content: '/'
      display: inline-block
      margin: 0 5px      
</style>
