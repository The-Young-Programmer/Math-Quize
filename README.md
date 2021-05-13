<!-- Created by The Young Programmer aka NemoNet -->
<html>
 <head> 
  <title>Math yQuiz</title> 
  <meta name="viewport" content="width=device-width, initial-scale=1"> 
  <style type="text/css">
  /* Created by NemoNet */

@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
body {
    font-family: 'Poppins', sans-serif;
    text-align: center;
    background: linear-gradient(90deg, rgba(13,120,207,1) 19%, rgba(18,182,231,1) 93%);
    color:white;
}
#question {
    font-size: 40px;
    font-weight: bold;
}
button, input {
    font-family: 'Poppins', sans-serif;
    font-weight: bold;
    
}
input {
    height: 42px;
    font-size: 30px;
    width: 150px;
    text-align: center;
    color: rgba(13,120,207,1);
    border: 2px solid white;
    margin: 8px;
    border-radius: 10px;
}
#quizbody button {
    width: 100px;
    height: 50px;
    margin: 8px;
    font-size: 22px;
    background-color: transparent;
    color: white;
    font-weight: bold;
    border: 2px solid white;
    border-radius: 15px;
}
#serial {
    font-size: 22px;
    font-weight: bold;
}
#diff button {
    width: 180px;
    height: 50px;
    margin: 8px;
    font-size: 21px;
    background-color: transparent;
    color: white;
    font-weight: bolder;
    border: 2px solid white;
    border-radius: 10px;
}

#result {
    font-size: 25px;
    font-weight: bold;
}
.titlebar {
    margin: 10px;
}
.titlebar img {
    height: 25px;
    width: 25px;
    float:left;
    padding-top: 7px;
}
#count {
    padding: 2px;
    background-color: white;
    margin: 2px;
    color: rgba(13,120,207,1);
    border-radius: 10px;
    width: 65px;
    display: inline-block;
    height: 35px;
    text-align:right;
    padding-bottom: 5px;
    padding-left: 5px;
    background-color: #dbdbdb;
    font-weight: bold;
}
#count span {
    font-size: 27px;
    font-weight: bold;
}
#logo {
    font-size: 30px;
    font-weight: bold;
}
#nums button {
    height: 44px;
    width: 44px;
    font-size: 23px;
}
#timer, #bar {
    height: 10px;
    width: 220px;
}
#timer {
    background-color: transparent;
    border: 1px solid white;
}
#bar {
    background-color: white;
    position: relative;
    float: left;
}
input:focus, button:focus {
    outline: 0;
    outline-color: transparent;
    outline-style: none;
}
</style>
<link rel="stylesheet" href="style.css"> 
  <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script> 
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@9"></script> 
  
 </head> 
 <body> 
 <script>
     
     // Created by NemoNet
var myTimeout = setTimeout(function() {
         alert("Hello 🖐 .....am NemoNet aka The Young Programmer\n     This my first programming game "); 
         alert("pls kindly give me a star 🌟 on WhatsApp")
      }, 15000);
      
//Declaring Variables
var count=1, total=0, correct=0, wrong=0, lim=0;
var ans = "", question ="", input="", width= 220, t = '', n1, n2, n3, r1, r2, mode=0;
var opr = [];

//Hide Quiz Body At Start
$(document).ready(function() {
    $("#quizbody").hide();
});

//Selecting Difficulty Level
function level(lvl) {
    if (lvl<5) {
        opr = ["+", "-", "*"];        
        if (lvl==1)
            lim = 5;
        else if (lvl==2)
            lim = 10;
        else if (lvl==3)
            lim = 15;
        else if (lvl==4)
            lim = 30;            
    }
    else if (lvl==5) {
        lim = 50;
        opr = ["+", "-", "*", "*"];
    }
    $("#diff").hide();
    $("#quizbody").show();
    if (mode==1) {
        $("#donebtn").hide();
    }
    else {
        $("#donebtn").show();
    }
    quiz();
}

//Generating Questions
function quiz() {
    var len = opr.length;    
    n1 = Math.floor(Math.random() * lim);
    n2 = Math.floor(Math.random() * lim);
    n3 = Math.floor(Math.random() * lim);    
    r1 = opr[Math.floor(Math.random()*len)];
    r2 = opr[Math.floor(Math.random()*len)];    
    question = n1+r1+n2+r2+n3;
    ans = eval(question);
    $("#question").html(question+" = ?");
    t = setInterval(timeCheck, 120);
}

//Checking Answer
function check() {
    var input = $("#answer").val();
    if(input == ans) {
        Swal.fire({
          icon: 'success',
          title: 'Correct',
          text: ans + ' is correct.',
          showConfirmButton: false,
          timer: 1500
        });
        correct++;
        $("#correct").html(correct);
    }
    else {
        Swal.fire({
          icon: 'error',
          title: 'Wrong',
          text: 'The answer was '+ans,
          showConfirmButton: false,
          timer: 1500
        });
        wrong++;
        $("#wrong").html(wrong);
    } 
    $("#answer").val('');
    count++;
    total++;
    $("#no").html(count);
    $("#total").html(total);
    clearInterval(t);
    width = 220;
    bar.style.width = '200px';
    quiz();
}

