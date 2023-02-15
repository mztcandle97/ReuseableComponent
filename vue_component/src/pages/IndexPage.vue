<template>
  <q-page>
    <h3 class="q-pa-lg">Button Component</h3>
    <q-card class="container">
      <div class="flex-row">
        <div class="flex-col">
          <BaseBtn label="Action" icon="arrow_right" type="primary" size="lg" />
        </div>
        <div class="flex-col">
          <BaseBtn
            label="Action"
            icon-right="arrow_right"
            type="primary"
            size="lg"
          />
        </div>
        <div class="flex-col">
          <BaseBtn label="Action" type="primary" size="md" />
        </div>
        <div class="flex-col">
          <BaseBtn label="" icon="arrow_right" type="primary" size="sm" />
        </div>
      </div>
      <div class="flex-row q-pa-md">
        <div class="flex-col">
          <BaseBtn
            label="Action"
            icon="chevron_left"
            type="secondary"
            size="lg"
          />
        </div>
        <div class="flex-col">
          <BaseBtn
            icon-right="arrow_right"
            label="Action"
            type="secondary"
            size="lg"
          />
        </div>
        <div class="flex-col">
          <BaseBtn label="Action" type="secondary" size="md" />
        </div>
        <div class="flex-col">
          <BaseBtn label="" icon="arrow_right" type="secondary" />
        </div>
      </div>
    </q-card>
    <h3 class="q-pa-lg">Alerts and Notification</h3>
    <q-card class="container">
      <div class="flex-row">
        <div class="flex-col">
          <BaseBtn
            label="All"
            type="primary"
            size="md"
            @click="showAll = true"
          />
        </div>
        <div class="flex-col">
          <BaseBtn
            label="Content Only"
            type="primary"
            size="md"
            @click="showContent = true"
          />
        </div>
        <div class="flex-col">
          <BaseBtn
            label="Title and Content"
            type="primary"
            size="md"
            @click="showTitleContent = true"
          />
        </div>
        <div class="flex-col">
          <BaseBtn
            label="Title Only"
            type="primary"
            size="md"
            @click="showTitle = true"
          />
        </div>
      </div>
    </q-card>
  </q-page>

  <BaseAlert v-model="showAll">
    <template #header> A short descriptive header </template>
    <template #body>
      <div class="text-center">
        This is a paragraph of information with additional supporting detail or
        links to help the user understand what they should do.
      </div>
    </template>
    <template #buttons>
      <BaseBtn label="Action" type="secondary" size="md" />
      <BaseBtn label="Action" type="primary" size="md" />
    </template>
  </BaseAlert>
  <BaseAlert v-model="showContent">
    <template #body>
      <div class="text-center">
        This is a paragraph of information with additional supporting detail or
        links to help the user understand what they should do.
      </div>
    </template>
  </BaseAlert>
  <BaseAlert v-model="showTitleContent">
    <template #header> A short descriptive header </template>
    <template #body>
      <div class="text-center">
        This is a paragraph of information with additional supporting detail or
        links to help the user understand what they should do.
      </div>
    </template>
  </BaseAlert>
  <BaseAlert v-model="showTitle">
    <template #header> A short descriptive header </template>
  </BaseAlert>
</template>
<script>
import BaseBtn from 'src/components/BaseBtn.vue';
import BaseAlert from 'src/components/BaseAlert.vue';

export default {
  components: {
    BaseBtn,
    BaseAlert,
  },
  data() {
    return {
      showAll: false,
      showContent: false,
      showTitleContent: false,
      showTitle: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  margin: auto;
  width: 50%;
  padding: 10px;
}
.flex-row {
  display: flex;
  @media screen and (min-width: 768px) {
    flex: 1;
    flex-direction: row;
    justify-content: space-between;
  }
}
.flex-col {
  margin: 6px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
  flex-direction: column;
  color: white;
}
.next-btn {
  width: 200px;

  .q-btn .q-icon {
    margin: 0;
  }
}
.action-btn {
  flex: 0 1 175px;
}
</style>
