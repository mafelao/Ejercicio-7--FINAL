# Ejercicio-7--FINAL
Visualización 3D. 


Table tabla;
PImage paper;
PFont anios;
String vars[]={"Artículos", "Libros", "Capítulos"};
//String axisX[]={"2004", "2005", "2006", "2007", "2008", "2009", "2010", "2011", "2012"};
PShape a, l, c;
void setup() {
  size (1000, 636, P3D);

  tabla = loadTable("Tablita.csv", "header");
  paper=loadImage("paper.png");
  anios=loadFont("Helvetica-15.vlw");

  //para saber cuantas filas hay en la tabla
  println(tabla.getRowCount() + " filas en total en la tabla");

  noStroke();
  a = createShape();
  l = createShape();
  c = createShape();

  a.beginShape();
  l.beginShape();
  c.beginShape();


  a.fill(102, 50, 80);
  l.fill(80, 100, 30);
  c.fill(255, 255, 50);

  a.vertex(100, 400);
  l.vertex(100, 400);
  c.vertex(100, 400);

  for (TableRow row : tabla.rows()) {

    int id= row.getInt("id");

    float anio = row.getFloat("anio");
    float articulo=row.getFloat("articulos");
    float libro=row.getFloat("libros");
    float capitulo=row.getFloat("capitulos de libro");
    String years = row.getString("anio");


    a.vertex(id*100+200, 400-(articulo)/20);
    l.vertex(id*100+200, 400-(libro)/20);
    c.vertex(id*100+200, 400-(capitulo)/20);
  }
  a.vertex(1000+200, 400);
  l.vertex(1000+200, 400);
  c.vertex(1000+200, 400);
  a.endShape();
  l.endShape();
  c.endShape();
}

void draw() {
  background(paper);
  //image(paper, 0, 0);
  textFont(anios, 16);
  fill(0);
  text("Producción por tipo (producción bibliográfica), 2004 - 2013", 50, 40);
  textFont(anios, 10);
  text("Fuente: Colciencias - Plataforma ScienTI - Colombia, enero 15 de 2014, 2004 - 2013.", 590, 600);
  textFont(anios, 12);
  text("*Información registrada para la Convocatoria 640-2013 para el reconocimiento y medición", 50, 70); 
  text("de grupos de investigación, desarrollo tecnológico y/o innovación y para el reconocimiento", 50, 85); 
  text("de investigadores del sistema nacional de ciencia, tecnología e innovación, año 2013.", 50, 100);

  pushMatrix();

  camera(mouseX, -mouseY*2, (height/2) / tan(PI/6), width/2, height/2, 0, 0, 1, 0);
  println(mouseX + ","+ mouseY);


  //TEXTO
  pushMatrix();
  translate(40, 0, 0);
  //rotateZ(PI/4);
  //rotateX(PI/4);
  textFont(anios, 15);
  fill(0);
  text(vars[0], 0, 400);
  popMatrix();

  pushMatrix();
  translate(40, 0, 100);
  //rotateZ(PI/4);
  //rotateX(PI/4);
  textFont(anios, 15);
  fill(0);
  text(vars[1], 0, 400);
  popMatrix();

  pushMatrix();

  translate(40, 0, 200);
  //rotateZ(PI/4);
  //rotateX(PI/4);
  fill(0);
  textFont(anios, 15);
  fill(0);
  text(vars[2], 0, 400);

  for (TableRow row : tabla.rows()) {
    int id= row.getInt("id");
    String anio = row.getString("anio");
    fill(0);
    text(anio, id*100+200, 400, 50);
    ellipse(id*100+200, 450, 5, 5);
    stroke(0);
    line(id*100+330, 450, 120, 450);
  }
  popMatrix();

  //POLIGONOS
  pushMatrix();
  translate(40, 0, 0);
  shape(a, 0, 20);
  popMatrix();

  pushMatrix();
  translate(40, 0, 100);
  shape(l, 0, 20);
  popMatrix();

  pushMatrix();
  translate(40, 0, 200);
  shape(c, 0, 20);
  popMatrix();

  popMatrix();
}
