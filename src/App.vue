<template>
    <div class="main">

        <form @submit.prevent>
            <h2>Создать новый пост</h2>
            <div class="form-group">
                <input v-bind:value="title"
                       @input="inputValueTitle"
                       class="input" 
                       id="inputTitle"
                       :class="{'error': emptyStr}"
                       type="text" 
                       placeholder="Название"
                >
                <div class="help-block" 
                     v-if="visibleTitle" 
                     id="error-input"
                >
                    <span>Поле не заполнено.</span>
                </div>
            </div>
            <div class="form-group">
                <input v-bind:value="body" 
                       @input="inputValueBody"
                       class="input"
                       id="inputBody" 
                       :class="{'error': emptyStr}"
                       type="text" 
                       placeholder="Описание"
                >
                <div class="help-block" 
                     v-if="visibleBody" 
                     id="error-desription"
                >
                    <span>Поле не заполнено.</span>
                </div>

            </div>
            <button class="btn" @click="createPost">Создать</button>
        </form>
        <div class="post" v-for="post in posts">

            <div class="post-title"><strong>Название</strong> {{ post.title }}</div>
            <div class="post-body"><strong>Описание</strong> {{ post.body }}</div>
           
        </div>

    </div>
</template>

<script>
export default {

    data() {
        return {
            posts: [
            ],
            title: '',
            body: '',
            emptyStr: false,
            visibleTitle: false,
            visibleBody: false
        }
    },
    methods: {
        inputValueTitle(event) {

            let inputTitle = document.querySelector('#inputTitle');
            let emptyInputTitle = document.querySelector('#error-input');
            this.title = event.target.value;
            if(event.target.value !== '') {
                inputTitle.classList.remove("error");
                emptyInputTitle.classList.add("unvisible");
            }

        },

        inputValueBody(event) {

            let inputBody = document.querySelector('#inputBody');
            let emptyInputBody = document.querySelector('#error-desription');
            this.body = event.target.value;
            if(event.target.value !== '') {
                inputBody.classList.remove("error");
                emptyInputBody.classList.add("unvisible");
            }

        },

        createPost() {

            let newTitlePost = this.title;
            let newBodyPost = this.body;
            let emptyInputTitle = document.querySelector('#error-input');
            let emptyInputBody = document.querySelector('#error-desription');

            if(newTitlePost.trim() == '') {
                this.visibleTitle = true;
            } 
            if(newBodyPost.trim() == '') {
                this.visibleBody = true;
            }
            if (newTitlePost.trim() !== '' && newBodyPost.trim() !== '') {
                const newPost = {
                    id: Date.now(),
                    title: this.title,
                    body: this.body,
                }
                this.posts.push(newPost);
                this.emptyStr = false;
                this.title = '';
                this.body = '';
            } else {
                this.emptyStr = true;
                if(newTitlePost.trim() == '' && newBodyPost.trim() == '') {
                    emptyInputTitle.classList.remove("unvisible");
                    emptyInputBody.classList.remove("unvisible");
                }
                if(newTitlePost.trim() == '') {
                    emptyInputTitle.classList.remove("unvisible");
                }
                if(newBodyPost.trim() == '') {
                    emptyInputBody.classList.remove("unvisible");
                }
            }
            
        }

    }

}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,300;0,400;0,500;0,700;0,900;1,300;1,400;1,500;1,700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box; 
}

html, body {
    height: 100%;
}

body {
    display: flex;
    flex-direction: column;
    font-family: 'Roboto', sans-serif;
    background-color: #242327;
    margin: 0 auto;
}

.wrapper {
    flex: 1 0 auto;
}

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 14px 22px;
    margin-bottom: 40px;
    background: #33343C;
}

.header a {
    color: #fff;
    text-decoration: none;
}

#app {
    max-width: 80%;
    margin: 0 auto;
    background: #fff;
    border: 5px solid #444444;
}

.main {
    padding: 20px;
    background-color: #f7f7f7;
}

h2 {
    margin: 1rem 0;
}

form {
    display: flex;
    flex-direction: column;
    margin-bottom: 35px;
}

.form-group {
    display: flex;
    flex-direction: column;
}

.form-group, .input {
    position: relative;
}

.form-group .help-block {
    position: absolute;
    padding: 0px 5px;
    font-size: 0.93em;
    line-height: 1.75em;
    margin: -2px 0 0 12px;
    color: #fff;
    background: #ff4e4e;
    bottom: 0;
}

.form-group .help-block:after {
    content: " ";
    position: absolute;
    left: 5px;
    bottom: 100%;
    width: 0;
    height: 0;
    border-bottom: 10px solid #ff4e4e;
    border-right: 10px solid transparent;
}

.with-errors {
    display: block;
}

.input {
    width: 100%;
    border: 2px solid #B8C2DC;
    margin-bottom: 24px;
    padding: 8px 10px;
}

.btn {
    margin-top: 20px;
    font-family: 'Roboto', sans-serif;
    font-weight: 500;
    cursor: pointer;
    align-self: flex-end;
    padding: 5px 10px;
    background: transparent;
    border: 2px solid #B8C2DC;
    color: #000;

}

.btn::placeholder {
    font-family: 'Roboto', sans-serif;
}

.post {
    border: 2px solid #B8C2DC;
    padding: 8px 10px;
    margin: 10px 0;
}

.post-title {
    padding-bottom: 7px;
    border-bottom: 1px dotted #B8C2DC;
    word-wrap: break-word;
}

.post-body {
    padding-top: 7px;
    padding-bottom: 8px;
    word-wrap: break-word;
}

.error {
    border: 2px solid #ff0000;
}

.footer {
    margin-top: 40px;
    flex-shrink: 0;
    display: flex;
    justify-content: center;
    flex-direction: column;
    background: #323741;
    padding: 10px 0;
}

.footer div {
    margin: 3px 0;
}

.footer a {
    text-decoration: none;
    color: #9B9DAB;
}

.footer p {
    text-align: center;
}

#line-block {
    display: none;
} 

#line-block p {
    color: #9B9DAB;
}

.line {
    font-weight: bold;
    font-size: 14px;
    padding-top:2px;
}

.unvisible {
    display: none;
}


@media (min-width: 420px) {

    .header {
        padding: 17px 55px;
    }

    .footer {
        flex-direction: row;
        padding: 0;
    }

    .footer div {
        margin: 20px 15px;
    }

    #line-block {
        display: flex;
        align-items: center;
        justify-content: center;
    }

}


@media (min-width:720px) {

    .footer div {
        margin: 20px 45px;
    }

}

</style>
