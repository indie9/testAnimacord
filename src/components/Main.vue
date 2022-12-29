<template>
    <div class="main-wrapper">
        <div class="content_container">
            <Button link="google.com" linkText="Напомнить PIN-код" />
            <Button
                link="https://spb.hh.ru/resume/d9baf77bff09a49b8a0039ed1f6b7254427846"
                linkText="Резюме Галанов Николай"
            />
        </div>
        <div class="content_container">
            <Button xClass="-primary" icon="fullArrow" @click="sayHi()" />
            <Button xClass="-danger" icon="exit" @click="sayHi()" />

            <Button xClass="-warning" icon="quest" @click="sayHi()" />
            <Button xClass="-primary" icon="arrow" @click="sayHi()" />

            <Button xClass="-danger" icon="google" @click="sayHi()" />
            <Button xClass="-info" icon="vk" @click="sayHi()" />

            <Button xClass="-action" icon="class" @click="sayHi()" />

            <Button xClass="-primary" icon="pen" @click="sayHi()" />
        </div>
        <div class="content_container">
            <Button
                xClass="-primary"
                textDelay="Повторное нажатие"
                @click="sayHi()"
                :hasTimer="true"
                :delay="10"
            >
                Кнопка с таймером
            </Button>
            <Button xClass="-secondary" @click="sayHi()">
                Отправить письмо
            </Button>
            <Button xClass="-warning" @click="sayHi()">
                Отправить письмо
            </Button>
            <Button xClass="-disabled" @click="sayHi()">
                Отправить письмо
            </Button>
            <Button xClass="-info" @click="sayHi()"> Отправить письмо </Button>
            <Button xClass="-danger" @click="sayHi()">
                Отправить письмо
            </Button>
            <Button xClass="-action" @click="sayHi()">
                Отправить письмо
            </Button>
        </div>
    </div>
</template>

<script setup>
import Button from "./Button.vue";

const sayHi = () => {
    console.log("hello world");
};
</script>

<style scoped>
.main-wrapper {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    background-color: #1e1e1e;
    padding: 50px;
    height: 80vh;
    width: 80vw;
}
.content_container {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    width: 100%;
    height: 100%;
    margin-bottom: 30px;
}
</style>
