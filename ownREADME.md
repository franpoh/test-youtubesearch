// Dotenv is a zero-dependency module 
// loads environment variables from a .env file into process.env
// Stores configuration in the environment separate from code

// npm install googleapis
// npm install dotenv
// api key is in .env file in root folder

require("dotenv").config();
console.log(process.env.YOUTUBE_TOKEN);

const { google } = require("googleapis");

google.youtube("v3").search.list({
    key: process.env.YOUTUBE_TOKEN,
    part: "snippet",
    q: "rammstein",
}).then((response) => {
    const { data } = response;
    data.items.forEach((item) => {
        console.log(`Title: ${item.snippet.title}\nURL: https://www.youtube.com/watch?v=${item.id.videoId}`)
    })
}).catch((err) => console.log(err));

this.addHistory = this.addHistory.bind(this);

componentDidMount() {
        this.setState({
            ...this.state,
            history: JSON.parse(localStorage.getItem("history")),
        })
    }

    addHistory(event) {
        const historyitem = {
            title: this.state.searchTitle,
            url: this.state.searchURL,
        }

        console.log("History Item: ", historyitem);

        this.state.history.push(historyitem);
        localStorage.setItem("history", JSON.stringify(this.state.history));
    }