<template>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Josefin+Slab:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;1,100;1,200;1,300;1,400;1,500;1,600;1,700&family=Sen&display=swap" rel="stylesheet">
    
    <ControlPanel />
    
    <IntroductionText :userName="username" />
    
    <TaskList />
</template>

<script>
import ControlPanel from './components/ControlPanel.vue'
import TaskList from './components/TaskList.vue'
import IntroductionText from './components/IntroductionText.vue'

export default {
    name: 'App',
    components: {
        ControlPanel,
        TaskList,
        IntroductionText
    },
    data() {
        return {
            username: "Bruno",
        };
    }
};
</script>

<style>
* {
    background-color: #FCFCF3;
}

#app {
    font-family: 'Josefin Slab', serif;
    /* font-family: 'Sen', sans-serif; */
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
}

h1 {
  font-size: 2.5rem;
}
</style>
