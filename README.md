# web_karaoke

아래의 코드에서 API키를 추가하여 열면 됩니다.
라이브러리의 업데이트가 없다면 별다른 수정없이 웹페이지 하나로 사용 가능합니다.
```js
/*******************************
 * 사이드 바 내 검색
 * Created 2020.07.09.
 * Author: Jeong MinGyu
 *******************************/
var Search = () => {
    const API_KEY = "AIzaSyDTGfPj4WN39YV1i9Wb9y5LDgMkGoH6boA";
    $.ajax({
        url: 'https://www.googleapis.com/youtube/v3/search?channelId=UCDqaUIUSJP5EVMEI178Zfag&key='+API_KEY+'&part=snippet&maxResults=5&q=' +
            encodeURI($('#songName').val() + " 노래방"),
        type: 'GET',
        dataType: 'json',
        success: function (data) {
            var result = data;
            console.log(result.items);
            var str = "";
            for (var i = 0; i < 5; i++) {
                str += '<li id="songSelect' + i + '"><img src="' + result.items[i].snippet
                    .thumbnails.default.url + '" alt="' + result.items[i].id.videoId +
                    '"><br>' + result.items[i].snippet.title + "</li>";
            }
            $("#select").html(str);
            $('#songName').val('');
        },
        error: function (msg) {
            alert(msg);
            console.log('Error:' + msg);
        }
    });
};
```