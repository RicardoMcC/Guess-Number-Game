# Guess-Number-Game
#By Ricardo McCauley 
Enter a number to see if your choice is correct.
Enter a number, and hit the "Guess Number" button.
If you enter a number, and it is wrong replace current number with anohther number.
Then hit the "Guess Number" button to enter guess. 
Each time you do not get the right number, there will be hints to help you.
The hint can be warmer, which means your guess is closer to the right answer than your previous guess.
Or the hint could be colder, which means your guess it farther away from the  current number.
Another hint will be indicating whether your going above or under the correct number.
By using saying number to high or low. 
Please king make sure to choose numbers 1-100 otherwise your aswer will not count. 


package guess;
import helpers.ExitButton;
import helpers.NumberUtilities;
import helpers.OutputUtilities;
import javafx.event.Event;

import javax.swing.JButton;
import javax.swing.JLabel;

import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.FocusEvent;
import java.awt.event.FocusListener;
import  java.awt.Color;

import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;



import java.awt.event.WindowEvent;
import java.util.Random;
/***********************************************************************
Program Name: GuessGame 
Programmer's Name: Ricardo McCauley 
Program Description:Guess the number
***********************************************************************/


public class GuessGame extends JFrame{
    int	GUESS_MAX = 100;
    int GUESS_MIN = 0;
	private JButton guessButton;
	private JButton newgameButton;
	private JLabel messageLabel;
	private JLabel guessLabel;
	private JLabel resultLabel;
	private JLabel guessattemptsLabel;
	private JLabel warmorcoldLabel;
	private JTextField userguess;
	int guessCount = 0;
   int numberToGuess = NumberUtilities.getRandomNumber(GUESS_MAX);
   
	public GuessGame() {

		createFrame();
		createTextFields();
		createButtons();
	

	}
		private void createTextFields()
		{
			 messageLabel = new JLabel("Guess a number 1-100 thats a whole number \n");
				guessLabel = new JLabel("\n enter your guess\n");
				resultLabel =new JLabel(" guess result");
				guessattemptsLabel= new JLabel("number of attempts: ");
				warmorcoldLabel= new JLabel(" ");
				 userguess = new JTextField(3);
				
			this.add( messageLabel);
			this.add(guessLabel);
			this.add( userguess);
			this.add(resultLabel);
			this.add(warmorcoldLabel);
			this.add(guessattemptsLabel);
	
		
		//	txtResult = new JTextField();
			//make the result field a read only field, user cannot edit
			//txtResult.setEditable(false);
		//	this.add(txtResult);
			
		}
		private void createButtons()
		{
		//	create the button objects and add to the container
			guessButton = new JButton("Guess number");
			this.add(guessButton);
						
			GuessButtonHandler  ghandler = new GuessButtonHandler();
			guessButton.addActionListener(ghandler);
			
			
			//create the button objects and add to the container
			newgameButton = new JButton("new game");
			this.add(newgameButton);
						
			NButtonHandler nhandler = new NButtonHandler();
			newgameButton.addActionListener( nhandler );
			
			//add the exit button from the helper files
			this.add(new ExitButton());	    
			
			FocusHandler fhanlder = new FocusHandler();
			 userguess.addFocusListener(fhanlder);
		
		}
		
		
		private void createFrame()
		{// try borderLayout(5,5);
			//set gridlayout with 4 rows and 2 columns
			this.setLayout(new FlowLayout());
			this.setTitle("A Simple Graphical User Interface");
		}
		
		class NButtonHandler implements ActionListener {
			public void actionPerformed(ActionEvent e ){
				
				    numberToGuess =(int) NumberUtilities.getRandomNumber(GUESS_MAX);
			 guessCount = 0;
				resultLabel.setText("Lets Play!!");
				warmorcoldLabel.setText("");
				userguess.setText("");
				guessattemptsLabel.setText(" guess attempts"+ guessCount);
			}
		}
		
		
		
		class FocusHandler implements FocusListener {
			public void focusGained(FocusEvent e ){
			 if (e.getSource()==  userguess){
				 userguess.setText("");
			 }
			
			 else if (e.getSource()==  userguess){
				 guessButton.requestFocus();
			 }
			}
	
			public void focusLost(FocusEvent e) {
				if(e.getSource()== userguess){
					guessButton.requestFocus();
				}
			
			}
	}
		class GuessButtonHandler implements ActionListener {
			int lastDistance =0;
		
		public void actionPerformed(ActionEvent event){
			
		
		
		 int guess = 0;
		boolean correct = false;
		int currentDistance = 0;
		String instring;

		
	
	    
		
		
		if (guessCount == 0){
		lastDistance = GUESS_MAX;
		}
	

		instring = userguess.getText();
		if (instring.equals("")){
			instring = ("0");
			userguess.setText("0");
		}
		guess = Integer.parseInt(instring);
		
		if(guess >= GUESS_MIN && guess <=GUESS_MAX){
			guessCount = guessCount+1;
		//	if (!correct) {
				currentDistance = Math.abs(guess- numberToGuess);
				if (currentDistance <= lastDistance){
					//Set alert to read 
				
					resultLabel.setForeground(Color.red);
					warmorcoldLabel.setText("getting warming");
					warmorcoldLabel.setForeground(Color.RED);
					
					}
					//else {
					if ( currentDistance >= lastDistance){
				//	Set alert to blue 
						
						resultLabel.setForeground(Color.blue);
						warmorcoldLabel.setText("getting colder ");
						warmorcoldLabel.setForeground(Color.blue);
					}
				
				if(guess > numberToGuess)
					resultLabel.setText("number to high");
					
					else if ( guess <numberToGuess)
						resultLabel.setText("number to  low");
					else if(guess == numberToGuess){
						
						resultLabel.setText("Correct");
				resultLabel.setForeground(Color.GREEN);
				warmorcoldLabel.setText("Great Job");
				warmorcoldLabel.setForeground(Color.GREEN);
					correct = true;
				}
				
				lastDistance = currentDistance;
				
				//}
		
			
	
		
		}
		
		
		guessattemptsLabel.setText(" guess attempts"+ guessCount);
		}
		}}
