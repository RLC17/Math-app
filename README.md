# Math-app
# A math game that can be used to help children learn math

var playing = false;
var score; 
var action;
var timeremaining;
var correctanswer;
// If we click on start/reset
document.getElementById("startreset").onclick = function(){
  // if we are playing  
    if(playing == true){
        location.reload(); //reload page
        
    }else {   //if we are plaing then set score to 0
        
        //change mode to playing
        playing = true;
        
        //change score to 0
        score = 0;
        document.getElementById("scorevalue").innerHTML = score;
        
        //show countdown box
        show("timeremaining");
        timeremaining = 60;
        document.getElementById("timeremainingvalue").innerHTML = timeremaining;
        
        //hide gameover box
        hide("gameover");
        
        //change start to reset button
        
        document.getElementById("startreset").innerHTML = "Reset Game";
        
        //start countdown
        
        startcountdown();
        
        //generate questions and multiple answers
        
        generateQA();
    }
    
}
//Clicking on answer box

for(i=1; i<5; i++){
    document.getElementById("box"+ i).onclick = function(){
   
    // check if we are playing
    if(playing== true){
        
        if(this.innerHTML == correctanswer){
            
            //increase score by 1
            score++;
            document.getElementById("scorevalue").innerHTML = score;
            
            //hide wrong box and show correct box
            
            hide("wrong");
            show("correct");
            setTimeout(function(){
                hide("correct");
                
            }, 1000);
            
            //generate new question
           generateQA();
        }else{
            
             hide("correct");
            show("wrong");
            setTimeout(function(){
                hide("wrong");
                
            }, 1000);
        }
    }
    
}

}
//show correctbox

//console=comd+option+c

//functions

//start counter
function startcountdown(){
    
    action = setInterval(function(){
        timeremaining-= 1;
       
        document.getElementById("timeremainingvalue").innerHTML = timeremaining;
        if(timeremaining == 0){//game over
            stopcountdown();
            
            show("gameover"); 
            
            document.getElementById("gameover").innerHTML = "<p>Game over!</p><p>Your score is " + score +".</p>";
            
            hide("timeremaining");
            hide("correct");
            hide("wrong");
            playing = false;
            document.getElementById("startreset").innerHTML = "start game";
        }
            
    },1000);
}
//stop counter
function stopcountdown(){
    clearInterval(action);
}
//hide an element
function hide(id){
    
    document.getElementById(id).style.display = "none";
}
//show an element
function show(id){
    
    document.getElementById(id).style.display = "block";
}

//Generate Q&A

function generateQA(){
    var x = 1+ Math.round(9*Math.random());
    var y = 1+ Math.round(9*Math.random());
    correctanswer = x*y;
    
    document.getElementById("question").innerHTML = x + "x" + y;
    
    var correctposition = 1+ Math.round(3*Math.random());
    
    document.getElementById("box"+ correctposition).innerHTML = correctanswer; //Fill one box with the correct answer.
    
    //fill boxes with wrong answers
    
    var answers = [correctanswer];
    
    for(i=1; i<5; i++){
        
        if(i !== correctposition){
            
            var wronganswer;
            
            do{
              wronganswer = (1+ Math.round(9*Math.random()))*(1+ Math.round(9*Math.random()));
                
            } while(answers.indexOf(wronganswer)>-1);{
                
                
            }
                      
            document.getElementById("box"+i).innerHTML = wronganswer;
            wronganswer;
                      answers.push(wronganswer);
        }
    }
    
}
