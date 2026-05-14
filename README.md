<!DOCTYPE html>
<html lang="hi">

<head>

<meta charset="UTF-8">

<meta name="viewport"
content="width=device-width, initial-scale=1">

<title>VKR FREE STUDY.</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
}

body{

font-family:Arial,sans-serif;

background:
linear-gradient(135deg,#1e3c72,#2a5298);

min-height:100vh;

overflow-x:hidden;

}

.container{

width:100%;

max-width:700px;

margin:auto;

background:white;

min-height:100vh;

padding:20px;

}

.logo{

text-align:center;

font-size:34px;

font-weight:bold;

margin-bottom:20px;

color:#1e3c72;

}

.card{

background:#fff;

padding:20px;

border-radius:15px;

box-shadow:0 0 15px rgba(0,0,0,0.2);

margin-top:15px;

}

input{

width:100%;

padding:18px;

margin:12px 0;

border-radius:12px;

border:1px solid #ccc;

font-size:20px;

}

button{

width:100%;

padding:18px;

margin-top:12px;

border:none;

border-radius:12px;

font-size:20px;

cursor:pointer;

transition:0.3s;

}

#loginBtn{

background:#28a745;

color:white;

}

.option{

background:#f1f1f1;

text-align:left;

}

.option:hover{

background:#ddd;

}

.correct{

background:green !important;

color:white;

}

.wrong{

background:red !important;

color:white;

}

#nextBtn{

background:#007bff;

color:white;

display:none;

}

#timer{

font-size:32px;

font-weight:bold;

text-align:right;

color:red;

margin-bottom:15px;

}

#question{

font-size:28px;

line-height:1.5;

margin-bottom:20px;

}

#result{

text-align:center;

font-size:30px;

font-weight:bold;

margin-top:30px;

line-height:1.6;

}

.progress{

width:100%;

height:12px;

background:#ddd;

border-radius:10px;

overflow:hidden;

margin-bottom:20px;

}

.progress-bar{

height:100%;

width:0%;

background:#28a745;

transition:0.3s;

}

@media screen and (max-width:600px){

.container{

padding:15px;

}

.logo{

font-size:28px;

}

#question{

font-size:23px;

}

input{

font-size:18px;

padding:16px;

}

button{

font-size:18px;

padding:16px;

}

}

</style>

</head>

<body>

<audio id="correctSound">
<source
src="https://www.soundjay.com/buttons/sounds/button-3.mp3"
type="audio/mpeg">
</audio>

<audio id="wrongSound">
<source
src="https://www.soundjay.com/buttons/sounds/button-10.mp3"
type="audio/mpeg">
</audio>

<div class="container">

<div class="logo">
𝗩𝗞𝗥 𝗙𝗥𝗘𝗘 𝗦𝗧𝗨𝗗𝗬
<br>📖 Reasoning Class–01
</div>

<div class="card" id="loginBox">

<h2 style="text-align:center;">
Student Login
</h2>

<input
type="text"
id="userid"
placeholder="Enter User ID">

<input
type="password"
id="password"
placeholder="Enter Password">

<button id="loginBtn">
Start Quiz
</button>

</div>

<div id="quizBox"
style="display:none;">

<div class="progress">

<div class="progress-bar"
id="progressBar"></div>

</div>

<div id="timer">20</div>

<div class="card">

<h2 id="question"></h2>

<div id="options"></div>

<button id="nextBtn">
Next Question
</button>

</div>

</div>

<div id="result"></div>

</div>

<script>

