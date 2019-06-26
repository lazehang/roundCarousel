<template>
    <div :class="`${className}`">
        <img :src="img" class="item__image js-imgsrc" />
    </div>
</template>
<script>
export default {
    props: {
        img: String,
        className: {
            type: String,
            default: ""
        }
    }
}
</script>
