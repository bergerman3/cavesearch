<html> 
  <head>
    <title>cave search web</title> 
  </head>
  <body>
	<!--This draws the canvas on the webpage -->
    <canvas id="mycanvas"></canvas> 
  </body>
 
  <!-- Include the processing.js library -->
  <!-- See https://khanacademy.zendesk.com/hc/en-us/articles/202260404-What-parts-of-ProcessingJS-does-Khan-Academy-support- for differences -->
  <script src="https://cdn.jsdelivr.net/processing.js/1.4.8/processing.min.js"></script> 
  <script>
  var programCode = function(processingInstance) {
    with (processingInstance) {
      size(600, 600); 
      frameRate(60);
//{
/*no peeking!*/var loAndBehold = ["jfhp","jgm","jce","jfs","jkl"];
//}
/**
        
                 Contest: Underground
                
         I have completed 100% of Khan Academy's 
        'Intro to JS' and have been programming 
                    for 30+ months.
    
          I would prefer to be placed in the
                      [Advanced]
                       bracket
                       
    DONE:
        -bug fixes
    TODO: (in order)
     - alot of things actually. This is version 2
         - modifiers
         - endless mode
         - tutorial
         - (potential) item rework
         - mod-making capability
         - mod tutorial (like Factori)
         - saving system in HTML export
         - mod saving system (in HTML export)
         - sound (in HTML)
     
**/
//funny function that returns true if one list of numbers has all greater or equal to numbers than the other, if both lists are the same length
var step = 0;
var selfEnd = false;
var liGrOrEqual = function(li1,li2){
    if(li1.length!==li2.length){return false;}
    for(var a = 0; a <= li1.length; a++){
        if(li1[a] < li2[a]){return false;}
    }
    return true;
};
//subtrcts two lists.
var subList = function(li1,li2){
    if(li1.length!==li2.length){return null;}
    var li3 = [];
    for(var a = 0; a < li1.length; a++){
        li3[a] = li1[a] - li2[a];
    }
    return li3;
};
var colStart = 255;
var guidePart = 1;
var diff = 5;
var craftPart = 0;
var craftSlot = null;
var craftType = null;
var craftNeeds = [[10,0,0,0,0],[20,15,0,0,0],[30,30,20,5,15],[0,0,0,0,3],[25,10,5,5,0]];
var cheatStr = "";
var mOLM = millis();
var LFX = 5;
var LFY = 5;
var gS = 0;
var lazerian = {x: 300,y: 300,hp: 500, vulnerable: true, dS: 190, lazTime: 0, timeToLaz: 480};
var winnable = false;
var lingered = false;
var sSLR = millis()+20000;
var greedy = false;
var worth = 0;
var yellow = 0;
var backRed = 0;
var pS = millis();
var kpN;
var timeSinceBegin = millis();
var timeAtEnd = millis();
var keys = {};
var plr = {x: 0,y:300,hp:100,jump: 0,gravity: true,corrosive: false};
plr.gravity = true;
var backpack = {s: 0, i: 0, g: 0, d: 0, la: 0};
/* items
    0 = pickaxe
    1 = sword
    2 = lazer rifle
    3 = medkit
    4 = jackhammer
*/
var inventory = [];
var eqIn = 0;
var hotbar = [[0,Infinity],[1,100],[4,600],[3,null],[null,null],[null,null]];
var durbs = [Infinity,200,1200,null,1000];
var equipped = 0;
var ihp = Infinity;
//sprites for tools
var weap = {};
weap.jackhammer = function(x,y){
    noStroke();
    fill(250);
    rect(x+18,y+60,3,7);
    fill(0);
    rect(x,y+10,40,5);
    rect(x+17,y+50,5,10);
    fill(190,190,0);
    rect(x+7.5,y,25,25);
    rect(x+15,y+20,10,29);
    stroke(150);
    strokeWeight(5);

};
weap.meds = function(x,y){
    noStroke();
    fill(0);
    rect(x+5,y+3.75,4,5);
    rect(x+31,y+3.75,4,5);
    rect(x+5,y,30,3.75);

    fill(150, 0, 0);
    rect(x,y+7.5,40,25);
    fill(255);
    rect(x+18,y+12.5,4,15);
    rect(x+12.5,y+17.5,15,4);
    stroke(150);
    strokeWeight(5);
};
weap.lazer = function(x,y){
    noStroke();
    fill(89, 89, 89);
    rect(x,y,50,15);
    rect(x-5,y+2.5,10,10);
    fill(212);
    rect(x+15,y+6.5,25,2);
    stroke(212, 212, 212);
    strokeWeight(2);
    line(x+40,y+7.5,x+50,y);
    line(x+40,y+7.5,x+50,y+15);
    fill(255);
    stroke(255, 0, 0,128);
    strokeWeight(3);
    ellipse(x+50,y+7.5,9.5,9.5);
    stroke(150);
    strokeWeight(5);
};
weap.pick = function(x,y){
    noStroke();
    fill(163, 126, 5);
    rect(x+18.75,y,12.5,47.5);
    fill(79, 79, 79);
    rect(x+5,y-8,40,7.5);
    rect(x,y-5,50,10);
    rect(x,y+5,10,15);
    rect(x+40,y+5,10,15);
    

    fill(90);
    stroke(150);
    strokeWeight(5);
};
weap.sword = function(x,y){
    noStroke();
    fill(125, 125, 125);
    rect(x+25,y+5,10,30);
    rect(x+27.5,y-5,5,10);
    fill(0);
    rect(x+22.25,y+35,15,5);
    rect(x+21.25,y+40,17.5,5);
    rect(x+26.25,y+45,7.5,15);
    fill(60);
    rect(x+25,y+5,3,30);
    rect(x+27.5,y-5,2,10);
    stroke(150);
    strokeWeight(5);

};
var need = [100,80,60,40,20];
var mp = false;
//bases variables
var scene = 0;
//gamestuff
var playerX = 100;
var playerY = 300;
var rarities = [
100,1000,1001,1002,1003,
95, 100, 1000,1001,1002,
95, 99,  100, 1000,1001,
90, 95,100, 1000,1001,
90, 95,  100, 1000,1001,
85, 92.5,100, 1000,1001,
85, 92.5,97.5,100, 1000,
80, 90,  95,  97.5,100 ,
75, 87.5,92.5,95,  100 ,
60, 70,  75,  85,  100 ,
60, 70,  75,  85,  100
];
var FTNH = 0;
var FX = 0;
var FY = 0;
var PFX = 0;
var PFY = 0;
var selfMove = true;
var mr = false;
var back = color(94, 93, 92);
var craftable;
    //rev
    var revenant = function(x,y,hp,dmg,spd,id){this.id = id; this.x = x;this.y = y; this.hp = hp; this.mhp = hp; this.dmg = dmg; this.spd = spd;this.jump = 0;this.gravity = true;
    if(this.id === 2){this.hp *= 2; this.mhp *= 2;}
    };
    revenant.prototype.do = function(){
        if(plr.x > this.x){this.x+=this.spd;}
        if(plr.x < this.x){this.x-=this.spd;}
        if(plr.y > this.y){this.y+=this.spd;}
        if(plr.y + 4 < this.y&&this.gravity === false){this.jump = 90*this.spd;}
        this.y -= constrain(this.jump/10,-10,60);
        if(this.gravity){this.jump -= 1;}
        if(mr||keys[101]&&FTNH<=0){if(dist(mouseX,mouseY,this.x,this.y) <= 22.5){this.hp--;FTNH = 9;if(equipped === 1){this.hp -= 2;ihp-=1;hotbar[eqIn][1]-=1;if(ihp<=0){yellow = 180; ihp = null; equipped = null;hotbar[eqIn] = [null,null];}}}}
        if(this.hp <= 0){this.spd = 0;this.jump = 0;this.x = -400; this.y = -400;}
        if(dist(this.x,this.y,plr.x,plr.y)<=40&&plr.hp >= 25){plr.hp-=this.dmg;backRed = (this.id + 1)*45;}
        this.gravity = true;
    };
    revenant.prototype.display = function(){
        if(this.id === 1){
            stroke(255,255,255,75);
            fill(227, 227, 227);
            ellipse(this.x,this.y,30,30);
            fill(189, 0, 0);
            ellipse(this.x,this.y,this.hp*50/this.mhp, this.hp*50/this.mhp);}else{
            stroke(255,255,255,75);
            fill(0, 255, 102);
            ellipse(this.x,this.y,30,30);
            fill(0, 0, 189);
            ellipse(this.x,this.y,this.hp*50/this.mhp, this.hp*50/this.mhp);
            }

    };
var revsOnDisp = [];


var stone = function(x,y,id){
    this.x = x;
    this.y = y;
    this.id = id;
    if(this.id <= rarities[FY * 5]){
        this.hp = 3+FY;
        this.mhp = 3+FY;
    }else if(this.id <= rarities[FY * 5 + 1]){
        this.hp = 5+FY;
        this.mhp = 5+FY;
    }else if(this.id <= rarities[FY * 5 + 2]){
        this.hp = 7+FY/2;
        this.mhp = 7+FY/2;
    }else if(this.id <= rarities[FY * 5 + 3]){
        this.hp = 10 + FY/3;
        this.mhp = 10+ FY/3;
    }else{
        this.hp = 15 + FY/3;
        this.mhp = 15 + FY/3;
    }
    if(random(0,1000)<= FY*FY&&diff>1){this.hp = 250; this.mhp = 1; this.id = -100;}
};
stone.prototype.display = function(){
    var p = constrain(this.hp/this.mhp,0.25,1);
    if(this.death >= 22 - FY){
        this.x = -400;
        this.y = -400;
    }
    this.i = 0;
    if(this.id <= rarities[FY * 5]&&this.ldam === false){
        stroke(122, 121, 122);
        fill(140, 138, 138);
    }else if(this.id <= rarities[FY * 5 + 1]&&this.ldam === false){
        stroke(194, 186, 194);
        fill(242, 242, 242);
        this.i = 1;
    }else if(this.id <= rarities[FY * 5 + 2]&&this.ldam === false){
        stroke(191, 182, 7);
        fill(255, 242, 0);
        this.i = 2;
    }else if(this.id <= rarities[FY * 5 + 3]&&this.ldam === false){
        stroke(7, 147, 189);
        fill(0, 234, 255);
        this.i = 3;
    }else if(this.ldam === false && this.id !== -100){
        stroke(7, 189, 44);
        fill(13, 255, 0);
        this.i =4;
    }else if(this.hp > 200){
        fill(0);
        stroke(0);
    }
    if(this.ldam){this.bdam=true;}
    if(this.id <= rarities[FY * 5]&&this.bdam){
        stroke(186, 28, 0);
        fill(128, 26, 0);
    }else if(this.id <= rarities[FY * 5 + 1]&&this.bdam){
        stroke(251, 123, 0);
        fill(255, 67, 0);
        this.i = 1;
    }else if(this.id <= rarities[FY * 5 + 2]&&this.bdam){
        stroke(255, 117, 75);
        fill(219, 119, 75);
        this.i = 2;
    }else if(this.id <= rarities[FY * 5 + 3]&&this.bdam){
        stroke(255, 155, 127);
        fill(255, 105, 101);
        this.i = 3;
    }else if(this.bdam && this.id !== -100){
        stroke(255, 205, 118);
        fill(183, 123, 0);
        this.i =4;
    }else if(this.bdam && this.hp > 200){
        fill(100,0,0);
        stroke(120,0,0);
    }
    
    for(var d = 0; d < revsOnDisp.length; d++){
    if(revsOnDisp[d].x + 20 >= this.x+(1-p)*25 && revsOnDisp[d].x + 20 <= this.x+(1-p)*25 + 10*p && revsOnDisp[d].y + 16 >= this.y+(1-p)*25 && revsOnDisp[d].y - 16 <=this.y+(1-p)*25+50*p){revsOnDisp[d].x = this.x+(1-p)*25 - 20;}else{    if(revsOnDisp[d].y + 20 >= this.y+(1-p)*25 && revsOnDisp[d].y + 20 <= this.y+(1-p)*25+10*p&&revsOnDisp[d].x + 16 >= this.x+(1-p)*25 && revsOnDisp[d].x - 16 <= this.x+(1-p)*25+50*p){revsOnDisp[d].gravity = false;revsOnDisp[d].jump = 0;revsOnDisp[d].y = this.y+(1-p)*25-20;}
    if(revsOnDisp[d].y - 20 >= this.y+(1-p)*25 + 40*p && revsOnDisp[d].y - 20 <= this.y+(1-p)*25+50*p&&revsOnDisp[d].x + 16 >= this.x+(1-p)*25 && revsOnDisp[d].x - 16 <= this.x+(1-p)*25 + 50*p){revsOnDisp[d].y = this.y+(1-p)*25+50*p+20;revsOnDisp[d].jump = -1;}}

    if(revsOnDisp[d].x - 20 >= this.x+(1-p)*25+40*p && revsOnDisp[d].x - 20 <= this.x+(1-p)*25+50*p && revsOnDisp[d].y + 16 >= this.y+(1-p)*25 && revsOnDisp[d].y - 16 <=this.y+(1-p)*25+50*p){revsOnDisp[d].x = this.x+(1-p)*25+50*p+20;}else{    if(revsOnDisp[d].y + 20 >= this.y+(1-p)*25 && revsOnDisp[d].y + 20 <= this.y+(1-p)*25 + 10*p&&revsOnDisp[d].x + 16 >= this.x+(1-p)*25 && revsOnDisp[d].x - 16 <= this.x+(1-p)*25 + 50*p){revsOnDisp[d].gravity = false;revsOnDisp[d].jump = 0;revsOnDisp[d].y = this.y+(1-p)*25 - 20;}
    if(revsOnDisp[d].y - 20 >= this.y+(1-p)*25+40*p && revsOnDisp[d].y - 20 <= this.y+(1-p)*25+50*p&&revsOnDisp[d].x + 16 >= this.x+(1-p)*25 && revsOnDisp[d].x - 16 <= this.x+(1-p)*25 + 50*p){revsOnDisp[d].y = this.y+(1-p)*25+50*p+20;revsOnDisp[d].jump = -1;}
        }
    }
    
    
    if(plr.x + 20 >= this.x+(1-p)*25 && plr.x + 20 <= this.x+(1-p)*25 + 10*p && plr.y + 16 >= this.y+(1-p)*25 && plr.y - 16 <=this.y+(1-p)*25+50*p){plr.x = this.x+(1-p)*25 - 20;}else{    if(plr.y + 20 >= this.y+(1-p)*25 && plr.y + 20 <= this.y+(1-p)*25+10*p&&plr.x + 16 >= this.x+(1-p)*25 && plr.x - 16 <= this.x+(1-p)*25+50*p){plr.gravity = false;plr.jump = 0;plr.y = this.y+(1-p)*25-20;if(plr.corrosive){this.hp = 0;}}
    if(plr.y - 20 >= this.y+(1-p)*25 + 40*p && plr.y - 20 <= this.y+(1-p)*25+50*p&&plr.x + 16 >= this.x+(1-p)*25 && plr.x - 16 <= this.x+(1-p)*25 + 50*p){plr.y = this.y+(1-p)*25+50*p+20;plr.jump = -1;if(plr.corrosive){this.hp = 0;}}}

    if(plr.x - 20 >= this.x+(1-p)*25+40*p && plr.x - 20 <= this.x+(1-p)*25+50*p && plr.y + 16 >= this.y+(1-p)*25 && plr.y - 16 <=this.y+(1-p)*25+50*p){plr.x = this.x+(1-p)*25+50*p+20;}else{    if(plr.y + 20 >= this.y+(1-p)*25 && plr.y + 20 <= this.y+(1-p)*25 + 10*p&&plr.x + 16 >= this.x+(1-p)*25 && plr.x - 16 <= this.x+(1-p)*25 + 50*p){plr.gravity = false;plr.jump = 0;plr.y = this.y+(1-p)*25 - 20;if(plr.corrosive){this.hp = 0;}}
    if(plr.y - 20 >= this.y+(1-p)*25+40*p && plr.y - 20 <= this.y+(1-p)*25+50*p&&plr.x + 16 >= this.x+(1-p)*25 && plr.x - 16 <= this.x+(1-p)*25 + 50*p){plr.y = this.y+(1-p)*25+50*p+20;plr.jump = -1;if(plr.corrosive){this.hp = 0;}}
}
    
  

    if(mouseX > this.x && mouseX < this.x + 50 && mouseY > this.y && mouseY < this.y + 50 && dist(plr.x,plr.y,this.x+25,this.y+25)<= 200||this.ldam){
        if(mr||keys[101] && FTNH <= 0 && equipped === 0||equipped=== 4 && keys[101]&&ihp > 0||this.ldam||this.mdam){
            if(equipped === 4){hotbar[eqIn][1] --; ihp --;if(ihp <= 0){yellow = 180; equipped = null;hotbar[eqIn] = [null,null];}}
            if(this.ldam === false){this.hp -= 1; if(this.id === -100){plr.hp -= 0.5;backRed += 120; backRed = constrain(backRed,0,255);} }else{this.hp-=this.mhp/25-0.1; if(this.id === -100){plr.hp -= 0.001;}}
            if(this.hp <= 0&&greedy===false){
                var ides = this.i + 1;
                            if(ides === 1){
                                backpack.s ++;
                            }else if(ides === 2){
                               backpack.i ++;
                               worth += 1;
                          }else if(ides === 3){
                               backpack.g ++;
                               worth += 3;
                         }else if(ides === 4){
                               backpack.d ++;
                               worth += 9;
                        }else if(ides === 5){
                               backpack.la ++;
                               worth += 27;
                         }else{
                             plr.hp -= 50;
                         }
}else if(greedy&&this.hp<=0){yellow = 120;}
        }
	if(keys[101]&&FTNH<=0){FTNH = 6;}
    }
    if(random(0,2500) <= 1 && lingered && diff === 5){this.hp = 0;}
    strokeWeight(3);
    
    if(this.hp > 200){
        fill(0,0,0,255);
        stroke(100,100,100,255);
    }
    rect(this.x+(1-p)*25,this.y+(1-p)*25,50*p,50*p,2);
    this.ldam = false;this.mdam = false;
};
var field = [new stone(0,550,1)];

//generate field and field types
var rooms = [];
//each room has 2-3 entrances/exits

//0011 (left, down, for enterance)
rooms[0] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,0,1,1,1,1,1,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 0,0,0,0,0,0,0,0,0,0,0,1,
 0,0,0,0,0,0,0,0,0,0,0,1,
 1,0,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
];
rooms[1] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,0,1,1,1,1,1,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 0,0,0,0,0,0,0,0,0,1,1,1,
 0,0,0,0,0,0,0,0,0,1,1,1,
 1,0,0,0,0,0,0,0,0,1,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,1,1,1,1,1,1,1,
 1,1,1,0,0,0,0,1,1,1,1,1,
];
rooms[2] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,0,1,1,1,1,1,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 0,0,0,0,0,0,0,0,0,1,1,1,
 0,0,0,0,0,0,0,0,0,1,1,1,
 1,0,0,0,0,0,0,0,0,1,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
];
rooms[3] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,0,0,1,1,
 1,1,1,1,1,1,1,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,0,1,
 1,1,0,0,0,0,0,0,0,0,0,1,
 0,0,0,0,0,0,0,0,0,0,0,1,
 0,0,0,0,0,0,0,0,0,0,0,1,
 1,0,0,0,0,0,0,0,0,0,1,1,
 1,0,0,0,0,0,0,0,0,0,1,1,
 1,0,1,0,0,0,0,0,0,1,1,1,
 1,0,0,0,0,0,0,0,1,1,1,1,
 1,0,0,1,0,0,0,1,1,1,1,1,
];
rooms[4] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,0,0,0,0,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
//1010 (up, down)
rooms[5] = [
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
];
rooms[6] = [
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,1,1,1,1,1,1,1,1,
 1,1,0,0,0,0,0,0,1,1,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,1,1,1,1,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
];
rooms[7] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[8] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,0,0,0,0,1,
 1,1,1,1,1,1,1,1,1,1,0,1,
 1,1,1,1,1,1,0,0,0,1,0,1,
 1,1,1,1,1,0,0,1,0,1,0,1,
 1,1,1,1,1,0,0,1,0,1,0,1,
 1,1,1,1,1,0,0,1,0,0,0,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[9] = [
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,0,0,0,0,0,0,0,0,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
 1,1,1,0,0,0,0,0,0,1,1,1,
];
//0101 (right,left)
rooms[10] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[11] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 1,1,1,1,0,0,0,0,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
 1,1,1,1,0,0,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[12] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,0,1,0,0,0,1,0,0,0,1,0,
 0,0,0,0,1,0,0,0,1,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[13] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,0,0,1,1,1,1,1,0,0,0,0,
 0,0,0,0,0,0,0,1,0,0,0,0,
 0,0,0,1,1,1,0,1,0,0,0,0,
 0,0,0,1,1,1,0,0,0,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[14] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,1,1,1,1,1,1,1,1,1,1,0,
 0,1,1,0,0,0,1,0,1,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,1,1,0,0,0,1,0,1,0,0,0,
 0,1,1,1,1,1,1,1,1,1,1,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
