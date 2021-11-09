# 클릭하면 넘어가는 슬라이드

```js
const MybingoInMypage = (): JSX.Element => {
	const bingoState = useSelector((state: RootState) => state.bingo);

	const handleClickPreSlider = () => {
		const firstSlider = document.querySelector('.first');
		const currentSlide = document.querySelector('.move');

		if (currentSlide) {
			currentSlide.classList.remove('move');
			const nextSlider = currentSlide.previouselementsibling;
			if (nextSlider) {
				nextSlider.classList.add('move');
			} else {
				firstSlider.classList.add('move');
			}
		}
	};

	const handleClickNextSlider = () => {
		const firstSlider = document.querySelector('.first');
		const currentSlide = document.querySelector('.move');

		if (currentSlide) {
			currentSlide.classList.remove('move');
			const nextSlider = currentSlide.nextElementSibling;
			if (nextSlider) {
				nextSlider.classList.add('move');
			} else {
				firstSlider.classList.add('move');
			}
		}
	};

	return (
		<div className='mybingoinmypage'>
			<span className='preBtn'>
				<FontAwesomeIcon icon={faChevronLeft} className='chevron mybingoinmypage-left' onClick={handleClickPreSlider} />
			</span>
			<div className='mybingoinmypage-container'>
				<div className='mybingoinmypage-bingo-slider'>
					<div className='first mybingoinmypage-bingo move'>
						<h1>2021</h1>
						<Bingo MockBingo={bingoState} />
					</div>

					<div className='mybingoinmypage-bingo'>
						<h1>2020</h1>
						<Bingo MockBingo={bingoState} />
					</div>

					<div className='mybingoinmypage-bingo'>
						<h1>2019</h1>
						<Bingo MockBingo={bingoState} />
					</div>
				</div>
			</div>
			<span className='nextBtn'>
				<FontAwesomeIcon icon={faChevronRight} className='chevron mybingoinmypage-right' onClick={handleClickNextSlider} />
			</span>
		</div>
	);
};
```

```scss
.mybingoinmypage-bingo-slider{
  width:500px;
  height:500px;
  position:relative;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.mybingoinmypage-bingo{
    position: absolute;
    z-index: 0;
    opacity: 0;
    transition: all 0.5s ease-in-out;
    transform: scale(0.9);
}

.move{
  z-index: 1;
  opacity: 1;
  transform: none;
}
```