// =======================
// LOGIN DATA
// =======================

 const users = [

{id:"Abhinav", pass:"1001"},
{id:"Ankush", pass:"1002"},
{id:"Khusbu", pass:"1003"},
{id:"Rahul", pass:"1004"},
{id:"Rohan", pass:"1005"},
{id:"Aman", pass:"1006"},
{id:"Suman", pass:"1007"},
{id:"Neha", pass:"1008"},
{id:"Pooja", pass:"1009"},
{id:"Priya", pass:"1010"},

{id:"Ritika", pass:"1011"},
{id:"Anjali", pass:"1012"},
{id:"Sonu", pass:"1013"},
{id:"Monu", pass:"1014"},
{id:"Vikash", pass:"9601"},
{id:"Deepak", pass:"1016"},
{id:"Karan", pass:"1017"},
{id:"Arjun", pass:"1018"},
{id:"Nitesh", pass:"1019"},
{id:"Suraj", pass:"1020"},

{id:"Radha", pass:"2535"},
{id:"Ravi", pass:"1022"},
{id:"Vivek", pass:"1023"},
{id:"Sanjay", pass:"1024"},
{id:"Ajay", pass:"1025"},
{id:"Anjani", pass:"5312"},
{id:"Sandeep", pass:"1027"},
{id:"Mukesh", pass:"1028"},
{id:"Rakesh", pass:"1029"},
{id:"Aakash", pass:"1030"},

{id:"Golu", pass:"1031"},
{id:"Chandan", pass:"1032"},
{id:"Pankaj", pass:"1033"},
{id:"Umesh", pass:"1034"},
{id:"Manish", pass:"1035"},
{id:"Niraj", pass:"1036"},
{id:"Roshan", pass:"1037"},
{id:"Shivam", pass:"1038"},
{id:"Aditya", pass:"1039"},
{id:"Ankit", pass:"1040"},

{id:"Sakshi", pass:"1041"},
{id:"Payal", pass:"1042"},
{id:"Komal", pass:"1043"},
{id:"Muskan", pass:"1044"},
{id:"Nisha", pass:"1045"},
{id:"Kajal", pass:"1046"},
{id:"Rani", pass:"1047"},
{id:"Sapna", pass:"1048"},
{id:"Simran", pass:"1049"},
{id:"Jyoti", pass:"1050"},

{id:"Tina", pass:"1051"},
{id:"Rekha", pass:"1052"},
{id:"Meena", pass:"1053"},
{id:"Kiran", pass:"1054"},
{id:"Aarti", pass:"1055"},
{id:"Seema", pass:"1056"},
{id:"Babita", pass:"1057"},
{id:"Sunita", pass:"1058"},
{id:"Geeta", pass:"1059"},
{id:"Alok", pass:"1060"},

{id:"Ashish", pass:"1061"},
{id:"Bittu", pass:"1062"},
{id:"Dilip", pass:"1063"},
{id:"Farhan", pass:"1064"},
{id:"Ganesh", pass:"1065"},
{id:"Harsh", pass:"1066"},
{id:"Imran", pass:"1067"},
{id:"Jitendra", pass:"1068"},
{id:"Kishan", pass:"1069"},
{id:"Lalit", pass:"1070"},

{id:"Mohit", pass:"1071"},
{id:"Nakul", pass:"1072"},
{id:"Omprakash", pass:"1073"},
{id:"Prashant", pass:"1074"},
{id:"Qasim", pass:"1075"},
{id:"Ritesh", pass:"1076"},
{id:"Shahrukh", pass:"1077"},
{id:"Tarun", pass:"1078"},
{id:"Uday", pass:"1079"},
{id:"Varun", pass:"1080"},

{id:"Wasim", pass:"1081"},
{id:"Yash", pass:"1082"},
{id:"Zaid", pass:"1083"},
{id:"Bhavesh", pass:"1084"},
{id:"Chetan", pass:"1085"},
{id:"Dev", pass:"1086"},
{id:"Eshan", pass:"1087"},
{id:"Faiz", pass:"1088"},
{id:"Gautam", pass:"1089"},
{id:"Himanshu", pass:"1090"},

{id:"Irfan", pass:"1091"},
{id:"Jagdish", pass:"1092"},
{id:"Krishna", pass:"1093"},
{id:"Lokesh", pass:"1094"},
{id:"Madhav", pass:"1095"},
{id:"Naresh", pass:"1096"},
{id:"Pritam", pass:"1097"},
{id:"Rupesh", pass:"1098"},
{id:"Shubham", pass:"1099"},
{id:"Yuvraj", pass:"1100"}

];

// =======================
// QUIZ QUESTIONS
// =======================

