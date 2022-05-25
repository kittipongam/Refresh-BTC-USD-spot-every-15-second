# Refresh BTC-USD spot every 15 second


## Introduction
Web Service เป็นตัวกลางในการสื่อสารข้อมูล เช่นต้องการรู้ราคา Bitcoin
หรือ Cryptocurrency ตัวไหน ก็ส่งคําถามไปที่ Web Service ของ Coinbase ได้ โดยจะส่งไปถามราคาจากเว็ปของ coinbase และเขียนคำสั่งให้ refresh ทำงานทุกๆ 15 นาทีเพื่อแสดงผลลัพธ์ราคาที่อัพในเเต่ละ 15 วินาที

### Add some title and button
//button with event onclick to command refresh function
>
    <title>BTC-USD-spot</title>
    <button onclick="refresh()">refresh</button>
>


### fetch command and convert to JSON
use fetch command with url and convert to JSON(Java Scipt Object Notation and show to use innerText command)
>
    function refresh(){
                var url="https://api.coinbase.com/v2/prices/BTC-USD/spot"
                fetch(url).then(convert).then(show)
                startTime()
            }
            function convert(response){
                return response.json()
            }
            var e =document.getElementById("target")
            function show(data){
    
                e.innerText=data.data.amount
            }
>

### Adding some timer 
// let's add some clock watch
>
    <div class="timmerWatch">
        <p><span id="seconds">00</span>:<span id="tens">00</span></p>
    </div>
>
// let's add some clock watch function
>
            var timeToRefresh =15;   //as a variable to refresh every 15 seconds
            var seconds = 00;
            var tens = 00;
            var appendTens = document.getElementById("tens");
            var appendSeconds = document.getElementById("seconds");
            var Interval;
            function startTime() {
                clearInterval(Interval);
                Interval = setInterval(startTimer, 10); 
            }
            function resetTime() {
                clearInterval(Interval);
                tens = "00";
                seconds = "00";
                appendTens.innerHTML = tens;
                appendSeconds.innerHTML = seconds;    
            }
            async function startTimer() {
                tens++;
                if (tens < 9) {
                    appendTens.innerHTML = "0" + tens;
                }
                if (tens > 9) {
                    appendTens.innerHTML = tens;
                }
                if (tens > 99) {
                    seconds++;
                    appendSeconds.innerHTML = "0" + seconds;
                    tens = 0;
                    appendTens.innerHTML = "0" + 0;
                }
                if (seconds == timeToRefresh) {   
                    await resetTime()
                    await refresh()
                }
                if (seconds > 9) {
                    appendSeconds.innerHTML = seconds;
                }
    }
>


### Result

here is the result to refresh value BTC-USD spot from coinbase every 15 seconds

![image](https://user-images.githubusercontent.com/104770048/170193303-c86a3e8a-bdad-4003-b45a-c6d08e91b674.png)
