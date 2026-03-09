<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<title>Łukovia TV – Mecz na żywo</title>
<style>
body {
    margin: 0;
    font-family: 'Arial Black', Arial, sans-serif;
    background: linear-gradient(to bottom, #0b3d91, #1e90ff);
    color: #fff;
    text-align: center;
}
header {
    background: #ffcb05;
    color: #0b3d91;
    padding: 20px;
    font-size: 2.5em;
    font-weight: bold;
    letter-spacing: 2px;
    text-shadow: 2px 2px #1e90ff;
    border-bottom: 4px solid #0b3d91;
}
.video-container {
    position: relative;
    width: 85%;
    max-width: 1000px;
    margin: 40px auto;
    border: 5px solid #ffcb05;
    border-radius: 15px;
    box-shadow: 0 0 30px rgba(0,0,0,0.6);
    overflow: hidden;
}
iframe {
    width: 100%;
    height: 560px;
    border: none;
}
.info {
    margin-top: 20px;
    font-size: 1em;
    color: #fffbf0;
}
.scoreboard {
    position: absolute;
    top: 15px;
    right: 20px;
    background: rgba(255,203,5,0.8);
    color: #0b3d91;
    font-weight: bold;
    padding: 10px 15px;
    border-radius: 8px;
    font-size: 1.2em;
    text-shadow: 1px 1px #1e90ff;
}
</style>
</head>
<body>

<header>Łukovia TV – Mecz na żywo</header>

<div class="video-container">
    

    <!-- PLAYER -->
    <!-- Wystarczy wstawić link do Twitch lub YouTube -->
    <!-- Twitch: zmień NAZWA_KANALU na swój kanał i parent na domenę strony -->
    <iframe id="livePlayer" src="https://www.twitch.tv/lukoviatv_junior_mlodszy" allowfullscreen></iframe>

    <!-- YouTube alternatywnie (odkomentuj i zmień link) -->
    <!-- <iframe id="livePlayer" src="https://www.youtube.com/embed/ID_VIDEO?autoplay=1" allowfullscreen></iframe> -->
</div>

<div class="info">
    Transmisja tylko dla osób z linkiem. Udostępnij znajomym!<br>
                      Strona Łukovia TV 
</div>

<script>
// Możesz dynamicznie zmieniać link do streama w JS
// Przykład: zmiana Twitcha
// document.getElementById('livePlayer').src = "https://www.twitch.tv/lukoviatv_junior_mlodszy.netlify.app";

// Przykład: zmiana YouTube
// document.getElementById('livePlayer').src = "https://www.youtube.com/embed/ID_VIDEO?autoplay=1";
</script>

</body>
</html>