let quizData = [

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से A किस नंबर पर है? है?",
options:[
"1",
"2",
"3",
"4"
],
correct:"1"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से B किस नंबर पर है?",
options:[
"1",
"2",
"3",
"4"
],
correct:"2"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से C किस नंबर पर है?",
options:[
"1",
"2",
"3",
"4"
],
correct:"3"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से D किस नंबर पर है?",
options:[
"1",
"2",
"3",
"4"
],
correct:"4"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से E किस नंबर पर है?",
options:[
"5",
"2",
"3",
"4"
],
correct:"5"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से F किस नंबर पर है?",
options:[
"5",
"6",
"3",
"4"
],
correct:"6"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से G किस नंबर पर है?",
options:[
"5",
"6",
"7",
"8"
],
correct:"7"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से H किस नंबर पर है?",
options:[
"5",
"6",
"7",
"8"
],
correct:"8"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से I किस नंबर पर है?",
options:[
"7",
"9",
"10",
"8"
],
correct:"9"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से J किस नंबर पर है?",
options:[
"5",
"10",
"9",
"15"
],
correct:"10"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से K किस नंबर पर है?",
options:[
"10",
"13",
"11",
"12"
],
correct:"11"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से L किस नंबर पर है?",
options:[
"11",
"14",
"12",
"16"
],
correct:"12"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से M किस नंबर पर है?",
options:[
"12",
"13",
"14",
"15"
],
correct:"13"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से N किस नंबर पर है?",
options:[
"12",
"13",
"14",
"15"
],
correct:"14"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से O किस नंबर पर है?",
options:[
"13",
"5",
"10",
"15"
],
correct:"15"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से P किस नंबर पर है?",
options:[
"16",
"11",
"14",
"17"
],
correct:"16"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से Q किस नंबर पर है?",
options:[
"16",
"17",
"18",
"19"
],
correct:"17"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से R किस नंबर पर है?",
options:[
"16",
"17",
"18",
"19"
],
correct:"18"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से S किस नंबर पर है?",
options:[
"17",
"18",
"19",
"21"
],
correct:"19"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से T किस नंबर पर है?",
options:[
"19",
"20",
"21",
"22"
],
correct:"20"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से U किस नंबर पर है?",
options:[
"21",
"22",
"23",
"24"
],
correct:"21"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से V किस नंबर पर है?",
options:[
"21",
"22",
"23",
"24"
],
correct:"22"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से W किस नंबर पर है?",
options:[
"21",
"22",
"23",
"24"
],
correct:"23"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से X किस नंबर पर है?",
options:[
"21",
"22",
"23",
"24"
],
correct:"24"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से Y किस नंबर पर है?",
options:[
"22",
"23",
"24",
"25"
],
correct:"25"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से Z किस नंबर पर है?",
options:[
"25",
"26",
"22",
"21"
],
correct:"26"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'THE' नाम को अंकों में लिखें।",
options:[
"2078",
"2075",
"2085",
"2058"
],
correct:"2085"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'QUICK' नाम को अंकों में लिखें।",
options:[
"17219211",
"17219312",
"17219311",
"17218311"
],
correct:"17219311"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'BROWN' नाम को अंकों में लिखें।",
options:[
"218152314",
"218152313",
"218152113",
"218102113"
],
correct:"218152314"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'FOX' नाम को अंकों में लिखें।",
options:[
"61523",
"61521",
"61524",
"61024"
],
correct:"61524"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'JUMPS' नाम को अंकों में लिखें।",
options:[
"1021131618",
"1021131619",
"1021141619",
"1022141619"
],
correct:"1021131619"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'OVER' नाम को अंकों में लिखें।",
options:[
"1022518",
"1522519",
"1521518",
"1522518"
],
correct:"1522518"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'LAZY' नाम को अंकों में लिखें।",
options:[
"1212526",
"1212624",
"1212625",
"1211242"
],
correct:"1212625"
},

{
question:"अंग्रेजी वर्णमाला में बाएँ ओर से 'DOG' नाम को अंकों में लिखें।",
options:[
"4157",
"4175",
"4185",
"4158"
],
correct:"4157"
},
];