//Inserting Numbers
function ins(num) {
    var chk = $("#answer").val().includes(".");
    if ($("#answer").val() != '' && num == '-' || num == "." && chk)
    {
      //do nothing  
    }
    
    else {
      $("#answer").val($("#answer").val() + num);
      if (mode==1) {
          if ($("#answer").val() ==ans)
              check();
      }
    }      
}

//Timer
function timeCheck() {
    var bar = document.getElementById("bar");
    if(width == 0) {
        clearInterval(t);
        Swal.fire({
          icon: 'warning',
          title: 'Timeout',
          text: 'The answer was '+ans,
          showConfirmButton: false,
          timer: 1500
        });
        wrong++;
        $("#wrong").html(wrong);
    quiz();
    width = 220;
    bar.style.width = '200px';
    }
    else {
        width--;
        bar.style.width = width+'px';
    }
}

//Other Functions
$(function() {

   //Quick mode
    $("#mode").click(function() {
        if (mode==0) {
            $(this).html("Quick Mode (ON)");
            mode=1;
        }
        else {
            $(this).html("Quick Mode (OFF)");
            mode=0;
        }
    });
    
    //Reseting
    $("#res").click(function() {
        $("#diff").show();
        $("#quizbody").hide();
        count=1, total=0, correct=0, wrong=0, lim=0;
        $("#correct").html(correct);
        $("#wrong").html(wrong);
        $("#total").html(total);
        input.value = "";
        clearInterval(t);
        width = 220;
        bar.style.width = '200px';
    });
    
    //Deleting a number
    $("#del").click(function() {
        var txt = $("#answer").val();
        txt = txt.slice(0, -1);
        $("#answer").val(txt);
    });
   
   //Explaining Quick mode 
    $("#ex").click(function() {
        Swal.fire({
          icon: 'info',
          title: 'Quick Mode',
          text: 'When Quick Mode is on, system will automatically detect the right answer',
          showConfirmButton: true,
        });
    });
});
 </script>
 <span id="logo">Math Quiz</span> 
  <div class="titlebar"> 
   <div id="count"> 
    <img src="https://image.flaticon.com/icons/svg/1277/1277603.svg"> 
    <span id="total">0</span> 
   </div> 
   <div id="count"> 
    <img src="https://image.flaticon.com/icons/svg/1277/1277588.svg"> 
    <span id="correct">0</span> 
   </div> 
   <div id="count"> 
    <img src="https://image.flaticon.com/icons/svg/1277/1277612.svg"> 
    <span id="wrong">0</span> 
   </div> 
  </div> 
  <div id="diff"> 
   <h2>Select level</h2> 
   <button onclick="level(1)">Very Easy</button> 
   <br> 
   <button onclick="level(2)">Easy</button> 
   <br> 
   <button onclick="level(3)">Medium</button> 
   <br> 
   <button onclick="level(4)">Hard</button> 
   <br> 
   <button onclick="level(5)">Very Hard</button> 
   <div style="height:20px"></div> 
   <button style="height: 40px;width:220px" id="mode">Quick Mode (OFF)</button> 
   <button style="width:40px;height:40px" id="ex">?</button> 
  </div> 
  <div id="quizbody"> 
   <div style="height:10px"></div> 
   <div id="serial"> 
    <span>Question. </span> 
    <span id="no">1</span> 
   </div> 
   <p id="question"></p> 
   <center> 
    <div id="timer"> 
     <div id="bar"></div> 
    </div> 
   </center> 
   <br> 
   <input id="answer" readonly> 
   <button id="del" style="width:45px;padding:5px;">←</button> 
   <br> 
   <button id="donebtn" onclick="check()">Done</button> 
   <div id="nums"> 
    <button onclick="ins(1)">1</button> 
    <button onclick="ins(2)">2</button> 
    <button onclick="ins(3)">3</button> 
    <button onclick="ins(4)">4</button> 
    <br> 
    <button onclick="ins(5)">5</button> 
    <button onclick="ins(6)">6</button> 
    <button onclick="ins(7)">7</button> 
    <button onclick="ins(8)">8</button> 
    <br> 
    <button onclick="ins(9)">9</button> 
    <button onclick="ins(0)">0</button> 
    <button onclick="ins('-')">-</button> 
    <button onclick="ins('.')">.</button> 
   </div> 
   <br> 
   <button id="res">Reset</button> 
  </div> 
  <br /><br />
  <footer> 
   <a style="color:white;" href="https://wa.me/2348156622466?text=I%20Love%20your%20programming,%20my%20name%20is%20" target="_blank"> WhatsApp </a> 
  </footer> 
  <script src="script.js"></script> 
 </body>
</html>
