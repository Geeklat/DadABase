<template>
    <div>
        <v-button></v-button>
        <h1>Dad-A-Base</h1>
        <div>The Dad Joke Database</div>
        <input type="file" accept=".csv" @change="handleFileUpload( $event )"/>
    </div>
</template>

<script>
    export default {
        name: 'DadABase',
        props: {
            msg: String,
            //csvData: String,
        },
        mounted() {
            this.loadCSV();
        },  
        methods: {
            loadCSV()
            {
                console.log('Load CSV');                
            },
            handleFileUpload( event ){
                this.file = event.target.files[0];
                console.log(this.file);
                this.$papa.parse(this.file, {
                    delimiter: ",",
                    header: true,
                    skipEmptyLines: true,
                    complete: function( results ){
                        console.log("Finished parsing");
                        this.content = results;
                        this.parsed = true;
                        console.log(this.content.data); // jokes
                        console.log(this.content.meta['fields']); // headers
                    }.bind(this)
                });                
            },            
        },
        data(){
            return {
                file: '',
                content: [],
                parsed: false
            }
        },
    }

    
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
  