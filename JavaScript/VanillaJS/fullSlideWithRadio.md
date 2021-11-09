# 풀스크린 슬라이드

```jsx
<div classname='slider' id='slider'>

//name값이 같도록 설정해야함. 수동으로 클릭하면 넘어가는 코드
	<input type='radio' name='slider-radios' classname='slide-radio' checked id='slider-radio-1'/>
	<input type='radio' name='slider-radios' classname='slide-radio' id='slider-radio-2'/>
	<input type='radio' name='slider-radios' classname='slide-radio' id='slider-radio-3'/>
	<input type='radio' name='slider-radios' classname='slide-radio' id='slider-radio-4'/>

	<div classname='pagination'>
		<label for='slider-radio-1'></label>
		<label for='slider-radio-2'></label>
		<label for='slider-radio-3'></label>
		<label for='slider-radio-4'></label>
	</div>

	<div classname='slide' id='slide-1'>
		<div classname='slide-content'>
			<h1>Hello1</h1>
			<h2>World1</h2>
			<a href=''></a>
		</div>
		<img src='' alt=''/>
	</div>

	<div classname='slide' id='slide-2'>
			<div classname='slide-content'>
				<h1>Hello2</h1>
				<h2>World2</h2>
				<a href=''></a>
			</div>
			<img src='' alt=''/>
		</div>
	
	<div classname='slide' id='slide-3'>
			<div classname='slide-content'>
				<h1>Hello3</h1>
				<h2>World3</h2>
				<a href=''></a>
			</div>
			<img src='' alt=''/>
		</div>
	
	<div classname='slide' id='slide-4'>
			<div classname='slide-content'>
				<h1>Hello4</h1>
				<h2>World4</h2>
				<a href=''></a>
			</div>
			<img src='' alt=''/>
		</div>
</div>
```

```scss
//이미지 사이즈 2048*2048

*{
	box-sizing:border-box;
}

.slider{
	position:absolute;
	left:0;
	right:0;
	top:0;
	bottom:0;
	overflow:hidden;
	z-index:0;
}

.slide{
	position:absolute;
	width:100%;
	height:100%;
	//쓰윽.. 뒤에는 속도 조절 (https://easings.net/ko)
	transition:transform 1s cubic-bezier(0.85, 0, 0.15, 1);
	img{
		height:100vh;
	}
}

#slide-1{
	background:;
	left:0;
}
#slide-2{
	background:;
	left:100%;
}
#slide-3{
	background:;
	left:200%;
}
#slide-4{
	background:;
	left:300%;
}

#slider-radio-1:checked ~ .slide {transform:translateX(0);}
#slider-radio-2:checked ~ .slide {transform:translateX(-100%);}
#slider-radio-3:checked ~ .slide {transform:translateX(-200%);}
#slider-radio-4:checked ~ .slide {transform:translateX(-300%);}

//클래스명으로 설정해주기
input{
	display:none;
}

.pasination{
		position:absolute;
		left:50%;
		transform:translateX(-50%);
		botton:6rem;
		z-index:1;
}
```