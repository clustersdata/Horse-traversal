# Horse-traversal

Horse traversal

在Ｎ＊Ｍ的棋盘中，马只能走日字。马从位置(x,y)处出发，把

	棋盘的每一格都走一次，且只走一次。找出所有路径。
  
【参考程序】 {深度优先搜索法}

const n=5;m=4;

fx:array[1..8,1..2]of -2..2=((1,2),(2,1),(2,-1),(1,-2),(-1,-2),(-2,-1),

			     (-2,1),(-1,2));  {八个方向增量}
           
           
var

  dep,i:byte; x,y:byte;
  
  cont:integer; 	       {统计总数}
  
  a:array[1..n,1..m]of byte;   {记录走法数组}
  
procedure output; {输出,并统计总数}

var x,y:byte;

begin

    cont:=cont+1;  writeln;
    
    writeln('count=',cont);
    
    for y:=1 to n do  begin
    
	for x:=1 to m do write(a[y,x]:3);  writeln;
  
  
    end;     {	readln; halt;}
    
end;

procedure find(y,x,dep:byte);

var i,xx,yy:integer;

begin

    for i:=1 to 8 do
    
       begin
       
       xx:=x+fx[i,1];yy:=y+fx[i,2];  {加上方向增量,形成新的坐标}
       
	if ((xx in [1..m])and(yy in [1..n]))and(a[yy,xx]=0) then
  
		      {判断新坐标是否出界,是否已走过?}
          
	  begin
    
	    a[yy,xx]:=dep;	       {走向新的坐标}
      
	    if (dep=n*m)   then output
      
			    else find(yy,xx,dep+1); {从新坐标出发,递归下一层}
          
	    a[yy,xx]:=0     {回溯,恢复未走标志}
      
	  end;
    
      end;
      
end;

begin

  cont:=0;
  
  fillchar(a,sizeof(a),0);
  
  dep:=1;
  
  writeln('input y,x');readln(y,x);
  
{ x:=1;y:=1;}

  if (y>n) or(x>m) then begin writeln('x,y error!');halt;end;
  
  a[y,x]:=1;
  
  find(y,x,2);
  

  if cont=0 then writeln('No answer!') else write('The End!');
  
  readln;
  
end.

