<template>
    <div class="sourceselection">
        <div class="jumbotron">
            <h4>Select Your Favourite News Source</h4>
            <select class="form-control" v-on:change="sourceChanged">
                <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
            </select>

            <div v-if="source">
                <h6>{{source.description}}</h6>
                <div class="text-center">
                    <a v-bind:href="source.url" class="btn btn-sm btn-info btn-raised" target="_blank">Go to {{source.name}} Website</a>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export  default {
        name: 'sourceselection',
        data () {
            return {
                sources: [],
                source: ''
            }
        },
        methods: {
            sourceChanged: function (e) {
                for(var i=0; i<this.sources.length; i++){
                    if(this.sources[i].id == e.target.value){
                        this.source = this.sources[i];
                    }
                }
                this.$emit('sourceChanged', e.target.value);
            }
        },
        created: function () {
            this.$http.get('https://newsapi.org/v1/sources?langauge=en')
            .then(response => {
                this.sources = response.data.sources;
            });
        }
    }
</script>
<style scoped>

</style>