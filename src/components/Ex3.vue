<script>
import axios from 'axios';

export default {
    data() {
        return {
            moods: ["Happy", "Sad", "Angry"],
            mood: "Happy",
            entry: "",
            subject: "",
            message: "",
        }
    },
    computed: {
        baseUrl() {
            if (window.location.hostname == 'localhost')
                return 'http://localhost:3000'
            else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return `https://${codespace_host}`;
            }
        }
    },
    methods: {
        async addPost() {
            try {
                const response = await axios.get(`${this.baseUrl}/addPost`, {
                    params: {
                        'subject': this.subject,
                        'entry': this.entry,
                        'mood': this.mood
                    }
                })
                this.subject = ""
                this.entry = ""
                this.message = response.data.message;
                console.log(response.data.message);
            }
            catch (e) {
                console.error(e)
            }
        }
    },
    // add code here

}
</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        Mood:
        <!-- TODO: Build a dropdown list here for selecting the mood -->
        <select v-model="mood">
            <option v-for="mood of moods">{{ mood }}</option>
        </select>
        <br>

        <br>
        <button v-on:click="addPost()">Submit New Post</button>
        <p>{{ message }}</p>

        <hr> Click <a><router-link to="/ViewPosts/">here</router-link></a> to return to Main Page

    </div>
</template>
