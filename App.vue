
<template>

    <VueWheelSpinner
        ref="spinner"
        :slices="slices"
        :winner-index="defaultWinner"
        :cursor-angle="cursorAngle"
        :cursor-position="cursorPosition"
        :cursor-distance="cursorDistance"
        font="bold 26px Arial"
        textPosition="middle"
        @spin-start="onSpinStart"
        @spin-end="onSpinEnd">
  
      <template #cursor>
        <!-- <img class="cursor-img" :src="cursorImage" alt="Cursor"> -->
         Cursor
      </template>
  
      <template #default>
        <button
            class="spin-button"
            :disabled="isSpinning"
            @click="handleSpinButtonClick"
            @mouseover="handleSpinButtonHover"
            @mouseleave="handleSpinButtonLeave">
          Spin
        </button>
      </template>
  
    </VueWheelSpinner>
  
  </template>
  
  <script>
  import VueWheelSpinner from './src/components/VueWheelSpinner.vue'

  
    export default {
      components: {
        VueWheelSpinner
      },
      data() {
        return {
          winnerResult: null,
          slices: [
            {color: '#eb4d4b', text: 'Slice 1', textColor: '#fff'},
            {color: '#f0932b', text: 'Slice 2', textColor: '#f11'},
            {color: '#f9ca24', text: 'Slice 3', textColor: '#000'},
            {color: '#badc58', text: 'Slice 4', textColor: '#500'},
            {color: '#7ed6df', text: 'Slice 5', textColor: '#15f'},
            {color: '#e056fd', text: 'Slice 6', textColor: '#b22'}
          ],
          isSpinning: false,
          defaultWinner: 0,
          cursorAngle: 0,
          cursorPosition: 'edge',
          cursorDistance: 0
        };
      },
      methods: {
        playAudio(audio) {
          if (audio) {
            audio.volume = 0.5
            audio.play();
          }
        },
        handleSpinButtonClick() {
          if (this.buttonClickAudio) {
          }
          this.$refs.spinner.spinWheel(this.defaultWinner);
        },
        handleSpinButtonHover() {
          if (this.buttonHoverAudio) {
          }
        },
        handleSpinButtonLeave() {
          if (this.buttonLeaveAudio) {
          }
        },
        spinFor(index) {
          this.defaultWinner = index;
          this.$refs.spinner.spinWheel(index);
        },
        onSpinStart() {
          this.winnerResult = null;
          this.isSpinning = true;
        },
        onSpinEnd(winnerIndex) {
          this.isSpinning = false;
          this.winnerResult = this.slices[winnerIndex];
        }
      },
      mounted() {
      }
    };
  </script>
  
  <style>
  
    .cursor-img {
      width: 50px;
      aspect-ratio: 1 / 1;
      filter: drop-shadow(3px 3px 2px rgba(0, 0, 0, 0.19));
    }
  
    .spin-button {
      width: 100px;
      height: 100px;
      margin: 0 auto;
      aspect-ratio: 1 / 1;
      font-size: 20px;
      cursor: pointer;
      background: #eb4d4b;
      border-radius: 50%;
      transition: all 150ms;
      border: 10px solid white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      color: white !important;
      box-shadow: inset -3px -3px 2px 2px rgba(0, 0, 0, 0.19), 3px 3px 2px 2px rgba(0, 0, 0, 0.19);
      z-index: 11;
      position: relative;
      user-select: none;
  
      &:hover {
        box-shadow: inset -5px -5px 2px 2px rgba(0, 0, 0, 0.19), 3px 3px 2px 2px rgba(0, 0, 0, 0.19);
      }
  
      &:active {
        box-shadow: inset 3px 3px 2px 2px rgba(0, 0, 0, 0.19), 3px 3px 2px 2px rgba(0, 0, 0, 0.19);
      }
  
      &:disabled {
        background: #ccc;
        cursor: not-allowed;
        pointer-events: none;
      }
  
    }
  
  </style>