# URL의 길이와 GET의 한계

최근에 서버에서 데이터 목록을 불러오는 GET api에서 오류가 발생해 POST로 바꾼 적이 있다.

api에서 id의 배열을 사용해 query를 만드는 부분이 있는데,

배열 데이터가 많아지니 GET 메서드 특성상 URL이 브라우저가 허용하는 길이 이상으로 길어져 생긴 문제였다.

스탠다드가 권하는 URL 길이 한계가 있고 브라우저별로 정해지는 URL 길이 한계가 있다는 것을 처음 알았다.

[https://stackoverflow.com/questions/2659952/maximum-length-of-http-get-request](https://stackoverflow.com/questions/2659952/maximum-length-of-http-get-request)

[https://stackoverflow.com/questions/417142/what-is-the-maximum-length-of-a-url-in-different-browsers](https://stackoverflow.com/questions/417142/what-is-the-maximum-length-of-a-url-in-different-browsers)

[돌아가기](./README.md)
