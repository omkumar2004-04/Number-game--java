# Number-game--java
import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {
    
    // Method to play one round of the game
    public static boolean playRound() {
        Random rand = new Random();
        // Step 1: Generate a random number between 1 and 100
        int numberToGuess = rand.nextInt(100) + 1;
        
        // Step 5: Limit the number of attempts to 10
        int attempts = 10;
        
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the Number Guessing Game!");
        System.out.println("I have generated a number between 1 and 100. Try to guess it!");
        
        // Step 2: Prompt the user to guess the number
        while (attempts > 0) {
            System.out.println("You have " + attempts + " attempts left.");
            System.out.print("Enter your guess: ");
            
            // Input validation
            if (!scanner.hasNextInt()) {
                System.out.println("Please enter a valid number.");
                scanner.next(); // Consume invalid input
                continue;
            }
            
            int userGuess = scanner.nextInt();
            
            // Step 3: Compare the user's guess with the generated number
            if (userGuess < numberToGuess) {
                System.out.println("Your guess is too low.");
            } else if (userGuess > numberToGuess) {
                System.out.println("Your guess is too high.");
            } else {
                System.out.println("Congratulations! You guessed the correct number!");
                return true; // Correct guess, round won
            }
            
            attempts--; // Decrease the number of attempts left
        }
        
        System.out.println("Sorry, you've run out of attempts. The correct number was " + numberToGuess + ".");
        return false; // Failed to guess the number
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int totalRoundsWon = 0;
        int totalRoundsPlayed = 0;
        
        // Step 6: Add the option for multiple rounds
        while (true) {
            totalRoundsPlayed++;
            
            if (playRound()) {
                totalRoundsWon++;
            }
            
            // Step 7: Display user's score (rounds won / rounds played)
            System.out.println("\nYour score: " + totalRoundsWon + " out of " + totalRoundsPlayed + " rounds won.");
            
            // Ask the user if they want to play again
            System.out.print("\nDo you want to play another round? (yes/no): ");
            String playAgain = scanner.next().toLowerCase();
            
            if (!playAgain.equals("yes")) {
                System.out.println("Thank you for playing! Goodbye!");
                break;
            }
        }
        
        scanner.close();
    }
}
