<template>
    <div class="container">
        <template v-for="field of fields">
            <label :for="field.field">{{ field.field }}: &nbsp;</label>
            <template v-if="field.type !== 'children'">
                <input :id="field.field" :name="field.field" type="text" v-model="field.value"/><br>
            </template>
            <template v-else>
                <TheFormBuilder :fields="field.children" />
            </template>
        </template>
    </div>
</template>
<script setup lang="ts">
import type { Product } from '@/classes/Form';

const props = withDefaults(
    defineProps<{
        fields: Product[];
    }>(),
    {
        fields: () => []
    }
)
</script>
<style scoped >
.container {
    margin: 10px 0;
    border: 1px solid red;
    padding: 10px 20px;
}
</style>