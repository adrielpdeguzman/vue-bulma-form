<template>
  <div class="VuelmaForm__file file">
    <label class="file-label">
      <input
        class="file-input"
        v-bind="$props"
        :id="name"
        :value="null"
        @change="input"
        @blur.stop="onBlur"
        @focus.stop="onFocus"
      >
      <span class="file-cta">
        <span class="file-icon" v-if="hasIcon">
          <i class="fa" :class="`fa-${icon}`"></i>
        </span>
        <span class="file-label" v-text="placeholder"></span>
      </span>
      <span class="file-name" v-show="filename" v-text="filename"></span>
    </label>
  </div>
</template>

<script>
import Control from './Control';

export default {
  name: 'file-control',
  extends: Control,
  props: {
    /**
     * The placeholder label for the upload button.
     */
    placeholder: String,

    /**
     * The font-awesome icon to be used for upload button.
     */
    icon: {
      type: [String, Boolean],
      default: 'upload',
    },

    /**
     * Return array of files instead of FileList.
     */
    isArray: Boolean,
  },
  computed: {
    filename() {
      if (!this.value) {
        return null;
      }

      return this.value[0].name;
    },
    hasIcon() {
      return this.icon;
    },
  },
  methods: {
    /**
     * Handle the change input value event.
     */
    input(event) {
      const { name, files: value } = event.target;
      this.emit(name, this.isArray ? [...value] : value);
    },
  },
};
</script>
