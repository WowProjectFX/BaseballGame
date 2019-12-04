```javascript
        
	//[0] 스트라이크 , [1] 볼, [3] 아웃, [3] 안타 횟수 저장 
	let ballCount = [0, 0, 0, 0]; 

	// 랜덤한 투구 - 0 스트라이크 , 1 볼, 2 아웃, 3 안타 생성
	// 0~3을 랜덤으로 생성하여 무작위 투구 구현	
        function pitch() {
            let pitch = Math.floor(Math.random() * 4);
            return pitch;
        }
        
        
				// 랜덤한 투구 볼 카운트 판단 함수
				// 랜덤 투구에서 발생한 숫자를 각 조건에 맞게 처리
        function pitchPrint(num) {
            switch (num) {
                case 0:
                    strike();
                    break;

                case 1:
                    ball();
                    break;

                case 2:
                    hit();
                    break;

                default:
                    out();
                    break;
            }
        }

        //스트라이크일때 결과 출력 및 값 수정
				//화면에 값을 출력하고 스트라이크 카운트 증가
        function strike() {
            document.write("스트라이크!<br>");
            ballCount[0]++;
        }
        
        //볼일때 결과 출력 및 값 수정
				//화면에 값을 출력하고 볼 카운트 증가
        function ball() {
            document.write("볼!<br>");
            ballCount[1]++;
        }
        
        //아웃일때 결과 출력 및 값 수정
				//화면에 값을 출력하고 볼 카운트 증가
        function out() {
            document.write("아웃!  다음 타자가 타석에 입장했습니다.<br>");
            ballCount[2]++;
            ballCount[0] = 0; //스트라이크 회수 초기화
            ballCount[1] = 0; //볼 회수 초기화
        }
        
        //안타일때 결과 출력 및 값 수정
				//화면에 값을 출력하고 안타 카운트 증가
        function hit() {
            document.write("안타!  다음 타자가 타석에 입장했습니다.<br>");
            ballCount[3]++;
            ballCount[0] = 0; //스트라이크 회수 초기화
            ballCount[1] = 0; //볼 회수 초기화
        }

        //현재 볼카운트 출력
        function ballCountPrint() {
            document.write(ballCount[0] + "S "
                + ballCount[1] + "B "
                + ballCount[2] + "O<br><br>");
        }

        //최종 안타수 출력
        function hitCountPrint() {
            document.write("최종안타수: " + ballCount[3] + "<br>");
        }
				
				//메인 함수 프로그래밍 조건에 맞게 실행
        function main() {
            while (ballCount[2] < 3) {
                pitchPrint(pitch());
                if (ballCount[0] === 3) out();
                if (ballCount[1] === 4) hit();
                ballCountPrint();
            }
            hitCountPrint();
            document.write("Game Over<br>")
        }
```

