<template>
    <div v-if="video" class="col-md-6">
        <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" :src="videoUrl" />
        </div> 
        <div class="details">
            <h4>{{ video.snippet.title }}</h4>
            <p>{{ video.snippet.description }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'VideoDetail',
    props: ['video'],
    computed: {
        videoUrl() {
            const { videoId } = this.video.id
            return `https://www.youtube.com/embed/${videoId}`
        }
    }
}
</script>

<style scoped>
.details {
    margin-top: 5px;
    padding: 5px;
    border: 1px solid rgb(206, 206, 206);
    border-radius: 2px;
}
</style>
