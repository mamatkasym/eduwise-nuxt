<template>
    <div class="page-body">
        <div class="container">
            <h2 class="page-title">My Applications</h2>
            <application />
        </div>
    </div>
</template>

<script>
import Application from '@/components/client-admin/my-application'
export default {
    name: 'Client',
    components: { Application },
    layout: 'ClientAdmin',
}
</script>

<style></style>
