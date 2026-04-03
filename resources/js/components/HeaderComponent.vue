<template>
    <header id="header">
        <h1><a href="#" @click.prevent="changePage('HomePage')">CookHelper</a></h1>
        <nav class="main">
            <input type="search" placeholder="Поиск рецептов..." />
            <a href="#menu">Войти</a>
        </nav>
    </header>
</template>

<script>
export default {
    name: 'HeaderComponent',
    props: ['isUser', 'user', 'changePage', 'PUBLIC'],
};
</script>
