<template>
    <img :src="src" class="ico" alt="click" />
</template>

<script setup>
import { computed } from "vue";
const props = defineProps({
    name: {
        type: String,
        required: true,
    },
    size: {
        type: String,
        default: "16px",
    },
});
const src = computed(() => {
    return `/src/assets/${props.name}.svg`;
});

const styles = computed(() => {
    var width = props.width || props.size,
        height = props.height || props.size,
        style = {};

    if (width) {
        style.width = width;
    }

    if (height) {
        style.height = height;
    }

    return style;
});
</script>
<style scoped>
.ico {
    width: 24px;
    height: 24px;
}

@media (min-width: 660px) {
    .ico {
        width: 30px;
        height: 30px;
    }
}
</style>
