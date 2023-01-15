<template>
    <div flex justify-center>

        <div border="~ rounded gray-200 dark:gray-700" outline="none active:none" m="b-4" justify-center w-screen-sm
            hover-bg-blend-overlay bg-opacity-80
            v-bind:class="match ? 'bg-green-900 hover-bg-green-900' : 'hover-bg-gray-800'">
            <div v-if="match" text-s text-right m-r-2 m-t-2 text-green:80>
                <a i-carbon-checkmark-outline class="inline-block" />
            </div>
            <div v-else text-s text-right m-r-2 v-bind:class="match ? 'text-green:80' : 'text-gray:50'">
                {{ getScore }}
            </div>
            <div class="result__title">
                <h5 text-xs>ID: {{ result.item.id }}</h5>
                <h2 class="text-2xl font-bold">{{ result.item.name }}</h2>
            </div>
            <div class="result__description">
                <p class="text-sm text-gray:90" font-italic>{{ result.item.description }}</p>
            </div>
            <div class="result__tags">
                <div v-for="tag in result.item.tags" class="tag" text-xs text-gray:80>
                    {{ tag }}
                </div>
            </div>
            <div text="xl gray4" m-5 flex justify-center gap-3>
                <a i-carbon-json-reference :href="result.item.mappingURL" target="_blank" />
                <a i-carbon-api-1 :href="result.item.url" target="_blank" />
            </div>
        </div>
    </div>

</template>

<script setup lang="ts">
export interface Props {
    result: {
        item: {
            name: string;
            id: string;
            description: string;
            url: string;
            mappingURL: string;
            tags: [];
        },
        score: number;
        refIndex: number;
    }
}
const props = defineProps<Props>()
const match = ref(false)
const getScore = computed(() => {
    // if score is smaller 0.005 show "Match"
    if (props.result.score < 0.005) {
        match.value = true
        return 'Match'
    }
    // if score is smaller 0.1 show "Good Match"
    if (props.result.score < 0.1) {
        return "Good Match"
    }
    else {
        return "Similar"
    }
})


</script>

<style scoped>
.result__title {
    padding: 1rem;
}

.result__description {
    padding: 1rem;
}

.result__tags {
    padding: 1rem;
}
.tag{
    display: inline-block;
    padding: 0.5rem;
    margin: 0.5rem;
    border-radius: 0.5rem;
    background-color: #424952;
}
</style>