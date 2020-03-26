# repository3
type
  ukaz=^TT;
  TT=record
    num:byte;
    next:ukaz;
  end;
  
procedure print(top:ukaz);
  forward;

procedure FormNumber(var top:ukaz);
  var
    p:ukaz;
    k,t:integer;
  begin
    k:=0;
    new(top);
    top^.num:=2;
    t:=2;
    repeat      
      if ((top^.num)*2+k) div 10 = 0
        then
          begin
            new(p);
            p^.next:=top;
            p^.num:=(top^.num)*2+k;
            t:=p^.num;
            top:=p;
            k:=0;
          end
        else
          begin
            new(p);
            p^.next:=top;
            p^.num:=((top^.num)*2+k) mod 10;
            t:=p^.num;
            top:=p;
            k:=1;
          end;
         print(top); 
    until (t=1) and (k=0);
  end;

procedure print(top:ukaz);
  var
    p:ukaz;
  begin
    write(top^.num);
    p:=top;
    repeat
      p:=p^.next;
      write(p^.num);
    until p^.next=nil;
    writeln;
  end;

var
  top:ukaz;
  
begin
  FormNumber(top);
  writeln('Искомое число:');
  print(top);
end.