//1001 (up,left)
rooms[15] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[16] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,0,0,0,1,1,1,1,1,
 1,1,1,0,0,0,0,1,1,1,1,1,
 1,1,0,0,0,0,1,1,1,1,1,1,
 0,0,0,0,0,1,1,1,1,1,1,1,
 0,0,0,0,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[17] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,0,0,0,1,1,1,1,1,1,1,1,
 0,0,0,0,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[18] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,0,0,0,1,
 1,1,1,1,1,0,0,1,0,1,0,1,
 1,1,1,1,1,0,0,1,0,1,0,1,
 1,1,1,1,1,1,0,0,0,1,0,1,
 0,0,0,0,1,1,1,1,1,1,0,1,
 0,0,0,0,0,1,1,1,1,1,0,1,
 1,1,1,1,0,0,0,0,0,1,0,1,
 1,1,1,1,1,1,1,1,0,1,0,1,
 1,1,1,1,1,1,1,1,0,0,0,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[19] = [
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,0,1,1,1,1,1,1,
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,1,1,0,1,1,1,1,
 0,0,1,0,0,0,0,0,1,1,1,1,
 0,0,1,0,1,0,0,0,1,1,1,1,
 0,0,0,0,1,0,0,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
//0110 (right,down)
rooms[20] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[21] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,0,0,0,0,0,
 1,1,1,1,1,1,1,1,0,0,0,0,
 1,1,1,1,1,0,1,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[22] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,0,0,0,0,0,
 1,1,1,1,1,1,1,0,0,0,0,0,
 1,1,1,1,1,0,0,1,1,0,0,1,
 1,1,1,1,1,0,0,1,0,0,0,1,
 1,1,1,1,1,0,0,1,0,0,1,1,
 1,1,1,1,1,0,0,0,0,0,1,1,
 1,1,1,1,1,0,0,0,0,1,1,1,
];
rooms[23] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,0,0,0,0,0,
 1,1,1,1,1,1,0,0,0,0,0,0,
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[24] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,0,0,
 1,1,1,1,1,0,0,1,1,1,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
