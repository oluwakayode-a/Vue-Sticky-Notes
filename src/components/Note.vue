<template>
    <transition leave-active-class="animated bounceOut">
        <div class="h-48 w-full sm:w-1/4 my-2">
            <div class="h-full rounded-lg px-4 py-4" :class="note.bg">
                <div class="flex text-white items-center mb-3 justify-between pr-2">
                    <h2 class="font-semibold">{{ note.title }}</h2>
                    <span class="fa fa-trash cursor-pointer" @click="deleteNote(index)"></span>
                </div>
                <hr>
                <p class="text-white mt-3 break-words">{{ note.note }}</p>
            </div>
        </div>
    </transition>
</template>

<style scoped>
    @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

    @media (min-width: 640px) {
        div {
            flex: 0 0 30%;
        }
    }
</style>

<script>
export default {
    name: 'Note',
    props: ['note', 'index', 'deleteNote'],
}
</script>