// =======================

let currentQuestion = 0;

let score = 0;

let timer;

let timeLeft = 20;

let studentName = "";

const loginBtn =
document.getElementById("loginBtn");

const loginBox =
document.getElementById("loginBox");

const quizBox =
document.getElementById("quizBox");

const questionEl =
document.getElementById("question");

const optionsEl =
document.getElementById("options");

const nextBtn =
document.getElementById("nextBtn");

const timerEl =
document.getElementById("timer");

const resultEl =
document.getElementById("result");

const progressBar =
document.getElementById("progressBar");

// =======================

function shuffleArray(array){

for(let i=array.length-1;i>0;i--){

let j =
Math.floor(Math.random()*(i+1));

[array[i],array[j]]=
[array[j],array[i]];

}

return array;

}

// =======================

loginBtn.onclick = ()=>{

const user =
document.getElementById("userid").value;

const pass =
document.getElementById("password").value;

let valid = false;

users.forEach(data=>{

if(
data.id == user &&
data.pass == pass
){
valid = true;
}

});

if(valid){

studentName = user;

loginBox.style.display = "none";

quizBox.style.display = "block";

shuffleArray(quizData);

loadQuestion();

startTimer();

}else{

alert("गलत User ID या Password");

}

}

// =======================

function startTimer(){

clearInterval(timer);

timeLeft = 20;

timerEl.innerText = timeLeft;

timer = setInterval(()=>{

timeLeft--;

timerEl.innerText = timeLeft;

if(timeLeft<=0){

clearInterval(timer);

nextQuestion();

}

},1000);

}

// =======================

function loadQuestion(){

nextBtn.style.display = "none";

const current =
quizData[currentQuestion];

questionEl.innerText =

(currentQuestion+1)

+ ". "

+ current.question;

optionsEl.innerHTML = "";

progressBar.style.width =

((currentQuestion+1)
/quizData.length)*100 + "%";

let options =

current.options.map(option=>({

text:option,

correct:
option===current.correct

}));

shuffleArray(options);

options.forEach((option)=>{

const btn =
document.createElement("button");

btn.innerText = option.text;

btn.classList.add("option");

btn.onclick = ()=>checkAnswer(
btn,
option.correct
);

optionsEl.appendChild(btn);

});

}

// =======================

function checkAnswer(button,isCorrect){

clearInterval(timer);

const buttons =
document.querySelectorAll(".option");

buttons.forEach(btn=>btn.disabled=true);

if(isCorrect){

document.getElementById(
"correctSound"
).play();

button.classList.add("correct");

score++;

}else{

document.getElementById(
"wrongSound"
).play();

button.classList.add("wrong");

buttons.forEach(btn=>{

if(

btn.innerText.trim()

===

quizData[currentQuestion]
.correct.trim()

){

btn.classList.add("correct");

}

});

}

nextBtn.style.display = "block";

}

// =======================

nextBtn.onclick = ()=>{

nextQuestion();

}

// =======================

function nextQuestion(){

currentQuestion++;

if(currentQuestion < quizData.length){

loadQuestion();

startTimer();

}else{

showResult();

}

}

// =======================

function showResult(){

quizBox.style.display = "none";

// DATE & TIME

let now = new Date();

let date = now.toLocaleDateString();

let time = now.toLocaleTimeString();

// ATTEMPT COUNT

let todayKey =

"R1_" +

studentName +

"_" +

date;

let attempt =

localStorage.getItem(todayKey);

if(attempt == null){

attempt = 1;

}else{

attempt = Number(attempt) + 1;

}

localStorage.setItem(
todayKey,
attempt
);

// RESULT SHOW

resultEl.innerHTML =

"🎉 " +

studentName +

"<br><br>आपका स्कोर<br><br>"

+

score +

" / "

+

quizData.length +

"<br><br>📅 Date: " +

date +

"<br><br>⏰ Time: " +

time +

"<br><br>📝 Attempt Today: " +

attempt;

}

</script>

</body>
</html>
