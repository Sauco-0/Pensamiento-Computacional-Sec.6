# Pensamiento-Computacional-Sec.6
Entrega de códigos

// VARIABLES
let colorRosado;
let tamañoCirculo = 40;
let circulos = [];

function setup() {

  // tamaño del canvas
  createCanvas(600, 600);

  // color del fondo
  colorRosado = color(255, 180, 220);

  // crear círculos automáticamente
  for (let numero = 0; numero < 20; numero++) {

    circulos.push({

      // posición random horizontal
      posicionX: random(width),

      // posición random vertical
      posicionY: random(height),

      // tamaño random del círculo
      tamañoCirculo: random(30, 70)
    });
  }
}

function draw() {

  // pintar fondo
  background(colorRosado);

  // el mouse cambia el grosor de las líneas
  let grosorLineas = map(mouseX, 0, width, 1, 10);

  strokeWeight(grosorLineas);

  // CONDICIONAL
  // si se hace click las líneas son blancas
  if (mouseIsPressed) {

    stroke(255);

  } else {

    // si no se hace click son negras
    stroke(0);
  }

  noFill();

  // dibujar todos los círculos
  for (let numero = 0; numero < circulos.length; numero++) {

    let circuloActual = circulos[numero];

    dibujarCirculo(
      circuloActual.posicionX,
      circuloActual.posicionY,
      circuloActual.tamañoCirculo
    );
  }

  // segundo condicional
  // si el mouse pasa la mitad cambia el color
  if (mouseX > width / 2) {

    fill(255);

  } else {

    fill(255, 100, 180);
  }

  noStroke();

  // círculo que sigue el mouse
  ellipse(mouseX, mouseY, tamañoCirculo);

  // el mouse cambia el tamaño del círculo
  tamañoCirculo = map(mouseY, 0, height, 20, 100);
}


// FUNCIÓN PROPIA
function dibujarCirculo(posicionX, posicionY, tamañoCirculo) {

  beginShape();

  // crear muchos puntos alrededor del círculo
  for (let angulo = 0; angulo < TWO_PI; angulo += 0.3) {

    // deformación random
    let radioIrregular = tamañoCirculo + random(-10, 10);

    // calcular posición horizontal
    let puntoX = posicionX + cos(angulo) * radioIrregular;

    // calcular posición vertical
    let puntoY = posicionY + sin(angulo) * radioIrregular;

    // crear punto curvo
    curveVertex(puntoX, puntoY);
  }

  // cerrar figura
  endShape(CLOSE);
}
