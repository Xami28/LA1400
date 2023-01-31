```java
package SamuelLucena;
import robocode.*;


public class Aimbot extends JuniorRobot
{
	double firePower;
	
	public void Modeshifter(){
	int checkPlayers = others;
		// Depending on Enemy amout, switch to different Actions.
		if ( checkPlayers > 15) { 
		dip(); // move away from Others.
	    }
		else if ( checkPlayers < 10) {
		warmachine();
		}
		else if (checkPlayers < 15) {
		good(); // Go around the Field casually.
	    }
		else if (checkPlayers == 0) {
		toosafe(); 	// Scanning speed is incresed to find Others.
		}
	}
	public void run() {
	
		setColors(black, blue, black, black, black);

		// Robot main loop
		while(true) {
		Modeshifter();
		}
	}
	public void onScannedRobot() {
		out.println(scannedDistance);
		out.println(scannedVelocity);
		turnGunTo(scannedAngle + scannedVelocity/2);
		if(scannedDistance < 100){
		   fire(3);
		   turnGunRight(360);	
		}
	}	
	public void onHitByBullet() {
		turnRight(90);
        ahead(fieldHeight / 2); // Move Height/Width of Field devided by Number in this case 2.
	}

	public void onHitWall() {
			// Move away from Wall in the Right Angle.
			 if (hitWallAngle != -1) {
           	turnRight(hitWallAngle);
           	back(fieldHeight / 4);
            turnRight(90);
		}
	}	
	
	public void dip() {
		int checkPlayers = others;
		turnRight (90); 
		ahead(fieldHeight / 4);
		turnRight (90);
		ahead (fieldHeight / 2);
		if (checkPlayers < 15);{
		good();
		}
	}

	public void warmachine () {
		if (scannedDistance > 0) {
           int angle = scannedBearing + heading - gunHeading;
           bearGunTo(angle);
           ahead(scannedDistance - 50);
           turnRight(scannedBearing);
		   fire (2);
         }
         else {
            turnGunRight(360);
            ahead(fieldHeight/2);
			fire (2);
        }
		 	good();
	}
	public void good() {
		ahead(fieldHeight / 8);
		turnLeft (90);
		back(fieldHeight / 8 - 20);
		turnRight(90);
	}
	public void toosafe() {
		ahead(fieldHeight / 4);
		turnGunRight (360);
	}
}
```
