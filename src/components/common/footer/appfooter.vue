<template>
  <footer class="footer">
    <template v-if="$props.workoutStarted && !$props.workoutComplete">
      <!-- <div class="btn-pause">Pause</div> -->
      <div class="btn-stop" @click="handleClick">Close Workout</div>
    </template>
    <template v-else>
      <div class="btn-details" @click="handleHome">
        <IconView icon="icon-home" />
      </div>
      <div class="btn-details" @click="handleHistory"><IconView icon="icon-history" :width="24" /></div>
      <div class="btn-details" @click="handleSetting"><IconView icon="icon-cog" /></div>
      <div class="btn-details" @click="handleInfo"><IconView icon="icon-flickr" /></div>
    </template>
  </footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import IconView from '@/components/common/iconview/IconView.vue';
import { useRouter } from 'vue-router';
import { ROUTES } from '@/router/constants';

export default defineComponent({
  name: 'appfooter',
  emits: ['reset-workout'],
  components: {
    IconView,
  },
  props: {
    workoutStarted: {
      type: Boolean,
      default: false,
    },
    workoutComplete: {
      type: Boolean,
      default: false,
    },
  },
  setup(props, { emit }) {
    const router = useRouter();
    /**
     * emit reset workout event
     */
    const handleClick = (): void => {
      emit('reset-workout');
    };

    /**
     * emit reset workout event
     */
    const handleSetting = (): void => {
      router.push({
        name: ROUTES.SETTING.name,
      });
    };

    /**
     * emit reset workout event
     */
    const handleHome = (): void => {
      router.push({
        name: ROUTES.HOME.name,
      });
    };

    /**
     * emit reset workout event
     */
    const handleHistory = (): void => {
      router.push({
        name: ROUTES.WORKOUTHISTORY.name,
      });
    };

    /**
     * emit reset workout event
     */
    const handleInfo = (): void => {
      router.push({
        name: ROUTES.INFO.name,
      });
    };

    return {
      handleClick,
      handleHome,
      handleSetting,
      handleHistory,
      handleInfo,
    };
  },
});
</script>

<style scoped lang="postcss">
@import '@css/app.css';
.footer {
  position: fixed;
  bottom: 0px;
  width: 100%;
  align-items: center;
  justify-content: center;
  display: flex;
  .btn-pause,
  .btn-stop,
  .btn-details {
    border-top: 1px solid $black-2;
    flex: 1;
    text-align: center;
    padding: 16px;
    background-color: $black-1;
    color: $white;
  }
  .btn-pause,
  .btn-details:not(:last-child) {
    border-right: 1px solid $black-2;
  }
}
</style>