//1100 (up,right)
rooms[25] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[26] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,0,1,1,1,1,
 1,1,1,1,1,0,0,0,0,1,1,1,
 1,1,1,1,1,1,0,0,0,0,0,0,
 1,1,1,1,1,1,1,0,0,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[27] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,0,0,0,0,1,
 1,1,1,1,1,0,0,1,1,1,0,1,
 1,1,1,1,1,0,0,1,1,1,0,1,
 1,1,1,1,1,0,0,1,1,1,0,1,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[28] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,1,1,0,0,0,0,0,
 1,1,1,1,0,1,1,0,0,0,0,0,
 1,1,1,1,1,0,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[29] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,0,1,1,1,0,
 1,1,1,1,1,0,0,0,1,1,1,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
//trois
rooms[30] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[31] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[32] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
rooms[33] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[34] = [
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 0,0,0,0,0,0,0,0,0,0,0,0,
 0,0,0,0,0,0,0,0,0,0,0,0,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
 1,1,1,1,1,0,0,1,1,1,1,1,
];
rooms[35] = [
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
 1,1,1,1,1,1,1,1,1,1,1,1,
];
var freedirs = {};
freedirs.up = [5,6,7,8,9,15,16,17,18,19,25,26,27,28,29,31,32,33,34];
freedirs.right = [10,11,12,13,14,20,21,22,23,24,25,26,27,28,29,30,32,33,34];
freedirs.down = [0,1,2,3,4,5,6,7,8,9,20,21,22,23,24,30,31,33,34];
freedirs.left = [0,1,2,3,4,10,11,12,13,14,15,16,17,18,19,30,31,32,34];

//munsters

//lowestFreeCell: Lowest index of field that is null
var LFC = 1;
//destroyed blocks
var destroyed = [[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1]];
//ids
var ids = [[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1]];
//fieldtypes
var ft = [0,21,12,30,3,35,20,13,3,35,
         33,17,35,29,32,11,31,21,32,1,
         27,12,4,35,22,13,31,27,30,18,
         24,13,34,30,32,30,31,24,32,0,
         27,30,15,5,23,16,28,16,35,6,
         20,34,30,32,34,13,3,35,23,17,
         25,17,33,4 ,6 ,35,33,12,32,2,
         24,10,19,33,18,20,32,4,23,19,
         8 ,32,13,32,4 ,27,3,33,15,35,
         26,14,10,11,32,14,32,17,35,35];
