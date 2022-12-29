<script setup>
import Icon from "./Icon.vue";
import { computed, onMounted, ref } from "vue";
const props = defineProps({
    xClass: String,
    icon: String,
    link: String,
    linkText: String,
    hasTimer: Boolean,
    textDelay: String,
    delay: Number,
});
const emit = defineEmits(["click"]);

let delayInSeconds = ref(0);

const startTimer = () => {
    delayInSeconds.value = props.delay || 60;
    let timerId = setInterval(() => {
        delayInSeconds.value -= 1;
        if (delayInSeconds.value <= 0) {
            clearInterval(timerId);
        }
    }, 1000);
};
const timerPending = computed(() => {
    return !!(delayInSeconds.value > 0);
});
const xClassRes = computed(() => {
    if (timerPending.value) {
        return "-disabled";
    } else {
        return props.xClass;
    }
});

const ButtonClick = () => {
    if (props.hasTimer && !timerPending.value) {
        emit("click");
        startTimer();
    } else if (!props.hasTimer) {
        emit("click");
    }
};
onMounted(() => {});
</script>

<template>
    <button
        class="btn"
        :class="[xClassRes, { 'btn-text-only': !icon, 'btn-icon-only': icon }]"
        @click="ButtonClick"
        type="button"
        v-if="!link"
    >
        <Icon :name="icon" v-if="icon" />
        <div class="btn-text" v-if="!icon">
            <div>
                <span v-if="hasTimer && timerPending && textDelay">
                    {{ textDelay }}</span
                >
                <slot v-else></slot>
            </div>

            <div v-if="hasTimer && timerPending" class="timer">
                {{ delayInSeconds }}
            </div>
        </div>
    </button>
    <div class="link-btn" v-else>
        <a :href="link" target="_blank">
            {{ linkText }}
        </a>
    </div>
</template>

<style>
.btn {
    cursor: pointer;
    color: white;
    height: 52px;
    min-width: 52px;
    border-radius: 19px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    font-size: 18px;
    line-height: 24px;
    text-transform: uppercase;
    font-family: "Phosphate", sans-serif;
}
.timer {
    width: 54px;
    height: 26px;
    background: #df3f3e;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 6px;
    border-radius: 10px;
}
.btn-icon-only {
    width: 52px;
}
.btn-text-only {
    border-top-right-radius: 18px;
    border-bottom-right-radius: 20px 19px;
    border-top-left-radius: 20px 19px;
    border-bottom-left-radius: 18px;
    padding: 0px 46px;
}
.btn-text {
    margin: 0px;
    white-space: nowrap;
    display: flex;
    flex-direction: row;
}
.link-btn a {
    font-family: "Nunito";
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 18px;
    text-align: center;
    color: #c4296c;
    border-bottom: 1px solid #c4296c;
    text-decoration: none;
}
.link-btn:hover a {
    color: #767679;
    border-bottom: 1px solid #767679;
    text-decoration: none;
}

.-primary {
    background-color: #702c7e;
}
.-secondary {
    background-color: #c4296c;
}
.-warning {
    background-color: #f4ba46;
}
.-disabled {
    background-color: #efefef;
    color: #767679;
}
.-info {
    background-color: #0083b6;
}
.-danger {
    background-color: #df3f3e;
}
.-action {
    background-color: #ed732e;
}

@media (min-width: 660px) {
    .btn-icon-only {
        height: 60px;
        min-width: 60px;
        border-radius: 22px;
    }
    .btn-text-only {
        height: 52px;
    }
}
</style>
