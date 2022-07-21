<script setup>
const home_url = 'https://edcilo.com'
const logo_url = 'https://storage.edcilo.com/edcilo-logo-clear.svg'
</script>

<template>
    <main class="edc-pg">
        <div class="edc-pg--cover">
            <div class="edc-pg--pattern" />

            <header class="edc-pg--header">
                <a :href="home_url">
                    <el-image
                        class="edc-pg--header-logo-img" 
                        :src="logo_url" 
                        style="width: 90px; height: 28px"
                        fit="contain"
                        alt="edcilo.com"
                        lazy>
                        <template #placeholder>&nbsp;</template>
                    </el-image>
                </a>
            </header>

            <section class="edc-pg--body">
                <div>
                    <h1 class="edc-pg--title">Password Generator</h1>
                    <p class="edc-pg--label">Generate a secure password!</p>
                    <generator />
                </div>
            </section>

            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 280">
                <path 
                    fill="#ffffff" 
                    fill-opacity="1" 
                    d="M0,96L120,128C240,160,480,224,720,234.7C960,245,1200,203,1320,181.3L1440,160L1440,320L1320,320C1200,320,960,320,720,320C480,320,240,320,120,320L0,320Z" />
            </svg>
        </div>

        <footer class="edc-pg--footer">
            <a :href="home_url">
                edcilo.com |  <font-awesome-icon icon="code" />
            </a>
        </footer>
    </main>
</template>

<style setup>
.edc-pg {
    display: flex;
    flex-direction: column;
    align-content: center;
    justify-content: space-between;
    height: 100vh;
}

.edc-pg--cover {
    position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    background: #E44D26;
    background: -webkit-linear-gradient(to right, #F16529, #E44D26);
    background: linear-gradient(to right, #F16529, #E44D26)

    /* background: #cb2d3e;
    background: -webkit-linear-gradient(to right, #ef473a, #cb2d3d);
    background: linear-gradient(to right, #ef473a, #cb2d3e); */
}

.edc-pg--cover svg {
    z-index: 100;
}

.edc-pg--pattern {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: 1;
    background-image:
        radial-gradient(var(--el-color-error), rgba(255,255,255, 0.5) 1px, transparent 1px),
        radial-gradient(var(--el-color-error), rgba(255,255,255, 0.75) 1px, transparent 1px);
    background-size: 100px 100px, 100px 100px;
    background-position: 0 0, 50px 50px;
}

.edc-pg--header {
    width: 100%;
    padding: 0.5rem;
    text-align: center;
    z-index: 100;
    position: relative;
}

.edc-pg--header-logo-img {
    width: 90px;
    height: auto;
}

.edc-pg--body {
    align-self: center;
    width: 100%;
    padding: 1rem;
    max-width: 400px;
    width: 100%;
    z-index: 100;
}

.edc-pg--footer {
    width: 100%;
    background-color: var(--el-bg-color);
    padding: 1rem;
    text-align: center;
}

.edc-pg--title {
    text-align: center;
    font-size: 2rem;
    color: #ffe4d8;
    font-weight: bold;
    margin-bottom: 1.5rem;
}

.edc-pg--label {
    text-align: center;
    color: #ffba9c;
    margin-bottom: 2rem;
}

a {
    text-decoration: none;
    color: #E44D26;
}
</style>
