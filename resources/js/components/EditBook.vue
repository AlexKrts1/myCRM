<template>
    <div>
        <h3 class="text-center">Edit Book</h3>
        <div class="row">
            <div class="col-md-6">
                <form @submit.prevent="updateBook">
                    <div class="form-group">
                        <label>Name</label>
                        <input type="text" class="form-control" v-model="book.name">
                    </div>
                    <div class="form-group">
                        <label>Author</label>
                        <input type="text" class="form-control" v-model="book.author">
                    </div>
                    <button type="submit" class="btn btn-primary">Update Book</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                book: {}
            }
        },
        created() {
            this.axios
                .get(`http://localhost:8000/api/book/edit/${this.$route.params.id}`)
                .then((response) => {
                    this.book = response.data;
                     console.log(response.data);
                     console.log('edit param id: '+this.$route.params.id);
                });
        },
        methods: {
            updateBook() {
                this.axios
                    .post(`http://localhost:8000/api/book/update/${this.book.id}`, {name:this.book.name, author: this.book.author})
                    .then((response) => {
                        this.$router.push({name: 'home'});
                        console.log('update param id: '+this.$route.params.id);
                        console.log('update post this/book param: '+this.book.id);
                    });
            }
        }
    }
</script>