# Simion-says-game
Hi I am Purbendu Chakraborty A student of Netaji Subhash Engineering College , currently I am in 3rd year IT department . this is the simon G game  says game using HTML,CSS and JS.
 /// HTML code ////
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simon Says Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Simon Says game</h1>
    <h2>Press any key to Start</h2>
    <div class="btn-container">
        <div class="line-one">

            <div class="btn red" id="red" type="button">1</div>
            <div class="btn orange" id="orange" type="button">2</div>
        </div>
        <div class="line-two">
            <div class="btn green" id="green" type="button">3</div>
            <div class="btn blue" id="blue" type="button">4</div>
        </div>
        
    </div>
    <script src="script.js"></script>
</body>
</html>

/// CSS code ///
*
{
    margin: 0px;
    padding: 0px;
}
body
{
    text-align: center;
}
.btn
{
    height: 200px;
    width: 200px;
    border-radius: 20%;
    border: 10px solid black;
    margin: 2.5rem;
}
.btn-container
{
    display: flex;
    justify-content: center;

}
.red
{
    background-color: #b31313;
}
.green
{
    background-color: rgb(18, 57, 18);
}
.orange
{
    background-color: orange;
}
.blue
{
    background-color: rgb(10, 63, 160);
}
.flash
{
    background-color: aliceblue;
}

// Js code //
let gameseq=[];
let usuerseq=[];

let started=false;
let level=0;

let btns=["red","orange","blue","green"];


let h2=document.querySelector("h2");

document.addEventListener("keypress", function(){
    if(started==false)
    {
        console.log("Game started");
        started = true;


        levelup();

    }

});



function levelup()
{
    usuerseq=[];
    level++;
    h2.innerText=`Level ${level}`;
    // random button choose

    let randinx=Math.floor(Math.random() * 3);
    let rancolor=btns[randinx];
    let randbtn=document.querySelector(`.${rancolor}`);
    // console.log(randinx);
    // console.log(rancolor);

    // console.log(randbtn);
    gameseq.push(rancolor);
    console.log("Game sequence is",gameseq);
    



    btnflash(randbtn);
}

function btnflash(btn)
{
   btn.classList.add("flash");
   setTimeout(function() {
    btn.classList.remove("flash");
   },250);

}

 function checkans(idx)
{
    //let idx=level-1;
//     usuerseq=[];

     console.log("Curr level is: ",level);

    if(usuerseq[idx] === gameseq[idx])
    {
        if(usuerseq.length==gameseq.length)
        {
            setTimeout(levelup,1000);

        }
    }
    else
    {
        h2.innerHTML=`game over !!Your score was <b> ${level} </b> <br>  Preass any ket to start`;
        document.querySelector("body").style.backgroundColor="red";
        setTimeout(function(){
           document.querySelector("body").style.backgroundColor="white";

        },150)
        reset();
    }
}    

function btnpress()
{
    console.log(this);

    let btn=this;
   btnflash(btn);

   //usuercolor=btn.getAttribute("id");
//    console.log(usuercolor);
//    usuerseq.push(usuercolor);

   usuercolor=btn.getAttribute("id");
   //console.log(usuercolor);
   usuerseq.push(usuercolor);
   console.log("Usuer sequence is",usuerseq);

   checkans ( usuerseq.length-1 );

   

}

let allbtns= document.querySelectorAll(".btn");

for(let  btn of allbtns)
{
    btn.addEventListener("click",btnpress);

}

function reset()
{
    started=false;
    gameseq=[];
    usuerseq=[];
    level=0;

}

 
