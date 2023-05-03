<script>
	import { onDestroy, tick } from 'svelte';

let name = "จอม";
	let age = 0;

	function updateAge() {
		// calculate age based on birthdate and time
		const birthDateTime = new Date('2009-05-03T12:30:00'); // set birth date and time
		const now = new Date(); // get current date and time
		const ageInMs = now.getTime() - birthDateTime.getTime(); // calculate age in milliseconds
		let newAge = ageInMs / (1000 * 60 * 60 * 24 * 365); // convert milliseconds to years, rounding to nearest year
		if (
			now.getMonth() < birthDateTime.getMonth() ||
			(now.getMonth() === birthDateTime.getMonth() && now.getDate() < birthDateTime.getDate())
		) {
			newAge -= 1; // adjust age if birthdate hasn't passed this year
		}
		if (
			now.getMonth() === birthDateTime.getMonth() &&
			now.getDate() === birthDateTime.getDate() &&
			now.getHours() === birthDateTime.getHours() &&
			now.getMinutes() === birthDateTime.getMinutes() &&
			now.getSeconds() === birthDateTime.getSeconds()
		) {
			newAge += 1; // adjust age if it's exactly the birth time
		}
		age = newAge;
	}

	// update age every second
	const interval = setInterval(updateAge, 50);

	// stop the interval when the component is destroyed
	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<div class="center">
	<div class="container">
		<div class="title">
			<div class="image" />

			<div>
				<h2>แฮปปี้เบิร์ดเดย์ {name} 🎂</h2>
				<h1><span class="age">{age.toFixed(9)}</span> ขวบแล้ว</h1>
			</div>
		</div>

		<div class="content">
			<p>
				เด็กเกย์ห้องหนึ่ง ในที่สุดก็อายุ {Math.trunc(age)} ขวบแล้ว (ไม่น่าโตมาเลย) เด็กหนุ่มผู้แปรผันของกาลเวลา
				ทำลายทุกขีดจำกัดของการเอากับเพื่อน และกฏของห้องหนึ่ง เป็นน่าที่ยินดีอย่างยิ่งในคำคืนของวันนี้
			</p>
		</div>
	</div>
</div>

<style lang="scss">
	$primary: #f1faee;
	$secondary: #457b9d;
	$call-to-action: #e63946;

	.container {
		max-width: 40rem;
		padding: 1rem;
	}

	.center {
		width: 100%;
		min-height: 100vh;

		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		

		background-image: url('./jom.png');
		background-repeat: none;
		background-size: cover;
		background-position: center;


		.title {
			font-size: 400;
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			max-height: 30rem;
			max-width: 50rem;
			gap: 2em;
			text-align: center;

			div {
				flex: 2 2 0%;
			}

			.image {
				flex: 1 1 auto;
				min-width: 100px;
				min-height: 150px;
				background-image: url('/cake.png');
				background-size: contain;
				background-repeat: no-repeat;
				background-position: center;
			}

			.age {
				color: #fff;
				text-shadow: 1px 0 0 #000, 0 -1px 0 #000, 0 1px 0 #000, -1px 0 0 #000;
			}
		}

		.content {
			padding: 2rem;
			margin-top: 1.5rem;
			border: 2px solid black;
			border-radius: 0.3rem;
			background-color: $secondary;
			color: white;
		}
	}
</style>
