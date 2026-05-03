<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
    <div class="cappa">
        <h1>Home page</h1>
        <Button variant="destructive">Click Me</Button>
        <Button class="viridis" variant="tertiarius">Click Me</Button>
    </div>
</template>

<style scoped>

.cappa {
    margin: 20px;
}

h1 {
    font-size: 24px;
    margin-bottom: 12px;
}

Button {
    margin-right: 12px;
}

.viridis {
    padding: 0 100px;
}

</style>