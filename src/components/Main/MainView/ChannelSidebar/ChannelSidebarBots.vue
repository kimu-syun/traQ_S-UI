<template>
  <sidebar-content-container v-if="botUserIds.length > 0" title="参加BOT">
    <channel-sidebar-member-icons :viewer-states="viewStates" />
  </sidebar-content-container>
</template>

<script lang="ts">
import { defineComponent, computed, PropType } from '@vue/composition-api'
import store from '@/store'
import { ChannelId } from '@/types/entity-ids'
import SidebarContentContainer from '@/components/Main/MainView/MainViewSidebar/SidebarContentContainer.vue'
import ChannelSidebarMemberIcons from './ChannelSidebarMemberIcons.vue'

export default defineComponent({
  name: 'ChannelSidebarBots',
  components: {
    ChannelSidebarMemberIcons,
    SidebarContentContainer
  },
  props: {
    channelId: { type: String as PropType<ChannelId>, required: true }
  },
  setup(props) {
    const botUserIds = computed(() => store.state.domain.messagesView.bots)
    const viewStates = computed(() =>
      botUserIds.value.map(id => ({
        user: store.state.entities.users[id],
        active: true
      }))
    )
    return { botUserIds, viewStates }
  }
})
</script>

<style lang="scss" module></style>
