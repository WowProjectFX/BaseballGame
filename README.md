```javascript
       let team1 = [],
           team2 = [],
           ballCount = [0, 0, 0, 0], //[0] 스트라이크 , [1] 볼, [2] 아웃, [3] 안타 횟수 저장
           team1ScoreCnt = 0, //각회별 점수 계산
           team2ScoreCnt = 0,
           team1Score = [0, 0, 0, 0, 0, 0], //각회별 점수 저장
           team2Score = [0, 0, 0, 0, 0, 0],
           team1PlayerCnt = 1, //플레이어 카운트
           team2PlayerCnt = 1,
           team1PitchCnt = 0, //투구수 카운트
           team2PitchCnt = 0,
           team1StrikeOuts = 0, //삼진수 카운트
           team2StrikeOuts = 0,
           team1Hitcnt = 0, //안타수 카운트 
           team2Hitcnt = 0,
           num = 1; //스킵 후 원하는 회차 저장


        function Player(no, name, hitRate) { // 플레이어 정보 객체를 만들기 위한 생성자
            this.no = no;
            this.name = name;
            this.hitRate = hitRate;
        }

        function PlayerBallCnt(strike, ball, out, hit) { // 플레이어 정보 객체를 만들기 위한 생성자
            this.strike = strike;
            this.ball = ball;
            this.out = out;
            this.hit = hit;
        }

        function team1NameAdd() { //1팀 이름 추가 
            let team1Name = "";
            team1Name = prompt("1번 팀의 이름을 입력하세요");
            team1.push(team1Name);
            document.write("1팀의 이름을 입력하세요> "
                + team1[0] + "<br>");
        }

        function team2NameAdd() { //2팀 이름 추가
            let team2Name = "";
            team2Name = prompt("2번 팀의 이름을 입력하세요");
            team2.push(team2Name);
            document.write("2팀의 이름을 입력하세요> "
                + team2[0] + "<br>");
        }

        function team1PlayerTest() { //[테스트 코드]1팀 가상 플레이어 정보 추가
            team1.push("코드스쿼드");

            for (let i = 0; i < 9; i++) {
                let ran = ((Math.random() * 4 + 1) / 10).toFixed(3);
                player = new Player(i + 1, "[team1] " + (i + 1) + "번 타자", ran);
                team1.push(player);
                document.write(team1[i + 1].name + ", " + team1[i + 1].hitRate + "<br>");
            }
        }

        function team2PlayerTest() { //[테스트 코드]2팀 가상 플레이어 정보 추가
            team2.push("마블 어벤져스");

            for (let i = 0; i < 9; i++) {
                let ran = ((Math.random() * 4 + 1) / 10).toFixed(3);
                player = new Player(i + 1, "[team2] " + (i + 1) + "번 타자", ran);
                team2.push(player);
                document.write(team2[i + 1].name + ", " + team2[i + 1].hitRate + "<br>");
            }
        }

        function team1PlayerAdd() { //1팀 플레이어 정보 추가 
            let input = "",
                inputArray = [],
                player = {};

            for (let i = 0; i < 9; i++) {
                document.write((i + 1) + "번 타자 정보를 입력>");
                input = prompt("타자이름, 타율");
                inputArray = input.split(", ");
                player = new Player(i + 1, inputArray[0], inputArray[1]);
                team1.push(player);
                document.write(team1[i + 1].name + ", " + team1[i + 1].hitRate + "<br>");
            }
        }

        function team2PlayerAdd() { //2팀 플레이어 정보 추가
            let input = "",
                inputArray = [],
                player = {};

            for (let i = 0; i < 9; i++) {
                document.write((i + 1) + "번 타자 정보를 입력>");
                input = prompt("타자이름, 타율");
                inputArray = input.split(", ");
                player = new Player(i + 1, inputArray[0], inputArray[1]);
                team2.push(player);
                document.write(team2[i + 1].name + ", " + team2[i + 1].hitRate + "<br>");
            }
        }

        function team1Info() { //1팀 정보 출력
            document.write(team1[0] + " 팀 정보><br>");
            for (let i = 1; i < team1.length; i++) {
                document.write(i + "번 " + team1[i].name + ", " + team1[i].hitRate + "<br>");
            }
        }

        function team2Info() { //2팀 정보 출력
            document.write(team2[0] + " 팀 정보><br>");
            for (let i = 1; i < team2.length; i++) {
                document.write(i + "번 " + team2[i].name + ", " + team2[i].hitRate + "<br>");
            }
        }

        function menuSelect() { //보기 메뉴 선택지
            document.write("<h2>신나는 야구시합</h2>");
            document.write("1. 데이터 입력 <br>");
            document.write("2. 데이터 출력 <br>");
            document.write("3. 시합 시작 <br><br>");
        }

        function menuPrompt() { //메뉴 선택 값 받기
            let menu = Number(prompt(
                "신나는 야구시합\n"
                + "1. 데이터 입력\n"
                + "2. 데이터 출력\n"
                + "3. 시합 시작\n"
                + "4. 테스트\n"
                + "메뉴를 선택하세요\n" + "(테스트코드실행 4->2->3)"));
            document.write("메뉴선택( 1 - 2 ) " + menu + "<br>");
            return menu;
        }

        function pitch() { // 랜덤한 투구 - 0 스트라이크 , 1 볼, 2 아웃, 3 안타 생성
            let pitch = Math.floor(Math.random() * 4);
            return pitch;
        }

        function hitRatePitch(h) { // 타자별 타율에 따른 랜덤한 투구 - 0 스트라이크 , 1 볼, 2 아웃, 3 안타 생성
            let pitch = Math.random().toFixed(3); //소수점 3자리 값을 가지는 랜덤한 투구 생성 (0.000 ~ 0.999)
            console.log("pitch: " + pitch);

            let percent = []; //타자별 타율 저장
            percent.push(0.1); //아웃일 확률 10%
            percent.push((1 - h) / 2 - 0.05); //볼일 확률 
            percent.push((1 - h) / 2 - 0.05); //스타라이크일 확률 
            percent.push(Number(h)); //안타일 확률 3
            console.log("percent: " + percent);

            let cumulative = 0.000; //순서대로 누적값 저장 1. 아웃 + 2. 볼 + 3. 스크라이크 + 4. 안타  
            let ranHit = 3; //최종 결과

            for (let i = 0; i < 4; i++) {
                cumulative += percent[i];
                console.log("cumulative: " + cumulative);
                if (pitch <= cumulative) {
                    if (i === 3) return ranHit;
                    else return ranHit = 2 - i;
                    console.log("ranHit: " + ranHit);
                }
            }
            return ranHit;
        }

        function strike() { //스트라이크일때 결과 출력 및 값 수정
            document.write("스트라이크!<br>");
            ballCount[0]++;
            ballCountPrint();
        }

        function ball() { //볼일때 결과 출력 및 값 수정
            document.write("볼!<br>");
            ballCount[1]++;
            ballCountPrint();
        }

        function out() { //아웃일때 결과 출력 및 값 수정
            document.write("아웃!  다음 타자가 타석에 입장했습니다.<br>");
            ballCount[2]++;
            ballCount[0] = 0; //스트라이크 회수 초기화
            ballCount[1] = 0; //볼 회수 초기화
            ballCountPrint();
        }

        function hit() { //안타일때 결과 출력 및 값 수정
            document.write("안타!  다음 타자가 타석에 입장했습니다.<br>");

            ballCount[3]++;
            ballCount[0] = 0; //스트라이크 회수 초기화
            ballCount[1] = 0; //볼 회수 초기화
            ballCountPrint();
        }

        function ballCountPrint() { //현재 볼카운트 출력
            document.write(ballCount[0] + "S "
                + ballCount[1] + "B "
                + ballCount[2] + "O<br><br>");
        }

        function hitCountPrint() { //최종 안타수 출력
            document.write("최종안타수: " + ballCount[3] + "<br>");
            return ballCount[3];
        }

        function team1PlayerLotation() { //1팀 플레이어 순서 저장 (1번 ~ 9번 타자 로테이션)
            document.write(team1PlayerCnt + "번 타자" + team1[team1PlayerCnt].name + "입니다.<br>");
            if (team1PlayerCnt === 9) {
                team1PlayerCnt = 0;
            }
            team1PlayerCnt++;
        }

        function team2PlayerLotation() { //2팀 플레이어 순서 저장 (1번 ~ 9번 타자 로테이션)
            document.write(team2PlayerCnt + "번 타자" + team2[team2PlayerCnt].name + "입니다.<br>");
            if (team2PlayerCnt === 9) {
                team2PlayerCnt = 1;
            } else {
                team2PlayerCnt++;
            }
        }

        function team1Attack() { //1팀 공격
            team1PlayerLotation();
            do {

                team1PitchCnt++;

                if (ballCount[2] === 3) { //아웃이 3번이면 공격 종료 
                    return;
                }

                if (ballCount[0] === 3) { //스트라이크가 3번이면 아웃
                    team1StrikeOuts++;
                    out();
                    team1PlayerLotation()
                }
                if (ballCount[1] === 4) { //볼이 4번이면 안타
                    hit();
                    team1PlayerLotation()
                }

                switch (hitRatePitch(team1[team1PlayerCnt - 1].hitRate)) {

                    case 0: strike();
                        break;
                    case 1: ball();
                        break;
                    case 2: out();
                        break;
                    default:
                        hit();
                        team1PlayerLotation();
                        break;
                }
            } while (ballCount[2] < 3)

        }

        function team2Attack() { //2팀 공격
            team2PlayerLotation();
            do {

                team2PitchCnt++;

                if (ballCount[2] == 3) {
                    return;
                } else if (ballCount[0] === 3) {
                    team2StrikeOuts++;
                    out();
                    team2PlayerLotation()
                }
                if (ballCount[1] === 4) {
                    hit();
                    team2PlayerLotation()
                }

                switch (hitRatePitch(team2[team2PlayerCnt - 1].hitRate)) {

                    case 0: strike();
                        break;
                    case 1: ball();
                        break;
                    case 2: out();
                        break;
                    default:
                        hit();
                        team2PlayerLotation();
                        break;
                }
            } while (ballCount[2] < 3)

        }

        function team1ScoreCount(i) { //1팀 각회별 점수 저장
            if (ballCount[3] > 3) team1ScoreCnt = ballCount[3] - 3;
            team1Score[i - 1] = team1ScoreCnt;
        }

        function team2ScoreCount(i) { //2팀 각회별 따른 점수 저장
            if (ballCount[3] > 3) team2ScoreCnt = ballCount[3] - 3;
            team2Score[i - 1] = team2ScoreCnt;;
        }

        function team1Tot() { //1팀 최종 점수 합계
            let sum = team1Score.reduce((a, x) => a += x, 0);
            return sum;
        }

        function team2Tot() { //2팀 최종 점수 합계
            let sum = team2Score.reduce((a, x) => a += x, 0);
            return sum;
        }

        function teamRegistration() { // 메뉴1번 선택시 팀이름 및 선수 등록

            team1NameAdd();
            team1PlayerAdd();
            document.write("<br>");
            team2NameAdd();
            team2PlayerAdd();
            document.write("팀 데이터 입력이 완료 되었습니다.");
            alert("입력완료!!!")
        }

        function teamInfoPrint() { // 메뉴2번 선택시 팀 정보 출력
            team1Info();
            document.write("<br>");
            team2Info();
            alert("출력완료!!!")
        }

        function test() { // [테스트코드] 가상의 팀, 선수 등록 
            team1PlayerTest();
            document.write("=============================================<br>");
            team2PlayerTest();
        }

        function team1Action(i) { // 1팀 공격 및 점수 출력
            document.write(i + " 회초 " + team1[0] + "공격<br><br>");
            team1Attack();
            team1ScoreCount(i);
            team1Hitcnt += hitCountPrint();
            document.write(i + "회초 득점: " + team1Score[i - 1] + "<br>");
            document.write("=============================================<br>");
        }

        function team2Action(i) {  // 2팀 공격 및 점수 출력 
            document.write(i + " 회말 " + team2[0] + "공격<br><br>");
            team2Attack();
            team2ScoreCount(i);
            team2Hitcnt += hitCountPrint();
            document.write(i + "회말 득점: " + team2Score[i - 1] + "<br>");
            document.write("=============================================<br>");
        }

        function scoreBoard() { //전광판에 팀별 각회당 점수 표시

            document.write("<table>");
            document.write("<tr>");
            document.write("<th></th>");

            for (let i = 1; i < 7; i++) {
                document.write("<th>" + i + "</th>");
            }
            document.write("<th>Tot</th>");

            document.write("</tr>");

            team1ScoreBoard();
            team2ScoreBoard();

            document.write("</table>");
        }

        function team1ScoreBoard() { //1팀 각회당 점수 표시

            document.write("<tr>");
            document.write("<td>" + team1[0] + "</td>");

            for (let i = 0; i < 6; i++) {
                document.write("<td>" + team1Score[i] + "</td>");
            }

            document.write("<td>" + team1Tot() + "</td>");
            document.write("</tr>");
        }

        function team2ScoreBoard() { //2팀 각회당 점수 표시

            document.write("<tr>");
            document.write("<td>" + team2[0] + "</td>");

            for (let i = 0; i < 6; i++) {
                document.write("<td>" + team2Score[i] + "</td>");
            }

            document.write("<td>" + team2Tot() + "</td>");
            document.write("</tr>");
            document.write("<br><br>");

        }

        function team1Board() { //1팀 현재 플레이어 상황 출력 

            document.write("<div>");
            document.write("<h3>" + team1[0] + "</h3>");
            for (let i = 1; i < team1.length; i++) {
                document.write(team1[i].no + ". " + team1[i].name + "<br>");
            }
            document.write("<br>")
            document.write("투구: " + team1PitchCnt + "<br>")
            document.write("삼진: " + team1StrikeOuts + "<br>")
            document.write("안타: " + team1Hitcnt + "<br>")
            document.write("</div>")
        }

        function team2Board() { //2팀 현재 플레이어 상황 출력

            document.write("<div>");
            document.write("<h3>" + team2[0] + "</h3>");
            for (let i = 1; i < team2.length; i++) {
                document.write(team2[i].no + ". " + team2[i].name + "<br>");
            }
            document.write("<br>")
            document.write("투구: " + team2PitchCnt + "<br>")
            document.write("삼진: " + team2StrikeOuts + "<br>")
            document.write("안타: " + team2Hitcnt + "<br>")
            document.write("</div>")
            document.write("<br><br>")
        }

        function gameReady() { //게임 시작 준비 - 메뉴 선택 및 실행
            let menu = 0;

            do {
                menuSelect();
                menu = menuPrompt();

                switch (menu) {
                    case 1:
                        teamRegistration();
                        break;
                    case 2:
                        teamInfoPrint();
                        break;
                    case 3:
                        gameStart()
                        break;
                    case 4:
                        test();
                        break;
                    default:
                        alert("1-3 보기중 하나를 고르세요!!!")
                        break;
                }

            } while (!(menu === 3))
        }

        function gameStart() { // 게임 시작
            document.write(team1[0] + " vs " + team2[0] + "의 시합을 시작합니다.<br><br>");
            let skip = 0;

            do {// 1~6 선택시 해당 회에서 바로 시작

                skip = Number(prompt("스킵하고 x회말 후 투구 보기(숫자+enter) ? "));
                console.log(skip);

            } while (skip === 0);

            let i, j; //i는 회 j 는 팀 ( 1 = 1팀 , 2 = 2팀)

            for (i = 1; i <= skip; i++) { //회

                for (j = 1; j < 3; j++) { // 초 / 말
                    ballCount = [0, 0, 0, 0];
                    
                  	// 6회말에 2팀이 1팀보다 점수가 높으면 게임 종료
                    if(i === 6 &&  j=== 2 && team2Tot() > team1Tot()) return; 

                    if (j === 1) {
                        team1Action(i);
                    } else {
                        team2Action(i);
                    }
                }

            }
        }

        function gameOver() { //게임 종료
            document.write("경기종료<br><br>")
            document.write(team1[0] + " vs " + team2[0] + "<br>");
            document.write(team1Tot() + " : " + team2Tot() + "<br>");
            document.write("Thank you<br>")
        }
```

