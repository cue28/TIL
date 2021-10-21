# 연속된 이미지를 불러와서 움직이는 듯이 표현한 것

ex)[https://www.apple.com/kr/macbook-pro-14-and-16/](https://www.apple.com/kr/macbook-pro-14-and-16/)

1. 자동으로 이미지 시퀀스가 플레이 된다.

```jsx
let canvas = document.getElementById('screen');
let ctx = canvas.getContext('2d');
//인스턴스 생성 html의 이미지 태그와 비슷하다고 생각하면 됨.
let img = new Image();

let imgNum = 0;

//1씩 증가시키는 함수
function playSequence() {
	//1초에 한번씩 실행되는 타이머
	let timer = setInterval(function() {
		console.log("Time Interval" + imgNum);

		//반복되는 이미지를 원한다면
		if (imgNum > 86) {
			imgNum = 0;
		};

		player(imgNum);
		imgNum++;
	}, 33);
};

//이미지를 불러오는 함수
function player(num) {
	img.src = "image/경로" + num + ".png";
};

playSequence();

//이렇게 하면 이미지가 겹쳐짐
img.addEventListener('load', function(e){
	ctx.drawImage(img, 0, 0);
});

//이렇게하면 한 컷씩
img.addEventListener('load', function(e){
	ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);
	ctx.drawImage(img, 0, 0);
});
```

1. 스크롤을 한다. (scroll.js)
2. 이미지 시퀀스가 플레이된다.

```jsx
let canvas = document.getElementById('screen');
let ctx = canvas.getContext('2d');
//인스턴스 생성 html의 이미지 태그와 비슷하다고 생각하면 됨.
let img = new Image();

let scrollYPos = 0;

//최초에 이미지를 불러옴
img.src = "image/경로/image01.png";

//이 부분이 다름
window.addEventListener('scroll', function(e){
	//너무 큰 값이 나와서 18으로 나누어 반올림해서 정수로 반환
	scrollYPos = Math.round(window.scrollY/18);
	console.log(scrollYPos);	//안 뜬다면 길이가 짧아서

	//0~86까지 지나면 멈춤 상태로 고정!
	if (scrollYPos > 86) {
		scrollYPos = 86;
	};

	play(scrollYPos);
});

//이미지를 불러오는 함수
function player(num) {
	img.src = "image/경로" + num + ".png";
};

//이렇게 하면 이미지가 겹쳐짐
img.addEventListener('load', function(e){
	ctx.drawImage(img, 0, 0);
});

//이렇게하면 한 컷씩
img.addEventListener('load', function(e){
	ctx.clearRect(0, 0, ctx.canvas.width, ctx.canvas.height);
	ctx.drawImage(img, 0, 0);
});
```

```css
//이미지 자체의 div를 고정시켜야함.
position : fixed;
top : 100px;
```

ref. 
[https://youtu.be/nPrvM4ArmIU](https://youtu.be/nPrvM4ArmIU)