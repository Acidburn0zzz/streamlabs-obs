<template>
<modal-layout :showControls="false">
  <div slot="content">

    <h4 v-if="!notificationsCount">
      {{ $t('You don\'t have any notifications') }}
    </h4>

    <div v-for="(notificationsService, groupName) in notificationGroups" :key="groupName">
      <h4 v-if="notificationsService.length">
        {{ groupName === 'unread' ? $t('New Notifications') : $t('Log') }}
      </h4>
      <div
        class="notification"
        v-for="notify in notificationsService"
        :key="notify.id"
        @click="onNotificationClickHandler(notify.id)"
        :class = "{
          'unread': notify.unread,
          'has-action': notify.action
        }"
      >
        <div class="icon">
          <span class="fa fa-info-circle" v-if="notify.type == 'INFO'"></span>
          <span class="fa fa-warning" v-if="notify.type == 'WARNING'"></span>
        </div>
        <div class="message">{{ notify.message }}</div>
        <div class="date">{{ moment(notify.date) }}</div>

      </div>
    </div>
  </div>

</modal-layout>
</template>

<script lang="ts" src="./Notifications.vue.ts"></script>

<style lang="less" scoped>
@import "../../styles/index";

.notification {
  color: var(--icon);
  padding: 5px 10px;
  margin-bottom: 5px;
  display: grid;
  grid-template-columns: 30px 1fr 130px;
  background: var(--hover);
  .border();

  &.has-action:hover {
    color: var(--title);
    background: var(--section);
    cursor: pointer;
  }

  &:last-child {
    margin-bottom: 20px;
  }

  .fa-warning {
    color: var(--warning);
  }

  .date {
    text-align: right;
  }
}
</style>
