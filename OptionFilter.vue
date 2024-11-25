<template>
  <div class="option-filter">
    <label class="filter-label">{{ label }}</label>
    <div class="select-wrapper">
      <select v-model="selected" class="filter-select" @change="onSelectChange">
        <option :value="defaultValue">{{ defaultText }}</option>
        <option v-for="(option, index) in options" :key="index" :value="option.value">
          {{ option.text }}
        </option>
      </select>
      <!-- canvas를 사용한 드롭다운 아이콘 -->
      <canvas ref="dropdownIcon" class="dropdown-icon"></canvas>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OptionFilter',
  props: {
    label: {
      type: String,
      required: true,
    },
    options: {
      type: Array,
      required: true,
    },
    defaultValue: {
      type: String,
      default: '',
    },
    defaultText: {
      type: String,
      default: '전체',
    },
    modelValue: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      selected: this.modelValue,
    };
  },
  watch: {
    modelValue(newValue) {
      this.selected = newValue;
    },
    selected(newValue) {
      this.$emit('update:modelValue', newValue);
    },
  },
  methods: {
    onSelectChange() {
      this.$emit('change', this.selected);
    },
    drawDropdownIcon() {
      const canvas = this.$refs.dropdownIcon;
      const ctx = canvas.getContext('2d');

      // canvas 크기 설정
      const width = 10;
      const height = 10;
      canvas.width = width;
      canvas.height = height;

      // 배경 투명
      ctx.clearRect(0, 0, width, height);

      // 삼각형 그리기
      ctx.fillStyle = '#000'; // 아이콘 색상
      ctx.beginPath();
      ctx.moveTo(0, 0); // 좌측 상단
      ctx.lineTo(width, 0); // 우측 상단
      ctx.lineTo(width / 2, height); // 아래 중앙
      ctx.closePath();
      ctx.fill();
    },
  },
  mounted() {
    this.drawDropdownIcon();
  },
};
</script>

<style scoped>
.option-filter {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #fff;
}

.filter-label {
  color: #3a3a3a;
  font-size: 18px;
  font-weight: 500;
  opacity: 0.5;
  white-space: nowrap;
}

.select-wrapper {
  position: relative;
  width: 100%;
}

.filter-select {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: auto;
  padding: 8px 36px 8px 12px; /* canvas 아이콘 공간 확보 */
  font-size: 18px;
  background-color: #fff;
  outline: none;
}

.dropdown-icon {
  position: absolute;
  right: 12px; /* 아이콘 위치 조정 */
  top: 50%;
  transform: translateY(-50%);
  pointer-events: none; /* 클릭 차단 */
}
</style>
