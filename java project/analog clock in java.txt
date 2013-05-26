import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import java.util.*;

public class Clock extends Frame implements MouseMotionListener{
int xmou=200; //set the center of circle
int ymou=200; //set the center of circle

double theta=-0.1047; //theta for second's hand
int x=xmou; //x position of Second's hand
int y=ymou; //y position of second's hand
int p,b; //perpendicular and base of Second's hand

int h; //hypotenous(heigth) of clock's hand


double the= -0.1047; //theta for creating outer circle

double thetamin=-0.1047;        //theta for minutes hand
int xm=xmou; //x position of minute's hand
int ym=ymou; //y position of minute's hand
int pmin,bmin; //perpendicular and base of Minute's hand


double thetah=-0.1047;         //theta for hour hand
int xh=xmou; //y position of hour's hand
int yh=ymou; //y position of hour's hand
int ph,bh; //perpendicular and base of hour's hand


double thetan=-0.0;          //theta for numbers of clock
int xn=xmou; //x position of Clock numbers
int yn=ymou; //y position of Clock numbers
int pn,bn; //perpendicular and base of clock numbers
int num=0; //for writing the numbers


//constructor

Clock(){
super();
setSize(500,500);
setBackground(Color.PINK);
setVisible(true);
addMouseMotionListener(this);
}


//method of implemented  mouse interface
public void mouseMoved(MouseEvent me){

}

public void mouseDragged(MouseEvent me){
xmou=me.getX(); //changing the clock position on mouse drag
ymou=me.getY(); //changing the clock position on mouse drag

}


//method to paint clock
public void paint(Graphics g){
      
           //for writing numbers in clock and outer circle

for(int p=0;p<60;p++){
  
        int xocir=xmou;      //x position of outer circle
     int yocir=ymou;      //y position of outer circle
     int pocir,bocir;     //perpendicular and base of outer circle

            pocir=  (int) (Math.sin(the) * (h+23));
            bocir=  (int) (Math.cos(the) * (h+23));
            xocir=xocir-pocir;
            yocir=yocir-bocir;
            the=the - 0.1047;

                 g.setColor(Color.BLUE);
         g.drawLine(xocir+5,yocir+5,xocir,yocir);
                g.setColor(Color.BLACK);
if(p%5==0 ){
num++;
if(num>12){
 num=1;
}

xn=xmou;
     yn=ymou;

if(thetan<=-6.28318531 ){
thetan=0.0;

}
thetan=thetan-0.523598776 ;
     pn=  (int) (Math.sin(thetan) * (h+10));
     bn=  (int) (Math.cos(thetan) * (h+10));
     xn=xn-pn;
     yn=yn-bn;
g.drawString(""+num,xn-3,yn+5);

   }      

     }
  
     //for drawing Clock hands

     g.setColor(Color.BLACK);
  
     g.drawLine(xmou,ymou,xm,ym); //drawing minute's hand
     g.drawLine(xmou,ymou,xh,yh); //drawing hour's hand
  
     g.setColor(Color.RED);
     g.drawLine(xmou,ymou,x,y); //drawing second's hand
      
    }


 public void newpoint(){

    Calendar now = Calendar.getInstance(); //creating a Calendar variable for getting current time

    //for second hand

    x=xmou;
    y=ymou;
    theta=-0.1047;
    theta=theta*now.get(Calendar.SECOND);
    p=  (int) (Math.sin(theta) * h);
    b=  (int) (Math.cos(theta) * h);
    x=x-p;
    y=y-b;
    //theta=theta - 0.1047;

  //for minutes hand

    xm=xmou;
    ym=ymou;

    thetamin=-0.1047;
    thetamin=thetamin*now.get(Calendar.MINUTE);
    pmin=  (int) (Math.sin(thetamin) * (h-6));
    bmin=  (int) (Math.cos(thetamin) * (h-6));
    xm=xm-pmin;
    ym=ym-bmin;

    //for hour's hand

    xh=xmou;
    yh=ymou;
    thetah=-0.1047;
    thetah=thetah*now.get(Calendar.HOUR)*5;


   if (now.get(Calendar.MINUTE)>=12 && now.get(Calendar.MINUTE)<24){
  thetah=thetah-0.1047;


   }
   else if(now.get(Calendar.MINUTE)>=24 && now.get(Calendar.MINUTE)<36){
  thetah=thetah-(2*0.1047);


   }
   else if(now.get(Calendar.MINUTE)>=36 && now.get(Calendar.MINUTE)<48){
  thetah=thetah-(3*0.1047);


   }
   else if(now.get(Calendar.MINUTE)>=48 && now.get(Calendar.MINUTE)<60){
  thetah=thetah-(4*0.1047);


   }


    ph=  (int) (Math.sin(thetah) * (h-15));
    bh=  (int) (Math.cos(thetah) * (h-15));
    xh=xh-ph;
    yh=yh-bh;




 }
  

   public static void main(String[] args) {
    
        Clock m=new Clock();
        m.h=60;
    
         while(true){
  
         m.newpoint();
         m.repaint();
         try{
     Thread.sleep(6);
     }catch(Exception e){
    
     }    
      }
    }

}