<template>
  <div
    :class="['row', classes]"
    :style="styles">
    <slot></slot>
  </div>
</template>

<script>
/* eslint-disable vue/no-unused-properties */

export default {
  name: 'sl-row',
  props: {
    row: {
      type: [Number, String],
      default: ''
    },
    sm: {
      type: [Number, String],
      default: ''
    },
    md: {
      type: [Number, String],
      default: ''
    },
    lg: {
      type: [Number, String],
      default: ''
    },
    xl: {
      type: [Number, String],
      default: ''
    },
    noGutters: {
      type: Boolean,
      default: false
    },
    noWrap: {
      type: Boolean,
      default: false
    },
    flexGrow: {
      type: [Number, String],
      default: -1
    }
  },
  computed: {
    classes () {
      const list = []
      const props = this._props
      const classes = Object.keys(props)
        .filter((prop) => props[prop] && !['noGutters', 'noWrap', 'fullHeight'].includes(prop))
      classes.forEach((option) => list.push(`${option}-${props[option]}`))
      if (this.fullHeight) list.push('full-height')
      if (this.noGutters) list.push('row-flush')
      if (this.noWrap) list.push('row-nowrap')
      return list.map((className) => className
        .replace(/([a-z])([A-Z])/g, '$1-$2')
        .toLowerCase()).join(' ')
    },
    styles () {
      const styles = {}
      if (this.flexGrow >= 0) styles.flex = `${this.flexGrow} 0 auto`
      return styles
    }
  }
}
</script>

<style lang="scss" scoped>
.row-nowrap {
  flex-wrap: nowrap;
}
</style>
