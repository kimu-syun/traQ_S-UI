<template>
  <div :class="$style.container">
    <icon
      :class="$style.icon"
      mdi
      name="chevron-double"
      width="28"
      height="28"
      @click="open"
    />
    <user-icon-ellipsis-list
      direction="col"
      transition="fade-bottom"
      show-count
      :user-ids="viewerIds"
      :class="$style.rest"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from '@vue/composition-api'
import Icon from '@/components/UI/Icon.vue'
import UserIconEllipsisList from '@/components/UI/UserIconEllipsisList.vue'
import { UserId } from '@/types/entity-ids'

export default defineComponent({
  name: 'ChannelSidebarHidden',
  props: {
    viewerIds: { type: Array as PropType<UserId[]>, default: [] }
  },
  components: { Icon, UserIconEllipsisList },
  setup(props, context) {
    const open = () => {
      context.emit('open')
    }
    return {
      open
    }
  }
})
</script>

<style lang="scss" module>
.container {
  @include color-ui-primary;
  display: flex;
  flex-direction: column;
  width: 56px;
  height: 100%;
  align-items: center;
}

.icon {
  margin-bottom: 16px;
  margin-top: 16px;
  cursor: pointer;
}
.rest {
  @include color-ui-secondary;
}
</style>
