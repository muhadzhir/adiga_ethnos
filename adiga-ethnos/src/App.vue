<template>
  <div class="content">
    <div class="input-wrapper">
      <input
        @input="checkTribe"
        @focus="focus"
        @focusout="focusOut"
        v-model="inputValue"
        class="input"
        type="text"
      >
        <span
          :class="{
          'input-label-filled': inputUsed,
          'input-label-warn': existTribe,
          'input-label-accept': isRightTribe
          }"
          class="input-label"
        >
          Национальность
        </span>
      <div class="input-tooltip" :class="{ 'input-tooltip-show': showTooltip }">
        <span class="input-tooltip-text" v-html="tooltipText"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isRightTribe: false,
      existTribe: false,
      inputValue: '',
      isFocused: false,
      showTooltip: false,
      tooltipText: '',
      rightTribe: {
        male: 'Черкес',
        female: 'Черкешенка'
      },
      tribes: [
        {
          male: 'Адыгеец',
          female: 'Адыгейка'
        },
        {
          male: 'Кабардинец',
          female: 'Кабардинка'
        }
      ]
    }
  },
  computed: {
    inputUsed () {
      return this.inputValue || this.isFocused
    }
  },
  methods: {
    focus () {
      this.isFocused = true
    },
    focusOut () {
      this.isFocused = false
    },
    checkTribe () {
      this.existTribe = false
      this.showTooltip = this.tribes.some((tribe, i) => Object.keys(tribe).some(t => {
        if (this.inputValue.trim().toLowerCase() === this.tribes[i][t].toLowerCase()) {
          this.existTribe = true
          this.tooltipText = `Возможно вы имели в виду ${this.rightTribe[t]}`
          return true
        }
      }))
      this.isRightTribe = Object.keys(this.rightTribe).some(m => this.inputValue.trim().toLowerCase() === this.rightTribe[m].toLowerCase())
    }
  }
}
</script>

  <style>
    .content {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      box-sizing: border-box;
      position: relative;
    }
    .input {
      height: 80px;
      border-radius: 10px;
      width: 400px;
      padding-left: 20px;
      padding-top: 20px;
      outline: none;
      margin-left: -100px;
      margin-top: -25px;
      font-size: 28px;
    }

    .input-wrapper {
      position: relative;
    }
    .input-tooltip {
      position: absolute;
      width: 426px;
      height: 100px;
      border-radius: 10px;
      color: white;
      left: -100px;
      top: 85px;
      background-color: green;
      font-family: Arial, Helvetica, sans-serif;
      max-height: 100px;
      box-sizing: border-box;
      font-size: 22px;
      transition: all .4s linear;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      max-height: 0;
    }
    .input-tooltip-show {
      max-height: 100px;
    }
    .input-tooltip-text {
      display: block;
    }
    .input-label {
      transition: all .2s linear;
      position: absolute;
      left: -80px;
      font-size: 28px;
      top: 20px;
      font-family: Arial, Helvetica, sans-serif;
      z-index: 1;
      pointer-events: none;
      color: #999;
    }
    .input-label-filled {
      top: -5px;
      font-size: 20px;
    }
    .input-label-warn {
      color: tomato;
    }
    .input-label-accept {
      color: #15a32b;
    }
    @media (max-width: 767px) {
      .content {
        padding-top: 50px;
        align-items: flex-start;
      }
      .input-wrapper {
        width: 100%;
        display: flex;
      }
      .input {
        width: 100%;
        margin-left: 10px;
        margin-right: 10px;
        height: 50px;
        font-size: 18px;
      }
      .input-tooltip  {
        left: 10px;
        top: 55px;
        width: calc(100% - 20px);
        height: 70px;
        font-size: 18px;
        text-align: center;
      }
      .input-label {
        transition: all .2s linear;
        position: absolute;
        left: 30px;
        font-size: 24px;
        top: 5px;
      }
      .input-label-filled {
        top: -15px;
        font-size: 16px;
      }
    }
  </style>
