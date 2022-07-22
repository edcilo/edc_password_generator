<script setup>
import { ElMessage } from 'element-plus'
import PasswordGenerator from "../services/password_generator"

const length = ref(12)
const uppercase = ref(true)
const numbers = ref(true)
const symbols = ref(true)
const password = ref(null)

const min = 6
const max = 256

const generate_password = () => {
    const pg = new PasswordGenerator(length.value)

    pg.with_uppercase = uppercase.value
    pg.with_numbers = numbers.value
    pg.with_symbols = symbols.value

    password.value = pg.generate()
}

const copy_to_clipboard = () => {
    if (navigator && navigator.clipboard && navigator.clipboard.writeText) {
        ElMessage({
            message: 'Copied!',
            type: 'success',
            showClose: true,
        })
        return navigator.clipboard.writeText(password.value)
    }
    return Promise.reject('The Clipboard API is not available.')
}

onMounted(() => {
  generate_password()
})
</script>

<template>
<el-card>
    <template #header>
        <div class="edc-pg--password-ctrls">
            <div class="edc-pg--password">
                <el-input v-model="password" class="edc-pg--password edc-pg--custom" readonly />
            </div>
            <el-button @click="copy_to_clipboard" class="edc-pg--custom">
                <font-awesome-icon icon="copy" />
            </el-button>
        </div>
    </template>

    <div class="edc-pg--section">
        <div class="edc-pg--length-label">
            Password length ({{length}} characters)
        </div>
        <div class="edc-pg--slider">
            <ClientOnly placeholder-tag="span">
                <el-slider 
                    v-model="length" 
                    :min="min"
                    :max="max" 
                    class="edc-pg--custom"
                    :show-input="false" />
            </ClientOnly>
        </div>
    </div>

    <el-row class="edc-pg--section">
        <el-col :span="8">
            <el-checkbox 
                v-model="uppercase" 
                class="edc-pg--custom"
                label="Uppercase" />
        </el-col>
        <el-col :span="8">
            <el-checkbox 
                v-model="numbers" 
                class="edc-pg--custom"
                label="Numbers" />
        </el-col>
        <el-col :span="8">
            <el-checkbox 
                v-model="symbols" 
                class="edc-pg--custom"
                label="Symbols" />
        </el-col>
    </el-row>

    <el-button 
        class="edc-pg--new-pass-btn edc-pg--btn-custom" 
        type="primary" 
        @click="generate_password">
        New password
    </el-button>
</el-card>
</template>

<style scoped>
.edc-pg--password-ctrls {
    display: flex;
    justify-content: space-between;
}

.edc-pg--password {
    width: 100%;
    margin-right: 1rem;
}

.edc-pg--section {
    margin-bottom: 1rem;
}

.edc-pg--slider {
    height: 32px;
}

.edc-pg--slider span {
    display: block;
    position: relative;
    top: 13px;
    width: 100%;
    height: 6px;
    background-color: var(--el-border-color-light);
    border-radius: 3px;
}

.edc-pg--new-pass-btn {
    width: 100%;
}

.edc-pg--length-label {
    font-size: 0.875rem;
    margin-bottom: 0.4rem;
    font-weight: 500;
    color: #F16529;
}

.edc-pg--custom {
    --el-color-warning: #F16529;
    --el-color-warning-light: #ff753a;
    --el-color-warning-lighter: #ffe4d8;
    
    --el-color-primary: var(--el-color-warning);
    --el-button-hover-border-color: var(--el-color-warning-light);
    --el-button-hover-bg-color: var(--el-color-warning-lighter);

    color: var(--el-color-warning);
}

.edc-pg--btn-custom {
    --el-color-warning: #F16529;
    --el-color-warning-light: #ff9364;
    --el-color-warning-dark: #E44D26;

    --el-color-primary: var(--el-color-warning);
    --el-button-hover-border-color: var(--el-color-warning-light);
    --el-button-hover-bg-color: var(--el-color-warning-light);
    --el-button-active-border-color: var(--el-color-warning-dark);
    --el-button-active-bg-color: var(--el-color-warning-dark);
}
</style>
