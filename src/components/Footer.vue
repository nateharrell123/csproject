<template>
<footer class="footer">
    <div class="links">
    </div>
        <div class="black">
            <div class="one">
                <h3 class="description-header">
                    Waiting stinks, am I right?
                </h3>
                <p class="description-text">
                    If only there was a quick and easy way to find out how busy nearby establishments are, without having to call first. 
                    <br>
                    <br>
                    Lucky for you, <strong>HowBusy.com</strong> does just that.
                    <br>
                    <br>
                    It works by using the <code> Google Places API & Javascript Maps API</code> to scout out nearby businesses, then the 
                    <code> Popular-Times Python library  </code>
                    to scrape <i> live </i>, real-time attendance for any establishment. 
                </p>
            </div>
        <div class="two">
            <img :src="require('../assets/github.png')"/>
            <button class="pretty" @click="toGit()">  Star on GitHub </button>
        </div>
        </div>
</footer>
</template>

<script>
export default {
    name : "Footer",
    methods : {
        toGit(){
            window.open('https://github.com/nateharrell123/csproject')
        }
    }
}
</script>

<style>
.links{
    background: #32363b;
    width : 100%;
    padding:100px 0px 0px;
}
.pretty{
    font-size: .8rem;
    cursor: pointer;
    margin-top: 10px;
    border: 2px solid #b6bbc1;
    background: transparent;
    border-radius: 10px;
    padding: 6.66667px 10px;
    display: block;
    transition: background .2s;
    color: #b6bbc1;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    font-size: 12px;
    font-weight: 600;
}
button:hover{
     background: steelblue;
}
.description-header{
    font-size: 1.5rem;
    color: #9aa1aa;
    text-align: center;
    font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
    flex-basis: 66%;

    display: flex;
    max-width: 800px;
    padding: 30px 10px 20px;
    margin: auto;
}
.one{
    font-size: .8rem;
    color: #9aa1aa;
    flex-basis: 66%;
}
.two{
    display: flex;
    flex-direction: column;
    align-items: center;
    flex-basis: 33%;
}
.description-text{
    font-size: 1.2rem;
    max-width: 800px;
    padding: 30px;
    margin: auto;
    color: #9aa1aa;
    font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
}
.black{
    background: #222;
    padding:50px;
}
.footer{
    flex-shrink: 0;
}
body{
    margin:0;
}
</style>