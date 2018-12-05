# wumpus
package game;

import java.util.Random;
import java.util.Scanner;

public class wumpus {

	// El mapa
	public static char[][] map = {{'*','*','*','*','*'},
								  {'*','*','*','*','*'},
								  {'*','*','*','*','*'},
								  {'*','*','*','*','*'},
								  {'*','*','*','*','*'}};
	
	// Variables de entrada del mapa
	public static int userInicioX;
	public static int userInicioY;
	
	// variables del disparo
	public static int disparoX;
	public static int disparoY;
	
	//Variables del usuario
	public static int userX;
	public static int userY;
	
	//Variables del oro
	public static int goldX;
	public static int goldY;
	
	// Variables del Wumpus
	public static int wumpusX;
	public static int wumpusY;
	
	// Variables del precipicio
	public static int precipicioX;
	public static int precipicioY;
	
	
	public static int points = 100;
	
	public static boolean estaJugando = true;
	public static boolean wumpusVivo = true;
	public static boolean yaDisparo = false;
	public static boolean recogeOro = false;
	public static boolean noCaiste = true;
	
	static Random rand = new Random();
	
	public static void main(String[] args) {
		
		// Configuraion de variables 
		userX = rand.nextInt(4-1);
		userY = rand.nextInt(4-1);
		
		userInicioX = userX;
		userInicioY = userY;
		
		goldX = rand.nextInt(5-1) + 1;
		goldY = rand.nextInt(5-1) + 1;
		
		wumpusX = rand.nextInt(5-1)+1;
		wumpusY = rand.nextInt(5-1)+1;

		// aquí ponemos la posicion del precipicio
		precipicioX = rand.nextInt(5-1)+1;
		precipicioY = rand.nextInt(5-1)+1;
		

		
		// Mostrando en consola las posiciones de los elementos del juego
		System.out.println("Gold Pos: "+goldX+"/"+goldY);
		System.out.println("Usr Pos: "+userX+"/"+userY);
		System.out.println("Wumpus Pos: "+wumpusX+"/"+wumpusY);
		System.out.println("Precipicio: "+precipicioX+"/"+precipicioY);
		
		
		map[userX][userY] = 'x';
		map[goldX][goldY] = 'g';
		map[wumpusX][wumpusY] = 'w';
		map[precipicioX][precipicioY] = 'a';
	
	
	
		
		//imprime instrucciones
		System.out.println("**************************************************\n"+
				"Estos son las acciones que puedes llevar a cabo:\n"+
				"Arriba: A \nAbajo: B \nIzquierda: I \nDerecha: D\n"+
				"Disparar Arriba: PA, Disparar Abajo: PB, Dispar izq: PI, Disparar Derecha: PD"
				+ "\nRecoger oro: O\n"+
				"**************************************************\n");
		
		// ciclo del juego
		while (points > 0 && estaJugando) { 
			   System.out.print("> "); 
			   Scanner scanner = new Scanner(System.in); 
			   String command = scanner.nextLine().toUpperCase(); 
			
			   // Verificar movimientos del usuario
			   if(command.equals("A")) {
				   System.out.println("mueve arriba");
				   
				   //Si el jugador intenta moverse fuera del área de juego debe sentir las paredes.
				   if(userX > 0 && userX <= 4) {
				
					   userX=userX-1;
				   }
				   else {
					   
				   }
			   }
			   else if(command.equals("B")) {
				   System.out.println("mueve abajo ");
				   if(userX >= 0 && userX < 4) {
					   userX=userX+1;
					   
					 
				   }
				   else {
					   System.out.println("Ya no puedes avanzar hacia abajo");
				   }
			   }
			   else if(command.equals("I")) {
				   System.out.println("mueve izquierda");
				   if(userY > 0 && userY <= 4) {
					   userY=userY-1;
					   
				   }
				   else {
					   System.out.println("Ya no puedes avanzar hacia izq");
				   }
			   }
			   else if(command.equals("D")) {
				   System.out.println("mueve derecha");
				   if(userY >= 0 && userY < 4) {
					   userY=userY+1;
				   }
				   else {
					   System.out.println("Ya no puedes avanzar hacia derecha");
				   }
				   
			   }
			
			   else if(command.equals("O")) {
			   		System.out.println("Recoger oro");
			   		//Verificar si el usuario esta en la misma posision que el oro
			   		//True-> mensaje Recogiste el oro, regresa a la puerta
			   		//False-> no estas cerca del oro 
			   		if (map[userX][userY] == map[goldX][goldY]) {
						System.out.println("Recogiste el oro, vuelve a la entrada");
						recogeOro = true;
					}
			   		else {
			   			System.out.println("No puedes tomar el oro");
			   		}
			   }
			   
			   //Disparar una flecha en una de cuatro direcciones, solo puede hacerlo una vez
			   else if(command.equals("PA")) {
				   if (!yaDisparo)  {
						System.out.println("Disparaste hacia arriba");
						disparoX = userX - 1;
						disparoY = userY;
						yaDisparo = true;
					}
					else {
						System.out.println("Ya no tienes flechas");
					}
			   }
			   else if(command.equals("PB")) {
				   if (!yaDisparo)  {
						System.out.println("Disparaste hacia abajo");
						disparoX = userX + 1;
						disparoY = userY;
						yaDisparo = true;
					}
					else {
						System.out.println("Ya no tienes flechas");
					}
			   }
			   else if(command.equals("PI")) {
				   if (!yaDisparo)  {
						System.out.println("Disparaste hacia izquierda");
						disparoX = userX;
						disparoY = userY - 1;
						yaDisparo = true;
					}
					else {
						System.out.println("Ya no tienes flechas");
					}
			   }
			   else if(command.equals("PD")) {
				   if (!yaDisparo)  {
						System.out.println("Disparaste hacia derecha");
						disparoX = userX;
						disparoY = userY + 1;
						yaDisparo = true;
					}
					else {
						System.out.println("Ya no tienes flechas");
					}
				   System.out.println("Disparo Pos: "+disparoX+"/"+disparoY);
			   }   
			
			   else {
			   		System.out.println("Opción invalida");
			   }
			    
				
				System.out.println("Usr Pos: "+userX+"/"+userY);
				System.out.println("Wum Pos: "+wumpusX+"/"+wumpusY);
				
				//Si el oro se encuentra en la misma área que el jugador debe poder ver un brillo vago
				if (map[userX][userY] == map[goldX][goldY]) {
				   System.out.println("Brillo vago");
				}
				
				//gana 1000 si toma el oro y sale
				if (map[userX][userY] == map[userInicioX][userInicioY] && recogeOro == true) {
					points = points + 1000;
					estaJugando = false;
				}
				
			
				//Si hay un precipicio en una de las áreas próximas debe percibir una ráfaga de viento
				String cai = "caiste al precipicio";
				String cuid = "rafaga de viento";
				int presiX = userX;
				int presiY= userY;
				
				if (presiX == 4) {
					presiX = presiX-1;
				}
				if (presiY == 4) {
					presiY = presiY-1;
				}
				if (presiX == 0) {
					presiX = presiX+1;
				}
				if (presiY == 0) {
					presiY = presiY+1;
				}
				
				// Verificar la ubicacion del usuario y si puede olerlo
				if ((map[presiX+1][presiY] == map[precipicioX][precipicioY] || 
					map[presiX-1][presiY] == map[precipicioX][precipicioY] ||
					map[presiX][presiY+1] == map[precipicioX][precipicioY] || 
					map[presiX][presiY-1] == map[precipicioX][precipicioY]) && noCaiste == true)   {
						System.out.println(cuid);
				}
						if (map[presiX][presiY] == map[precipicioX][precipicioY] && noCaiste == true) {
							points = points - 1000;
							estaJugando = false;
							System.out.println("has muerto");
						
				}
				
				
				
				// Verificar la ubicacion del usuario y si puede olerlo
				//Si el wumpus se encuentra en una de las áreas próximas debe poder olerlo
				if (wumpusVivo) {
					//Si al disparar la flecha el jugador mata al wumpus debe poder escucharlo.
					if (map[wumpusX][wumpusY] == map[disparoX][disparoY] && wumpusVivo==true) {
						points = points + 500;
						System.out.println("EL wumpus ha muerto");
						wumpusVivo = false;
					}
					int posXtemp = userX;
					int posYtemp = userY;
					
					if (posXtemp == 4) {
						posXtemp = posXtemp-1;
					}
					if (posYtemp == 4) {
						posYtemp = posYtemp-1;
					}
					if (posXtemp == 0) {
						posXtemp = posXtemp+1;
					}
					if (posYtemp == 0) {
						posYtemp = posYtemp+1;
					}
					
					// Verificar la ubicacion del usuario y si puede olerlo
					if ((map[posXtemp+1][posYtemp] == map[wumpusX][wumpusY] || 
						map[posXtemp-1][posYtemp] == map[wumpusX][wumpusY] ||
						map[posXtemp][posYtemp+1] == map[wumpusX][wumpusY] || 
						map[posXtemp][posYtemp-1] == map[wumpusX][wumpusY]) && wumpusVivo==true)   {
							System.out.println("Huele a wumpus");
					}
					
					// Si cae junto al wumpus muere
					if (map[userX][userY] == map[wumpusX][wumpusY] && wumpusVivo==true) {
						points = points - 1000;
						estaJugando = false;
						System.out.println("El wumpus te ha matado");
					}
				}
				
				//pierde un punto por cada acción que realiza
				points--;
			  }
			// Fin del juego
			System.out.println("Game Over x_x");
			System.out.println("Score: "+ points+ " puntos.");
		
		
			String mess="";
			
			for (int i =0; i<=map.length-1; i++) {
				mess="";
				for (int j =0; j<=map[i].length-1; j++) {
					mess +=map[i][j];
				
				}
				System.out.println(mess);
		}
	}
}

	
