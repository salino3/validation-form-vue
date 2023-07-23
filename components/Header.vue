<template>
 <header >
    <div class="container">
        <p class="paragraph">Validation Forms</p>
        <nav>
            <ul>
                <li>
                    <nuxt-link to="/">Simple Form</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="user-form">User Form</nuxt-link>
                </li>
            </ul>
        </nav>
    </div>
 </header>
</template>

<script >
export default {
    name: "Header"
}
</script>

<style lang="css" scope>

header {

    position: sticky;
    top: 0px;
    display: absolute;
    border: solid;
    min-height: 70px;
}

.container {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    
    
    @media (min-width: 725px) {
        gap: 15%;   
    }
}

ul {
    display: flex;
    flex-direction: row;
    gap: 40px;
}

.paragraph {
    font-family: Georgia, 'Times New Roman', Times, serif;
    font-weight: 600;
    color: rgb(255, 162, 0)
}
</style>
