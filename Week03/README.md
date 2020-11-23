float set_color = 255;
int nTiles = 0;
int wid = 0;
float center = 100;
boolean toggle = true;

void setup() 
{
    size(800, 800);
    nTiles=width / 100;
    // set width
    noStroke();
}

void draw() 
{
    if ((wid==0) || (wid==width/2)) toggle=!toggle;
    if (toggle) wid--;  else wid++;
    //transformation for width
    float angle = map(wid,0,width/2,0,PI);
    // transformation for the orignial angle
    background(255);
    translate(center / 2,center / 2);
    for (int y = 0; y < nTiles; y++) {
        for (int x = 0; x < nTiles; x++) {
            pushMatrix();
            translate(center * x, center * y);
            scale(center / width*2);
            set_color = 255;
            float foo = map(x, 0, nTiles, width/10, 10) ;
            float bar = map(y, 0, nTiles, -PI, PI / 3);
            // locate every part
            circle(wid, foo, angle, bar); 
            popMatrix();
        }
    }
}

void circle(float radius, float rSub, float angle, float Add)
{
      //pushMatrix();
       float col = 168;
       float col2 = 45;
       int transp = 100;
       do {
          fill(set_color,col,col2,transp);
          ellipse(0, 0, radius, radius);
          radius -= rSub; // define the radius of the next small circle
          angle += Add;
          float r = rSub * 0.6;
          float x = cos(angle + Add) * r;
          float y = sin(angle + Add) * r;
          translate(x, y);
          // reset the center of the next small circle
          col-=10;
          col2+=10;
          transp+=15;
      } while(radius >= 0);
      //popMatrix();
  }