/**for(var a2 = 1; a2 < 100; a2 ++){
    var y = false;
    var cor = [false,false,false,false];

    for(var i = 0; i < freedirs.up.length; i ++){
        if(freedirs.up[i] === ft[a2 - 10]){cor[0] = true;}
    }

    for( i = 0; i < freedirs.right.length; i ++){
        if(freedirs.right[i] === ft[a2 + 1]){cor[1] = true;}
    }
    for( i = 0; i < freedirs.down.length; i ++){
        if(freedirs.down[i] === ft[a2 + 10]){cor[2] = true;}

    }
    for( i = 0; i < freedirs.left.length; i ++){
        if(freedirs.left[i] === ft[a2 - 1]){cor[3] = true;}

    }  

    while(y === false){
        ft[a2] = round(random(0,35));
        var av = [false,false,false,false];

        y = true;
        for(var i2 = 0; i2 < freedirs.up.length; i2 ++){
                if(freedirs.up[i2] === ft[a2]){av[0] = true;}
       }
        for(var i2 = 0; i2 < freedirs.right.length; i2 ++){
                if(freedirs.right[i2] === ft[a2]){av[1] = true;}
       }
        for(var i2 = 0; i2 < freedirs.down.length; i2 ++){
                if(freedirs.down[i2] === ft[a2]){av[2] = true;}
       }
        for(var i2 = 0; i2 < freedirs.left.length; i2 ++){
                if(freedirs.left[i2] === ft[a2]){av[3] = true;}
       }
    //if(av[0] !== cor[2]){y = false;}
   // if(av[1] !== cor[3]){y = false;}
    //if(av[2] !== cor[0]){y = false;}
    //if(av[3] !== cor[1]){y = false;}
    }


}**/
for(var a1 = 0; a1 < ids.length;a1++){
    var b1 = 0;
    while(b1 < 144){
        var c = ids[a1];
        c[b1] = round(random(0,100));
        b1 ++;
    }
}
var convList = function(list){
    var e = 0;
    while(e<=144){
        var x = e % 12;
        var y = (e - x)/12;

        if(list[e] === 1){
            var i2 = ids[FX + (FY * 10)];
            var id2 = i2[e];
            field[e] = new stone(x*50,y*50,id2);
        }else{
            //too bad
            var i = ids[FX + (FY * 10)];
            var id = i[e];
            field[e] = new stone(-400,-400,i);
        }
        var g = 0;
        var dest = destroyed[FX + (FY * 10)];
        while(g <= dest.length){
            if(dest[g] === e){
                g = 1000;
                field[e].x = -400;
                field[e].y = -400;
            }
            g++;
        }
        e++;
    }
};
var specKeys = {};
convList(rooms[ft[FX + (FY * 10)]]);
var kp0 = false;
var strForMain = "They await you ...";
var kp = false;
draw = function() {
    kpN = false;
    kp0 = false;
    mouseReleased = function(){mp = false;};
    mouseClicked = function(){mp = true;};
    keyPressed = function(){keys[key.code] = true; kp = true;kp0 = true;kpN = true;  if(keyCode === 37 || keyCode === 38 || keyCode === 39 || keyCode === 40 || keyCode === SHIFT || keyCode === CONTROL){specKeys[keyCode]=true;kpN = true;}
};
    keyReleased = function(){keys[key.code] = false;
    if(keyCode === 37 || keyCode === 38 || keyCode === 39 || keyCode === 40 || keyCode === SHIFT || keyCode === CONTROL){specKeys[keyCode]=false;}
    };
    if(FX > 9){FX = 9;}
    if(FX < 0){FX = 0;}
    if(FY > 9){FY = 9;}
    if(FY < 0){FY = 0;}

    //readList

    mouseReleased = function(){
        mr = true;
    };
    //switch(scene). Wow, switch(case)????
    switch(scene){
        case -1:
        background(50);
        if(step<= 300){
            stroke(99, 71, 0);
            fill(149, 121, 0);
            strokeWeight(5);
            rect(0,400,600,30);
            rect(260,430,60,170);
            fill(0,155,0);
            stroke(0,100,0);
            ellipse(290,360,80,80);
        }else if(step <= 600){
            background(160);
            stroke(99, 71, 0);
            fill(149, 121, 0);
            strokeWeight(5);
            rect(0,400,600,30);
            rect(260,430,60,170);
            fill(0,155,0);
            stroke(0,100,0);
            ellipse(290,360,80,80);
            
            stroke(0,255,0,128);
            strokeWeight(120);
            line(290,360,700,700);
            stroke(255);
            strokeWeight(100);
            line(290,360,700,700);
            
            strokeWeight(1);
            fill(160,160,160,128);
            rect(0,0,600,600);
        }else if(step <= 900){
            fill(0,155,0);
            stroke(0,100,0);
            strokeWeight(5);
            ellipse(280,460,80,80);
            fill(255,255,255,200);
            noStroke();
            rect(250,50,20,150);
            rect(300,150,20,150);
            rect(275,250,15,150);
        }else{scene = 1;}
        if(mr){scene = 1;}
        step++;
        break;
    case 0:
            background(100, 100, 100);
            noStroke();
            
            fill(97, 45, 2);
            textAlign(CENTER, CENTER);
            textFont(createFont("monospace"),60);
            
            text("Cave Search",300,50);
            fill(255, 208, 0);
            text("Cave Search",305,55);
            fill(64, 64, 64);
            strokeWeight(5);
            stroke(0);
            rect(20,400,175,90,5);
            rect(20,300,175,90,5);
            rect(20,200,200,90,5);
            fill(255);
            text("Play", 110,240);
            text("Mode",105,340);
            text("Guide",110,440);
            textSize(40);
            text(strForMain,310,550);
            if(mouseX>=20&&mouseX<=220&&mouseY>=200&&mouseY<=290&&scene===0&&mp){
                colStart = 255;
                sSLR = millis()+20000;
                step = 0;
                scene = 1;
                timeSinceBegin = millis();
            }
            if(mouseX>=20&&mouseX<=195&&mouseY>=300&&mouseY<=390&&scene===0&&mp){scene = 3;}
            if(mouseX>=20&&mouseX<=195&&mouseY>=400&&mouseY<=490&&scene===0&&mp){scene = 4;}
            if(diff >= 4){
                fill(255);
                stroke(255,0,0,128);
                strokeWeight(20);
            }else if(diff === 1){
                fill(0,155,0);
                stroke(0,100,0);
                strokeWeight(20);
            }else{
                fill(0);
                stroke(0,255,0,128);
                strokeWeight(20);
            }
            ellipse(480,350,200,200);
            stroke(0);
            strokeWeight(5);
            break;
        case 1:
            if(FX === -1){FX = 0;}
            background(93+backRed+yellow,93+yellow,93);
            //ladder and text
            if(FX === 0 && FY === 0){
                fill(56, 43, 3);
                stroke(0, 0, 0);
                rect(5,0,10,600);
                rect(35,0,10,600);
                var f = 20;
                while(f <= 600){
                    rect(0,f,49,5);
                    f += 20;   
                }
                rect(100,400,50,25);
                rect(120,425,10,250);
                if(mouseX >= 100 && mouseX <= 150 && mouseY >= 400 && mouseY <= 425){
                    rect(100,100,400,400);
                    fill(255, 255, 255);
                    textSize(20);
                    text("Greetings, miner. Your goal is to collect a rare, green material called Lazerite. We'd like you to collect 20. Amongst those, we would ask you to collect as many other ores as you can. We've left some items down at lower levels to reward you for your mining expeditions. You can come back here at any time, to be safe from ... them.",100,100,400,400);
                    
                }
            }

            //display the field
            if(plr.y >= 580){if(PFY < 9){plr.corrosive = true;FY += 1;plr.y = 10;}else{plr.y = 580;plr.gravity = false;}}
            if(plr.y <= 0){if(PFY >= 1){plr.corrosive = true;FY -= 1;plr.y = 520;}else{plr.y = 0;}}
            if(plr.x >= 580){if(PFX < 9){plr.corrosive = true;FX += 1;plr.x = 10;}else{plr.x = 580;}}
            if(plr.x <= 0){if(PFX >= 1){plr.corrosive = true;FX -= 1;plr.x = 580;}else{plr.x = 0;}}

            plr.gravity = true;
            
            for(var c = 0; c<revsOnDisp.length;c++){
                revsOnDisp[c].display();
            }

            
            for(var a = 0; a < field.length; a++){
                if(field[a] !== 0){
                    field[a].display();
                    if(field[a].hp <= 0||field[a].x === -400){
                        var lin = destroyed[FX+(FY*10)];
                        lin[lin.length] = a;

                        field[a] = 0;
                    }
                }
            }
            
            if(plr.y >= 580){if(PFY < 9){plr.corrosive = true;FY += 1;plr.y = 10;}else{plr.gravity = false;}}

            
            //find closest null to index 0
            for(var b = field.length; b >= 0; b --){
                if(field[b] === 0){
                    LFC = b;
                }
            }
            if(FX !== PFX || FY !== PFY){
                worth = 0;
                greedy = false;
                lingered = false;
                sSLR = millis()+20000;
                plr.corrosive = true;
                if(FX === 0 && FY === 0){
                    convList(rooms[0]);
                }else {
    
                    convList(rooms[ft[FX + (FY * 10)]]);
                }
                revsOnDisp = [];
                if(diff >= 3){
                    var lenZ = FY + round(random(-1,3));
                    for(var a3 = 0; a3 < lenZ; a3++){
                        var iDK = 1;
                        if(random(0,1) <= FY/10 && diff >= 4){iDK = 2;}else{iDK = 1;}
                        revsOnDisp[a3] = new revenant(round(random(0,600)),round(random(0,600)),constrain((lenZ * 4)-round(random(-5,5)),5,10),0.1,random(0.4,0.6),iDK);
                    }
                }
            }
            
            // revs and traitors
            
            for(var c = 0; c<revsOnDisp.length;c++){
                revsOnDisp[c].do();
            }
            
            if(millis()-sSLR >= 10000&&FY >= 5&&diff===5){lingered = true;}
            if(pS !== second() && lingered&&diff === 5){backRed = 180;plr.hp -= 5;}
            pS = second();
            if(worth >= 81&&FY>=6&&diff === 5){greedy = true;}
            //player
            
            if(equipped === 2 && keys[101]){
                var plrun = true;
                if(ihp <= 0){
                    if(backpack.la>= 10){backpack.la -= 10; ihp = 1200;hotbar[eqIn][1]=1200;}else{plrun = false;}
                }

                if(plrun){
                    ihp -= 1;hotbar[eqIn][1]--;

                    fill(255,255-((1200-ihp)/8),255-((1200-ihp)/8));
                    textSize(50);
                    text(ihp, 50,50);

                    noStroke();
                    fill(255, 0, 0,255);
                    ellipse(mouseX,mouseY,120,120);
                    fill(255, 0, 0,175);
                    ellipse(mouseX,mouseY,140,140);
                    fill(255, 0, 0,100);
                    ellipse(mouseX,mouseY,160,160);
                    fill(255, 0, 0,50);
                    ellipse(mouseX,mouseY,180,180);


                    stroke(255, 0, 0);
                    strokeWeight(20);
                    line(plr.x,plr.y,mouseX,mouseY);
                    stroke(255, 0, 0,175);
                    strokeWeight(30);
                    line(plr.x,plr.y,mouseX,mouseY);
                    stroke(255, 0, 0,100);
                    strokeWeight(40);
                    line(plr.x,plr.y,mouseX,mouseY);
                    stroke(255, 0, 0,50);
                    strokeWeight(50);
                    line(plr.x,plr.y,mouseX,mouseY);

                    strokeWeight(15);
                    stroke(0);
                    line(plr.x,plr.y,mouseX,mouseY);
                    fill(0);
                    ellipse(mouseX,mouseY,100,100);
                    stroke(0);
                    strokeWeight(5);
                    
                    
                    for(var c = 0; c < field.length;c++){
                        if(dist(mouseX,mouseY,field[c].x,field[c].y)<= 50){field[c].ldam = true;
}
                    }
                    backRed += 3.5;
                    backRed = constrain(backRed,0,175);
                    var plCaseTrue = true;
                    plr.lx = mouseX;
                    plr.ly = mouseY;
                    plr.scanX = mouseX;
                    plr.scanY = mouseY;
                    var plClosestPos = [mouseX,mouseY];
                    while(dist(plr.scanX,plr.scanY,plr.x,plr.y)<500){
                        var plSX = 1;
                        var plSY = plr.slope;
                        if(plr.slope === null){plSX = 0; plSY = 1;}
                        if(plSY>1){plSX = plSX/plSY;plSY = 1;}
                        for(var b = 0; b < revsOnDisp.length;b++){
                            if(dist(revsOnDisp[b].x,revsOnDisp[b].y,plr.scanX,plr.scanY)<= 90){revsOnDisp[b].hp-=1;}
                        }
                        if(dist(lazerian.x,lazerian.y,plr.scanX,plr.scanY)<=110&&LFX === FX && LFY === FY){if(lazerian.hp > 250 && winnable === false){lazerian.hp -= 1/10;}else if(winnable){lazerian.hp -= 0.3;}}
                        for(var a = 0; a < field.length; a++){
                            if(dist(field[a].x,field[a].y,plr.scanX,plr.scanY)<= 125){field[a].ldam = true; if(dist(plClosestPos[0],plClosestPos[1],plr.x,plr.y)>dist(field[a].x,field[a].y,plr.x,plr.y)){plClosestPos = [field[a].x,field[a].y];field[a].ldam=true;}}
                        }
                        plr.scanX += plSX;
                        plr.scanY += plSY;
                    }
                }
            }
            strokeWeight(5);
            stroke(0,100,0);
            fill(0,155,0);
                //wasd
            if(selfMove){
                if(keys[119]||specKeys[UP]){
                    if(plr.gravity === false){plr.jump = 45;}
                }
                if(keys[32]){
                    if(plr.gravity === false){plr.jump = 45;}
                }
                if(keys[97]||specKeys[LEFT]){plr.x -= 2;}
                if(keys[115]||specKeys[DOWN]){plr.y += 2;}
                if(keys[100]||specKeys[RIGHT]){plr.x += 2;}
            }
            
            if(keys[92]){scene = 6;}
            if(plr.gravity === true){plr.jump -= 1;}
            plr.y -= constrain(plr.jump/10,-10,60);
            plr.corrosive = false;

            
            
            ellipseMode(CENTER);
            ellipse(plr.x,plr.y,40,40);
            //back? front?
            if(yellow > 0){yellow --;}
            if(backRed > 0){backRed-=3;}
            if(diff >= 2){
                gS = constrain(((7-dist(FX,FY,LFX,LFY))*40)-backRed,0,150)/3;
            }else{gS = 0;}
            if(diff >= 2){
                if(LFX === FX && LFY === FY&&lazerian.hp>0){
                    var lPH = false;
                    var dS = 0;
                    var speed = 0.5;
                    if(lazerian.hp <= 250){speed = 1;}
                    
                    if(lazerian.lazTime >= 255){
                        if(lazerian.x>=plr.x){lazerian.x1 = plr.x;lazerian.x2 = lazerian.x;lazerian.y1 = plr.y; lazerian.y2 = lazerian.y;}else{lazerian.x2 = plr.x;lazerian.x1 = lazerian.x;lazerian.y2 = plr.y; lazerian.y1 = lazerian.y;}
                        lazerian.slope = -(lazerian.y2-lazerian.y1)/(lazerian.x2-lazerian.x1);
                        if(lazerian.x2 === lazerian.x1){lazerian.slope = null;}
        
                        var lCaseTrue = true;
                        lazerian.lx = plr.x;
                        lazerian.ly = plr.y;
                        lazerian.scanX = plr.x;
                        lazerian.scanY = plr.y;
                        var lClosestPos = [plr.x,plr.y];
                        while(dist(lazerian.scanX,lazerian.scanY,plr.x,plr.y)<100){
                            var lSX = 1;
                            var lSY = lazerian.slope;
                            if(lazerian.slope === null){lSX = 0; lSY = 1;}
                            if(lSY>1){lSX = lSX/lSY;lSY = 1;}
                            for(var a = 0; a < field.length; a++){
                                if(dist(field[a].x,field[a].y,lazerian.scanX,lazerian.scanY)<= 70){if(lazerian.lazTime >= 255){field[a].hp-=0.5;} if(dist(lClosestPos[0],lClosestPos[1],lazerian.x,lazerian.y)>dist(field[a].x,field[a].y,lazerian.x,lazerian.y)){lClosestPos = [field[a].x,field[a].y];dS = a;if(lazerian.lazTime >= 255){field[a].hp-=(speed)*1;}}}
                            }
                            lazerian.scanX += lSX;
                            lazerian.scanY += lSY;
                        }
                        lazerian.lx = lClosestPos[0]+25;lazerian.ly = lClosestPos[1]+25;
                        if(lClosestPos[1]=== plr.y){lazerian.lx = plr.x;lazerian.ly = plr.y;lPH = true;}
                    }
                if(lazerian.timeToLaz > 0){lazerian.timeToLaz --;lazerian.lazTime -= (255/40);lazerian.lazTime = constrain(lazerian.lazTime,0,455);}else{lazerian.lazTime+= 8;}
                if(lazerian.lazTime >= 455){lazerian.timeToLaz = 480;}
                if(lazerian.vulnerable){if(mr||keys[101]&&FTNH<=0){if(dist(mouseX,mouseY,lazerian.x,lazerian.y)<=220){FTNH = 9;if(winnable){if(equipped === 1){lazerian.hp -= 3;}else{lazerian.hp-=1;}}else if(lazerian.hp > 250){lazerian.hp -= 1/3;}}}}
                mOLM = millis();
                if(dist(plr.x,plr.y,lazerian.x,lazerian.y)<=60){plr.hp-=speed;backRed = 120*speed;}
                if(lazerian.x > plr.x){lazerian.x-=speed;}else if(lazerian.x < plr.x){lazerian.x+=speed;}
                if(lazerian.y > plr.y){lazerian.y-=speed;}else if(lazerian.y < plr.y){lazerian.y+=speed;}
    
                strokeWeight(20);fill(0,0,255,200);stroke(0,100,255,128);
                ellipse(lazerian.x,lazerian.y,190,190);
                if(speed === 0.5){
                   fill(0,255,0,lazerian.hp*0.510);stroke(0,255,0,lazerian.hp*0.2);
                   
                }else{fill(255,0,0,lazerian.hp*0.510);stroke(255,0,0,lazerian.hp*0.2);}
                arc(lazerian.x,lazerian.y,70,70,0,2*PI);
                if(speed === 0.5){
                    stroke(0,255,0,128);fill(constrain(lazerian.lazTime,0,255));
                    arc(lazerian.x,lazerian.y,200,200,0,(lazerian.hp-250)*1.44/(180/PI));
                    if(lazerian.lazTime >= 255){
                        strokeWeight(90);stroke(0,255,0,128);
                        line(lazerian.x,lazerian.y,lazerian.lx,lazerian.ly);
                        strokeWeight(70);stroke(0,255,0,200);
                        line(lazerian.x,lazerian.y,lazerian.lx,lazerian.ly);
                        strokeWeight(50);stroke(255);
                        line(lazerian.x,lazerian.y,lazerian.lx,lazerian.ly);
                        strokeWeight(20);stroke(0,255,0,0);
                        arc(lazerian.x,lazerian.y,200,200,0,(lazerian.hp-250)*1.44/(180/PI));
                        
                        strokeWeight(20);stroke(0,255,0,128);
                        if(lPH){plr.hp-=0.2;backRed = 90;}
                        if(lPH === false){field[dS].hp -= 1;}
    
                    }
    
                }else{stroke(255,0,0,128);fill(255-constrain(lazerian.lazTime,0,255));
                    arc(lazerian.x,lazerian.y,200,200,0,lazerian.hp*1.440/(180/PI));
                    if(lazerian.lazTime >= 255){
                        strokeWeight(90);stroke(255,0,0,128);
                        line(lazerian.x,lazerian.y,lazerian.lx,lazerian.ly);
                        strokeWeight(70);stroke(255,0,0,200);
                        line(lazerian.x,lazerian.y,lazerian.lx,lazerian.ly);
                        strokeWeight(50);stroke(0);
                        line(lazerian.x,lazerian.y,lazerian.lx,lazerian.ly);
                        strokeWeight(20);stroke(255,0,0,0);
                        arc(lazerian.x,lazerian.y,200,200,0,(lazerian.hp)*1.44/(180/PI));
                        strokeWeight(20);stroke(255,0,0,128);
                        if(lPH){backRed = 60;
                            plr.hp-=0.4;
                            var sped = (1000-dist(plr.x,plr.y,lazerian.x,lazerian.y))/100;
                            if(plr.x > lazerian.x){plr.x-=1;}
                            if(plr.x < lazerian.x){plr.x+=1;}
                            if(plr.y > lazerian.y){plr.y-=1;plr.gravity = true;plr.jump = 0;selfMove = false;}
                            if(plr.y < lazerian.y){plr.y+=1;}
                            selfMove = false;
                        }
                        if(lPH === false){field[dS].hp -= 2;}
                    }
    
                }
                strokeWeight(3);
                }else if(LFX === FX && LFY === FY){
                    strokeWeight(20);fill(0,0,255,200);stroke(0,100,255,128);
                    if(lazerian.dS<=0){stroke(0,255,0,128);fill(0,255,0,200);}
                    ellipse(lazerian.x,lazerian.y,abs(lazerian.dS),abs(lazerian.dS));
                    lazerian.dS -= 3 + abs(lazerian.dS)*0.1;
                    lazerian.dS = constrain(abs(lazerian.dS),-20,1000)*(lazerian.dS/abs(lazerian.dS));
                    strokeWeight(3);
                }else
                if(lazerian.hp > 0&&FY >= 4){if(millis() - mOLM >= 5000){
                        mOLM = millis();
                        lazerian.lazTime = 0;
                        lazerian.timeToLaz = 480;
                        if(LFX > FX){LFX --;lazerian.x = 900;}else if(LFX<FX){LFX ++;lazerian.x = -300;}
                        if(LFY > FY){LFY --;lazerian.y = 900;}else if(LFY<FY){LFY ++;lazerian.y = -300;}
                    }
                }
            }
            if(lazerian.hp > 250){fill(yellow+backRed,yellow+gS,0,FY*22);}else{fill(yellow+backRed+gS,yellow,0,FY*22);
}
            rect(0,0,width,height);
            noFill();
            strokeWeight(20);
            stroke(255,255,255,FY*11);
            strokeWeight(5);
            ellipse(plr.x,plr.y,70,70);
            selfMove = true;
            if(plr.hp < 100){plr.hp += 2/60;}
            if(keys[101]&&equipped === 3){plr.hp += 50; plr.hp = constrain(plr.hp,0,100);equipped = null; ihp = null;hotbar[eqIn] = [null,null];}
            //lazerian
            if(backpack.s >= need[0] && backpack.i >= need[1] && backpack.g >= need[2] && backpack.d >= need[3] && backpack.la >= need[4]){winnable = true;}
            
            //backpack
            if(keys[118]){
                stroke(140, 140, 140);
                fill(97, 96, 93);
                beginShape();
                vertex(0,0);
                vertex(375,0);
                vertex(375,100);
                vertex(50,100);
                vertex(0,0);
                endShape();
                beginShape();
                vertex(0,400);
                vertex(200,400);
                vertex(300,600);
                vertex(0,600);
                endShape();
                beginShape();
                vertex(375,103);
                vertex(375,180);
                vertex(140,180);
                vertex(100,103);
                endShape();
                fill(150,150,150,128);
                rect(160,107,60,60);
                pushMatrix();
                rotate(PI/4);
                fill(199, 199, 199);
                rect(207.5,-62.5,50,50);
                popMatrix();
                if(equipped === 0){weap.pick(165,120);}else if(equipped === 1){weap.sword(162,115);
                    fill(158, 3, 3);
                    rect(165,155,50,10);
                    fill(8, 150, 8);
                    rect(165,155,ihp/4,10);
                }else if(equipped === 2){weap.lazer(165,133);
                    fill(158, 3, 3);
                    rect(165,155,50,10);
                    fill(8, 150, 8);
                    rect(165,155,ihp/24,10);
                }else if(equipped === 3){weap.meds(170,120);} else if(equipped === 4){weap.jackhammer(171,115);
                    fill(158, 3, 3);
                    rect(165,155,50,10);
                    fill(8, 150, 8);
                    rect(165,155,ihp/20,10);}

                
                
                fill(117, 0, 0);
                quad(50,40,375,40,375,80,70,80);
                fill(0, 99, 0);
                var precH = plr.hp/100;
                quad(50,40,50+precH*325,40,constrain(50+precH*325,70,375),80,70,80);
                fill(97, 96, 93);
                rect(375,0,337.5,200);
                stroke(122, 121, 122);
                fill(140, 138, 138);
                rect(400,12.5,25,25);
                stroke(194, 186, 194);
                fill(242, 242, 242);
                rect(400,50,25,25);
                stroke(191, 182, 7);
                fill(255, 242, 0);
                rect(400,87.5,25,25);
                stroke(7, 147, 189);
                fill(0, 234, 255);
                rect(400,125,25,25);
                stroke(7, 189, 44);
                fill(13, 255, 0);
                rect(400,162.5,25,25);
                fill(255);
                textSize(30);
                text(" x " + backpack.s + " (" + round(backpack.s/need[0]*100)/1+"%)",500, 25);
                text(" x " + backpack.i+ " (" + round(backpack.i/need[1]*100)/1+"%)",500, 62.5);
                text(" x " + backpack.g+ " (" + round(backpack.g/need[2]*100)/1+"%)",500, 100);
                text(" x " + backpack.d+ " (" + round(backpack.d/need[3]*100)/1+"%)",500, 137.5);
                text(" x " + backpack.la+ " (" + round(backpack.la/need[4]*100)/1+"%)",500, 175);
                text("" + round(precH*100) + "%",225,58);
                text("Depth: " + FY, 150,20);
                textSize(15);
                fill(255,255,0);
                text("Mining Worth: " + worth,75,425);
                var possG = true;
                if(FY<6||diff!==5){possG = false;}
                if(possG === false){text("Cannot be marked Greedy.",105,450);}else{if(greedy){text("You are greedy.",85,450);}else{text("Not greedy.",75,450);}}
                fill(255, 0, 100);
                text("Time in room: " + (((millis() - sSLR)+20000)/1000), 85,475);
                var possL = true;
                if(FY<5||diff!==5){possL = false;text("Cannot be marked as Lingering.",130,500);}else{if(lingered){text("You have lingered.",85,500);}else{text("You haven't lingered.",90,500);}}
            }
            if(keys[98]){
                scene = 1.5;
            }
            if(colStart > 0){
                fill(0,0,0,colStart);
                rect(-5,-5,610,610);
                colStart-= colStart/500 + 0.2;
            }
            
            var h;
            if(keys[49]){eqIn = 0; h = hotbar[0]; equipped = h[0];ihp = h[1];}
            if(keys[50]){eqIn = 1; h = hotbar[1]; equipped = h[0];ihp = h[1];}
            if(keys[51]){eqIn = 2; h = hotbar[2]; equipped = h[0];ihp = h[1];}
            
            if(keys[52]){eqIn = 3; h = hotbar[3]; equipped = h[0];ihp = h[1];}
            if(keys[53]){eqIn = 4; h = hotbar[4]; equipped = h[0];ihp = h[1];}
            if(keys[54]){eqIn = 5; h = hotbar[5]; equipped = h[0];ihp = h[1];}

            
            if(winnable && lazerian.hp <= 0 && lazerian.dS <= -600||diff === 1 && winnable){timeAtEnd = millis();scene = 2;}
            if(plr.hp<=0){scene = 5;lingered = false;greedy = false;worth = 0;sSLR = millis()+20000;backpack = {s: 0, i: 0, g: 0, d: 0, la: 0};plr = {x: 0,y:300,hp:100,jump: 0,gravity: true,corrosive: false};FX = 0; FY = 0; PFX = 0; PFY = 0; destroyed = [[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1]];
//ids
 ids = [[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1]];/*for(var a2 = 1; a2 < 100; a2 ++){
    var y = false;
    var cor = [false,false,false,false];

    for(var i = 0; i < freedirs.up.length; i ++){
        if(freedirs.up[i] === ft[a2 - 10]){cor[0] = true;}
    }

    for( i = 0; i < freedirs.right.length; i ++){
        if(freedirs.right[i] === ft[a2 + 1]){cor[1] = true;}
    }
    for( i = 0; i < freedirs.down.length; i ++){
        if(freedirs.down[i] === ft[a2 + 10]){cor[2] = true;}

    }
    for( i = 0; i < freedirs.left.length; i ++){
        if(freedirs.left[i] === ft[a2 - 1]){cor[3] = true;}

    }  

    while(y === false){
        ft[a2] = round(random(0,35));
        var av = [false,false,false,false];

        y = true;
        for(var i2 = 0; i2 < freedirs.up.length; i2 ++){
                if(freedirs.up[i2] === ft[a2]){av[0] = true;}
       }
        for(var i2 = 0; i2 < freedirs.right.length; i2 ++){
                if(freedirs.right[i2] === ft[a2]){av[1] = true;}
       }
        for(var i2 = 0; i2 < freedirs.down.length; i2 ++){
                if(freedirs.down[i2] === ft[a2]){av[2] = true;}
       }
        for(var i2 = 0; i2 < freedirs.left.length; i2 ++){
                if(freedirs.left[i2] === ft[a2]){av[3] = true;}
       }
    //if(av[0] !== cor[2]){y = false;}
   // if(av[1] !== cor[3]){y = false;}
    //if(av[2] !== cor[0]){y = false;}
    //if(av[3] !== cor[1]){y = false;}
    }


}*/mr = false;mp = false;LFX = 6; LFY = 6; lazerian = {x: 300,y: 300,hp: 1000, vulnerable: true, dS: 190, lazTime: 0, timeToLaz: 480};winnable = false;revsOnDisp = [];hotbar = [[0,Infinity],[1,100],[4,150],[3,null],[null,null],[null,null]];

for(var a1 = 0; a1 < ids.length;a1++){
    var b1 = 0;
    while(b1 < 144){
        var c = ids[a1];
        c[b1] = round(random(0,100));
        b1 ++;
    }
}convList(rooms[0]);

}
        break;
        
        case 1.5:
            background(150);
            fill(200);
            stroke(100);
            strokeWeight(5);
            rect(400,0,200,100);
            rect(400,110,200,100);

            //items lol
            rect(120,350,75,75);
            rect(240,350,75,75);
            rect(360,350,75,75);
            
            rect(120,470,75,75);
            rect(240,470,75,75);
            rect(360,470,75,75);
            
            for(var n = 0; n<6; n++){
                
                var ix = (n%3)*120+120;
                var iy = ((n-(n%3))/3)*120+350;
                
                if(eqIn === n){noFill();stroke(255);strokeWeight(5);rect(ix,iy,75,75);}
                
                
                
                textSize(25);
                if(hotbar[n][1]!==Infinity && hotbar[n][1] !== null){
                    switch(hotbar[n][0]){
                        case 0:
                            fill(0);
                            break;
                        case 1:
                            fill((durbs[1]-hotbar[n][1])*(255/durbs[1]), 0, 0);
                            break;
                        case 2:
                            fill((durbs[2]-hotbar[n][1])*(255/durbs[2]), 0, 0);
                            break;
                        case 3:
                            fill(0);
                            break;
                        case 4:
                            fill((durbs[4]-hotbar[n][1])*(255/durbs[4]), 0, 0);
    
                    }
                    
                    text(round((hotbar[n][1]/+durbs[hotbar[n][0]])*100)+"%",ix+37,iy+85);
                }else if(hotbar[n][1]===Infinity){
                    textSize(15);
                    fill(0);
                    text("Unbreakable",ix+37,iy+85);
                }else{
                    textSize(25);
                    fill(0);
                    text("null",ix+37,iy+85);
                }
                switch(hotbar[n][0]){
                    case 0:
                        weap.pick(ix+13,iy+20);
                        break;
                    case 1:
                        weap.sword(ix+8,iy+10);
                        break;
                    case 2:
                        weap.lazer(ix+15,iy+30);
                        break;
                    case 3:
                        weap.meds(ix+18,iy+20);
                        break;
                    case 4:
                        weap.jackhammer(ix+18,iy+5);
                }
            }
            fill(0);
            textSize(20);
            text("Durabilities: \n\n                     Pickaxe: Inf,    Sword: 200\n                    LAZ rifle: 1200,    Medkit: None\n                    Jackhammer: 250",100,200); 
            textSize(50);
            text("Items",80,50);
            text("Return",500,50);
                if(mr&&mouseX>=400&&mouseY<=100){scene = 1;}
            text("Craft",500,160);
                if(mr&&mouseX>=400&&mouseY<=210&&mouseY>=110){scene = 1.6;}
            break;
        case 1.6:
            background(150);
            fill(200);
            stroke(100);
            strokeWeight(5);
            rect(400,0,200,100);
            rect(400,110,200,100);
            rect(-5,500,610,105);
                        //items lol
            rect(40,10,75,75);
            rect(160,10,75,75);
            rect(280,10,75,75);
            
            rect(40,130,75,75);
            rect(160,130,75,75);
            rect(280,130,75,75);
            
            for(var n = 0; n<6; n++){
                
                var ix = (n%3)*120+40;
                var iy = ((n-(n%3))/3)*120+10;
                

                
                
                textSize(20);
                fill(0);
                text("Slot " + (n+1), ix+37,iy+85); 
                
                switch(hotbar[n][0]){
                    case 0:
                        weap.pick(ix+13,iy+20);
                        break;
                    case 1:
                        weap.sword(ix+8,iy+10);
                        break;
                    case 2:
                        weap.lazer(ix+15,iy+30);
                        break;
                    case 3:
                        weap.meds(ix+18,iy+20);
                        break;
                    case 4:
                        weap.jackhammer(ix+18,iy+5);
                }
            }

            
            fill(0);
            textSize(50);
            text("Craft",300,550);
                if(mr&&mouseY>=500){scene = 1.61;
                }
            text("Items",500,160);
                if(mr&&mouseX>=400&&mouseY<=210&&mouseY>=110){scene = 1.5;}
            text("Return",500,50);
                if(mr&&mouseX>=400&&mouseY<=100){scene = 1.5;}
            break;
        case 1.61:
            background(150);
            fill(200);
            stroke(100);
            strokeWeight(5);
            rect(400,0,200,100);
            var backpack2 = [backpack.s,backpack.i,backpack.g,backpack.d,backpack.la];
            switch(craftPart){
                case 0: //type
                    craftable = [];
                    //tools craftable 
                        for(var a = 0; a < 5; a ++){
                            craftable[a] = liGrOrEqual(backpack2,craftNeeds[a]);
                        }

                    fill(0);
                    textSize(50);
                    
                    fill(200);
                    stroke(100);
                    strokeWeight(5);
                    if(craftable[0]){fill(200);}else{fill(150, 0, 0);}
                    rect(100,220,200,100);
                    if(craftable[1]){fill(200);}else{fill(150, 0, 0);}
                    rect(300,220,200,100);
                    if(craftable[2]){fill(200);}else{fill(150, 0, 0);}
                    rect(100,320,200,100);
                    if(craftable[3]){fill(200);}else{fill(150, 0, 0);}
                    rect(300,320,200,100);
                    if(craftable[4]){fill(200);}else{fill(150, 0, 0);}
                    rect(100,420,400,100);
                    
                    fill(0);
                    textSize(30);
                    text("Pickaxe (1)",200,240);
                    text("Sword (2)", 400, 240);
                    text("Medkit (4)", 400, 340);
                    text("Jackhammer (5)",300,440);

                    textSize(20);
                    text("LAZ rifle (3)",200,340);

                    text("Needs 10 stone.",200,280);
                    text("Needs 20 stone and 15 iron.",320,250,180,65);
                    text("Needs 3 lazerite.",400,380);
                    
                    textSize(15);
                    text("Needs 30 stone & iron, 20 gold, 5 diamonds, and 15 lazerite.",110,330,200,100);
                    text("Needs 25 stone, 10 iron, 5 gold, and 5 diamonds.",210,430,180,100);

                    if(craftType !== null){
                        fill(200);
                        stroke(100);
                        strokeWeight(5);
                        rect(-5,500,610,105);
                        
                        
                        
                        fill(0);
                        textSize(30);
                        var tool = "Pickaxe";
                        if(craftType === 1){tool = "Sword";}
                        if(craftType === 2){tool = "LAZ rifle";}
                        if(craftType === 3){tool = "Medkit";}
                        if(craftType === 4){tool = "Jackhammer";}
                        
                        text(tool + "?",430,80,140,100);
                        textSize(50);
                        text("Yes.",300,550);
                            if(mr&&mouseY>=500){craftPart = 1;}
                    }else{
                        fill(0);
                        textSize(30);
                        text("Select a tool!",10,250,100,150);
                    }
                    textSize(30);
                    fill(0);
                    text("Type a number from 1-5 that is craftable for a tool type. Craftable tools will be grey, otherwise red.",10,-20,400,250);
                    if(keys[49]&&craftable[0]){craftType = 0;}
                    if(keys[50]&&craftable[1]){craftType = 1;}
                    if(keys[51]&&craftable[2]){craftType = 2;}
                    if(keys[52]&&craftable[3]){craftType = 3;}
                    if(keys[53]&&craftable[4]){craftType = 4;}
                    break;
                case 1: // slot
                        fill(200);
                        stroke(100);
                        strokeWeight(5);
                        if(craftSlot === null){
                            fill(0);
                            text("Select a slot!",300,300);
                        }else{
                            rect(-5,500,610,105);
                            fill(0);
                            if(hotbar[craftSlot][0]!==null){textSize(20);text("WARNING: Slot " + (craftSlot+1) + " already contains an item. Crafting will delete this item! Are you sure you want to do this?",20,320,560,200);
                            }
                            textSize(50);
                            text("Yes.",300,550);
                                if(mr&&mouseY>=500){
                                    
                                    hotbar[craftSlot] = [craftType,durbs[craftType]];
                                    if(eqIn === craftSlot){
                                        equipped = craftType;
                                        ihp = durbs[craftType];
                                    }
                                    backpack2 = subList(backpack2,craftNeeds[craftType]);
                                    backpack = {s: backpack2[0],i: backpack2[1],g: backpack2[2],d: backpack2[3],la: backpack2[4]};
                                    craftPart = 0;
                                    craftSlot = null;
                                    craftType = null;
                                    scene = 1.5;
                                }
                            text("Slot " + (craftSlot+1) + "?",300,300);
                        }
                        fill(0);
                        textSize(30);
                        text("Choose slot 1-6 to craft item into with number keys.",10,-50,400,200);
                        if(keys[49]){craftSlot = 0;}
                        if(keys[50]){craftSlot = 1;}
                        if(keys[51]){craftSlot = 2;}
            
                        if(keys[52]){craftSlot = 3;}
                        if(keys[53]){craftSlot = 4;}
                        if(keys[54]){craftSlot = 5;}
                        break;

            }
            fill(200);
            stroke(100);
            strokeWeight(5);
            rect(400,0,200,100);
            textSize(50);
            fill(0);
            text("Cancel",500,50);
                if(mr&&mouseX>=400&&mouseY<=100){scene = 1.6;
                    craftPart = 0;
                    craftSlot = null;
                    craftType = null;
                }
            break;
        case 2:
            background(0);
            fill(200,200,200);
            strokeWeight(3);
            stroke(255,255,255);
            textSize(15);
            text("\t You've made it. You've gotten all the materials you needed for that strange, disgraceful conglomerate. What were they even going to use it for? What is this " + '"lazerite?"' + " What is it worth? Who even are these people? Why didn't they give you those 'items' they said you would get? What made these so-called " +'"traitors"' + " so rebellious against their work that they went for a life of near-solitude? You are to soon figure out who they are, and when you know, you will HATE them! Just as the traitors, the disgusting revenants, and the terrifying monsters beneath! You will rebel against them! \n \n \n \n \n \n                                                 Game 1/3.",50,100,500,500);
        text("Seconds since beginning: " + round((timeAtEnd-timeSinceBegin)/1000),300,425);
        textSize(38);
        fill(255, 255, 255);
        stroke(255,255,255,128);
        rect(200,450,200,100);
        fill(0,0,0);
        text("Main Menu", 300,510);
        if(mouseX >= 200 && mouseX <= 400 && mouseY >= 450 && mouseY <= 550&&mp){
            scene = 0;lingered = false;greedy = false;worth = 0;sSLR = millis()+20000;backpack = {s: 0, i: 0, g: 0, d: 0, la: 0};plr = {x: 0,y:300,hp:100,jump: 0,gravity: true,corrosive: false};FX = 0; FY = 0; PFX = 0; PFY = 0; destroyed = [[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1]];
//ids
 ids = [[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1],[-1,-1]];/*for(var a2 = 1; a2 < 100; a2 ++){
    var y = false;
    var cor = [false,false,false,false];

    for(var i = 0; i < freedirs.up.length; i ++){
        if(freedirs.up[i] === ft[a2 - 10]){cor[0] = true;}
    }

    for( i = 0; i < freedirs.right.length; i ++){
        if(freedirs.right[i] === ft[a2 + 1]){cor[1] = true;}
    }
    for( i = 0; i < freedirs.down.length; i ++){
        if(freedirs.down[i] === ft[a2 + 10]){cor[2] = true;}

    }
    for( i = 0; i < freedirs.left.length; i ++){
        if(freedirs.left[i] === ft[a2 - 1]){cor[3] = true;}

    }  

    while(y === false){
        ft[a2] = round(random(0,35));
        var av = [false,false,false,false];

        y = true;
        for(var i2 = 0; i2 < freedirs.up.length; i2 ++){
                if(freedirs.up[i2] === ft[a2]){av[0] = true;}
       }
        for(var i2 = 0; i2 < freedirs.right.length; i2 ++){
                if(freedirs.right[i2] === ft[a2]){av[1] = true;}
       }
        for(var i2 = 0; i2 < freedirs.down.length; i2 ++){
                if(freedirs.down[i2] === ft[a2]){av[2] = true;}
       }
        for(var i2 = 0; i2 < freedirs.left.length; i2 ++){
                if(freedirs.left[i2] === ft[a2]){av[3] = true;}
       }
    //if(av[0] !== cor[2]){y = false;}
   // if(av[1] !== cor[3]){y = false;}
    //if(av[2] !== cor[0]){y = false;}
    //if(av[3] !== cor[1]){y = false;}
    }


}*/mr = false;mp = false;LFX = 6; LFY = 6;lazerian = {x: 300,y: 300,hp: 1000, vulnerable: true, dS: 190, lazTime: 0, timeToLaz: 480};winnable = false;revsOnDisp = [];hotbar = [[0,Infinity],[1,100],[4,150],[3,null],[null,null],[null,null]];
timeSinceBegin = millis();
for(var a1 = 0; a1 < ids.length;a1++){
    var b1 = 0;
    while(b1 < 144){
        var c = ids[a1];
        c[b1] = round(random(0,100));
        b1 ++;
    }
}convList(rooms[0]);

}
        break;
        
        case 3:
            background(100);
            fill(50);
            rect(400,-10,220,120,5);
            rect(150,275,120,80,5);
            rect(310,275,120,80,5);
            
            fill(255);
            
            triangle(210,295,170,335,250,335);
            triangle(370,335,330,295,410,295);
            
            if(mr && mouseX >= 150 && mouseX <= 270 && mouseY >= 275 && mouseY <= 355){
                if(diff < 5){diff++;}
            }
            if(mr && mouseX >= 310 && mouseX <= 430 && mouseY >= 275 && mouseY <= 355){
                if(diff > 1){diff--;}
            }
            
            
            textSize(50);
            text("Back",500,50);
                if(mouseX>=400&&mouseY <= 210&&mp){scene = 0;}

            text("Difficulty: " + diff,300,200);
            
            textSize(20);
            text("(Difficulty changes which enemies spawn)",50,350,500,100);
            switch(diff){
                case 1:
                    text("Seriously? Nothing can kill you, but uhhh... skill issue.",50,450,500,100);
                    break;
                case 2:
                    text("Lazerian exists.",50,450,500,100);
                    break;
                case 3:
                    text("Revenants lurk in the shadows, and lazerian exists.",50,450,500,100);
                    break;
                case 4:
                    text("Revenants, traitors, and lazerian. Getting tough.",50,450,500,100);
                    break;
                case 5:
                    text("Greed steals your stuff, Linger hurts you for ... lingering, oh, and, revenants, traitors and lazerian. If you beat this, GG.",50,450,500,100);
                    break;
                    
            }
            break;
        case 4:
            background(100);
            
            fill(50); 
            rect(400,-10,220,120,5);

            fill(255);
            textSize(50);
            text("Guide", 100,50);
            text("Back",500,50);
                if(mouseX>=400&&mouseY <= 210&&mp){scene = 0;guidePart = 1;} else if (mp && guidePart < 3){guidePart ++;}

            switch(guidePart){
                case 1:
                    textSize(20);
                    text("1. Basics",100,150);
                    textSize(15);
                    text("WASD, SPACE, and arrow keys make you move. Press E to use a tool (excluding sword, you click). Use number keys 1-6 to select an item from your inventory. Press V for basic and general stats, but press B for backpack stats and crafting. To win this game, you must 1. get 100 stone, 80 iron, 60 gold, 40 diamonds, and 20 lazerite, then 2. kill the Lazerian if difficulty is 2 or higher. Press \u005C (backslash in text? how?!?! u005C) key to pause.",60,175,400,230);
                    break;
                case 2:
                    textSize(20);
                    text("2. Tools",100,150);
                    textSize(15);
                    text("Tools. 5 of them. First, the pickaxe. It has infinite durability, it deals 10 dps to one block, and does no extra damage to enemies. Second, the sword. It has 200 durability, one exhausted per hit. It cannot hurt blocks, and deals 2 extra damage to revenants and traitors. It deals 2 extra damage to the Lazerian when block goals (necessary materials referenced in part 1) are met, and none when not met. Third is the LAZ rifle. It holds 1200 durability, 1 lost on each frame of use (60 fps = 20 seconds runtime). It does not break when at 0 durability, but is rather recharged with 10 lazerite. It deals massive damage through its 'lazer' attack.  The medkit, fourth, heals you 50 hp once before breaking. Last, the jackhammer has 1000 durability and loses one on each hit to a block. It deals 1 damage every frame. (60 fps = 60 damage per second)",45,175,515,345);
                    break;
                case 3:
                    textSize(20);
                    text("3. The Lazerian",100,150);
                    textSize(15);
                    text("As discussed in 1, you must kill this beast to win the game. It has 500 health, one lost each click to it. it chases the player at 0.5 pixels per second in each cardinal direction if its hp > 250, else 1 pixel per second. It deals 1 damage if you are in the middle of it (more than just outer edge) when hp is > 250, doubling if not. Every ~ 10 seconds, it will fire a lazer. It destroys almost everything near you, and, if its scans show nothing between you and it within 150-ish pixels of you, hits you. 0.2 dps to you if it hits when it has > 250 hp, and 0.4 hp when not. Also, it can pull you toward it when its hp < 250 and the lazer hits you. It is highly recommended to hold onto some LAZ rifle charge to deal grand damage to it. There is nothing more in this guide. G o o d   l u c k. W e  w i l l   b e   e x p e c t i n g   y o u ,   o r   e l s e . . .",60,175,500,345);
                    break;
            }
            text("Click to continue ...",300,550);
            break;
        case 5:
            background(0);
            fill(200);
            stroke(100);
            rect(0,500,600,100);
            textSize(50);
            fill(255);
            text("Ouch...", 300, 50);
            fill(0);
            if(selfEnd){scene = 0;selfEnd = false;}
            text("Back to main menu?",300,550);
                if(mr && mouseY >= 500){scene = 0;}
            fill(0, 155, 0);
            stroke(0,100,0);
            strokeWeight(5);
            ellipse(300,300,240,240);
            fill(0);
            rect(0,270,600,60);
            fill(255);
            textSize(40);
            text("Fail...", 300, 300);
            break;
        case 6:
            background(0);
            fill(200);
            stroke(100);
            strokeWeight(5);
            rect(200,150,200,100);
            rect(200,450,200,100);
            
            fill(0);
            textSize(40);
            text("Return",300,200);
            text("End Run",300,500);
                if(mouseX >= 200 && mouseX <= 400 && mr){
                    if(mouseY >= 150 && mouseY <= 250){scene = 1;}
                    if(mouseY >= 450 && mouseY <= 550){scene = 1; plr.hp = -1000; selfEnd = true;}
                }
            fill(255);
            textSize(50);
            text("Paused",300,50);
            textSize(20);
            text("Time since run start: " + round((millis()-timeSinceBegin)/1000), 300,350);
    }
    
    
    FTNH--;
    PFX = FX;
    PFY = FY;
    mr = false;
    mp = false;
    if(scene !== 1){
        sSLR = millis()+20000;
    }
};
//here we go, 22nd century!!!
//2101 lines later . . .    
}};
  // Get the canvas that ProcessingJS will use
  var canvas = document.getElementById("mycanvas"); 
  // Pass the function to ProcessingJS constructor
  var processingInstance = new Processing(canvas, programCode); 
  </script>
</html>



