<template>
  <DemoWalkthroughPageLayout :drawArrows="drawArrows">
    <h1 class="heading">
      Shoppers
    </h1>

    <p>
      To showcase how Amazon Personalize tailors course recommendations based on a student’s historical and real time
      click-through behavior, the EdTech Demo includes several fictitious students, each with different course
      preferences.
    </p>

    <div :class="{ 'images mt-5': true, 'images--mobile': isMobile }">
      <div ref="switch-shoppers-text" class="switch-shoppers-text">
        Switch students by clicking on the student details located next to the shopping cart icon. Top right corner.
      </div>

      <div class="switch-shoppers">
        <img
          :src="isMobile ? '/switch-shoppers-mobile.png' : '/switch-shoppers-desktop.png'"
          alt=""
          class="img-fluid"
          ref="switch-shoppers-img"
        />
      </div>

      <div class="select-shoppers-text">
        <p>
          This demo allows you to select students from the store students' dataset, based on age and course preferences.
        </p>

        <p>
          For an optimal demo experience, switch students at least twice to see the different course recommendations
          each student receives.
        </p>
      </div>

      <div class="select-shoppers"><img src="/select-shoppers.png" alt="" class="img-fluid" /></div>
    </div>
  </DemoWalkthroughPageLayout>
</template>

<script>
import { mapState } from 'vuex';
import DemoWalkthroughPageLayout from '../DemoWalkthroughPageLayout';

export default {
  name: 'DemoWalkthroughShoppersPage',
  components: { DemoWalkthroughPageLayout },
  computed: {
    ...mapState({ isMobile: (state) => state.modal.isMobile }),
  },
  data() {
    return {
      drawArrows: {
        desktop: [
          {
            from: { ref: 'switch-shoppers-text', target: ({ left, top }) => [left + 20, top] },
            to: { ref: 'switch-shoppers-img', target: ({ right, width, top }) => [right - width * 0.2, top + 10] },
            drawPoints: ({ fromX, fromY, toX, toY }) => [
              [fromX, fromY],
              [fromX, fromY - 20],
              [toX, fromY - 20],
              [toX, toY],
            ],
          },
        ],
        mobile: [
          {
            from: { ref: 'switch-shoppers-text', target: 'LEFT' },
            to: { ref: 'switch-shoppers-img', target: ({ left, top, height }) => [left, top + height * 0.2] },
            drawPoints: ({ fromX, fromY, toX, toY }) => [
              [fromX, fromY],
              [Math.min(fromX, toX) - 20, fromY],
              [Math.min(fromX, toX) - 20, toY],
              [toX, toY],
            ],
          },
        ],
      },
    };
  },
};
</script>

<style scoped>
.heading {
  font-weight: normal;
  font-size: 1.75rem;
  color: var(--blue-500);
}

.images {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto;
  grid-gap: 20px;
  grid-template-areas:
    'Switch SwitchText'
    'Select SelectText';
}

.switch-shoppers {
  grid-area: Switch;
}

.switch-shoppers-text {
  grid-area: SwitchText;
  align-self: start;
}

.select-shoppers {
  grid-area: Select;
  justify-self: end;
}

.select-shoppers-text {
  grid-area: SelectText;
}

.images--mobile {
  grid-template-columns: 1fr;
  grid-template-rows: auto;
  grid-template-areas: 
    'SwitchText'
    'Switch'
    'SelectText'
    'Select'
  ;
}

.images--mobile .switch-shoppers-text {
  justify-self: end;
  width: 80%;
  padding-left: 16px;
}

.images--mobile .switch-shoppers {
  justify-self: end;
  max-width: 90%;
}

.images--mobile .select-shoppers-text {
  margin-top: 16px;
}

.images--mobile .select-shoppers {
  justify-self: center;
  width: 80%;
  max-width: none;
}

.select-shoppers .img-fluid {
  width: 100%;
}
</style>
