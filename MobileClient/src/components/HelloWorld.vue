<template>
    <div class="post">
        <div v-show="loading" class="loading">
            Loading... Please refresh once the ASP.NET backend has started. Hello friend.ss
        </div>

        <div v-if="post" class="content">
            <table>
                <thead>
                    <tr>
                        <th>Date</th>
                        <th>Temp. (C)</th>
                        <th>Temp. (F)</th>
                        <th>Summary</th>                        
                    </tr>
                </thead>
                <tbody>
                    <tr>Work dude</tr>
                    <tr v-for="forecast in post" :key="forecast.date">
                        <td>{{ forecast.date }}</td>
                        <td>{{ forecast.temperatureC }}</td>
                        <td>{{ forecast.temperatureF }}</td>
                        <td>{{ forecast.summary }}</td>                        
                    </tr>
                </tbody>
            </table>
            <button type="button" class="btn btn-primary">Primary</button>           
        </div>
    </div>
</template>

<script lang="js">
    import Vue from 'vue';    

    export default Vue.extend({
        data() {
            return {
                loading: false,
                post: null,
                loc: null
            };
        },
        created() {
            // fetch the data when the view is created and the data is           
            this.fetchData();
        },
        watch: {
            // call again the method if the route changes
            '$route': 'fetchData'
        },
        methods: {
            fetchData() {
                this.post = null;
                this.loading = true;

                try {
                    fetch('weatherforecast')
                        .then(r => r.json())
                        .then(json => {
                            this.post = json;
                            this.loading = false;
                            return;
                        });
                } catch (e) {
                    console.log(e);
                }               
            }
        },
    });
</script>