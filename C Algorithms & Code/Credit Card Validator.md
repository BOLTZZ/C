# Credit Card Validator:
<strong>Background:</strong>
* Credit cards are plastic cards with which you can pay for goods or services on credit. There are 3 types of credit cards (American Express, MasterCard, and Visa) this program will validate. American Express uses 15-digit numbers, MasterCard uses 16-digit numbers, and Visa uses 13- and 16-digit numbers. Also, all Visa cards start with a 4, American Express starts with a 34 or 37, and, for this example, most MasterCard cards start with 51, 52, 53, 54, or 55.
* <em>Luhn's Algorithm</em> is used to determine if a credit card is syntactically valid, invented by Hans Peter Luhn of IBM:
  1. First, multiply every other digit by 2, starting with the number’s second-to-last digit, and then add those products’ digits together.
  2. Next, add the sum to the sum of the digits that weren’t multiplied by 2.
  3. If the total is divisible by 10 (or, put more formally, if the total modulo 10 is congruent to 0), the number is valid!
* An example of Luhn's Algorithm on a valid card number: 4003600000000014.
  1. We can gather all the every other digit by 2 in the number (bolded): <strong>4</strong>0<strong>0</strong>3<strong>6</strong>0<strong>0</strong>0<strong>0</strong>0<strong>0</strong>0<strong>0</strong>0<strong>1</strong>4. So now we have to multiply by 2: 1•2 + 0•2 + 0•2 + 0•2 + 0•2 + 6•2 + 0•2 + 4•2 = 2 + 0 + 0 + 0 + 0 + 12 + 0 + 8 and we have to add the digits of each number together: 2 + 0 + 0 + 0 + 0 + 1 + 2 + 0 + 8 = 13.
  2. Now, we need to add the previous sum (13) to the digits that weren't multiplied: 13 + 4 + 0 + 0 + 0 + 0 + 0 + 3 + 0 = 20.
  3. 20 is divisibile by 10, 20 % 10 = 0, so the credit card number is syntactically correct.
  
<strong>Program Explanation:</strong>
1. First, the program will take in the input of the numbers as a long data type. With the input it'll perform the 1st step of the Luhn's Algorithm by sorting out for every alternating digit, multiplying by 2, and summing the digits.
2. Next, the program will perform the 2nd step of the algorithm by summing up the rest of the digits and adding the new sum to the previous sum. Also, it'll find out if the number is syntactically correct.
3. Lastly, the program will find out which card the number belongs to using the differences between each card type, mentioned earlier. These are what will be printed out: Visa - "VISA\n", American Express - "AMEX\n", MasterCard - "MASTERCARD\n", and Invalid numbers - "INVALID\n".

<strong>Code:</strong>
```c
// Include modules:
#include <stdio.h>
#include <cs50.h>
// "Trick" C into running the get_card() method by showing it here:
int get_card(long card);
// Main Function:
int main(void)
{
    // Get the card number from the user:
    long card_num = get_long("Number:");
    // Run the get_card() function, inputting the card number and storing the output as an int object (num):
    int num = get_card(card_num);
    // Check if num is either 0, 1, 2, or 3 and output the correct response:
    if (num == 0)
    {
        printf("INVALID\n");
    } 
    else if (num == 1)
    {
        printf("AMEX\n");
    } 
    else if (num == 2)
    {
        printf("VISA\n");
    } 
    else if (num == 3)
    {
        printf("MASTERCARD\n");
    }
}
// get_card() function:
int get_card(long card)
{
    // Store the value of the card number in another long object (copy):
    long copy = card;
    // Set an int object (count) to 1, this will store the number of digits in copy:
    int count = 1;
    // Keeps on looping until copy is less than 10 and divides copy by 10, while adding 1 to count.
    // This helps gather the number of digits in copy:
    while (copy > 10)
    {
        copy = copy / 10;
        count ++;
    }
    // Sets an int object (lastDigit) to the last digit of card, the value of card % 10 (modulus 10):
    int lastDigit = card % 10;
    // Set int objects (x, z, first, and next) to 1, 1, 0, and 0, respectivley.
    int x = 1;
    int z = 1;
    int first = 0;
    int next = 0;
    // A for loop that counts down from each digit:
    for (int i = count; i >= 1; i --)
    {
        // Checks if the current digit position (i) is alternating by 2 from the last digit by if count - x equals i:
        if (count - x == i)
        {
            // Sets copy to card and filters out the digit in position i:
            copy = card;
            for (int y = 1; y <= x; y ++)
            {
                // Sets copy to copy minus the current last digit, all divided by 10. Also, set last digit to the copy modulus 10:
                copy = (copy - lastDigit) / 10;
                lastDigit = copy % 10;
            }
            // Create an int object (under) equal to 2 times the alternating digit (copy % 10):
            int under = 2 * (copy % 10);
            // Checks if under is greater than 10 which means it has 2 digits:
            if (under >= 10)
            {
                // Locates the ones digit of the 2 digit number and adds it to 1 since the highest 2 digit number is 18 (2 * 9):
                int ones = under % 10;
                under = ones + 1;
            }
            // Adds under to first, sets lastDigit to the last digit of card, and increases x by 2:
            first += under;
            lastDigit = card % 10;
            x += 2;
        } 
        // Checks if the digit position (i) isn't one of the alternating digits:
        else 
        {
            // Sets copy to card and filters out the digit in position i:
            copy = card;
            for (int y = 0; y <= (z - 2); y ++)
            {
                // Sets copy to copy minus the current last digit, all divided by 10. Also, set last digit to the copy modulus 10: 
                copy = (copy - lastDigit) / 10;
                lastDigit = copy % 10;
            }
           // Create an int object (under) equal to 2 times the alternating digit (copy % 10):
            int under = 2 * (copy % 10);
            // Checks if under is greater than 10 which means it has 2 digits:
            if (under >= 10)
            {
                // Locates the ones digit of the 2 digit number and adds it to 1 since the highest 2 digit number is 18 (2 * 9):
                int ones = under % 10;
                under = ones + 1;
            }
            // Adds under to next, sets lastDigit to the last digit of card, and increases z by 2: 
            next += under;
            lastDigit = card % 10;
            z += 2;
        }
    }
    // Sets int objects (ans, option, firstdigit, and seconddigit) to the last digit of first + next, 0, 0, and 0, respectivley:
    int ans = (first + next) % 10;
    int option = 0;
    int firstdigit = 0;
    int seconddigit = 0;
    // Checks the first two digits (firstdigit and seconddigit) of the card number, so it can be identified as American Express, Visa, or MasterCard:
    if (ans == 0)
    {
        // Sets copy to card and loops until copy is greater than 10^(count - 1):
        copy = card;
        while (copy > pow(10, (count - 1)))
        {
            // Sets copy to copy minus 10^(count - 1) and increases firstdigit by 1:
            copy = copy - pow(10, (count - 1));
            firstdigit ++;
        }
        // Sets copy to card - (firstdigit * 10^(count - 1)) so we can figure out the second digit. Loops until copy is greater than 10^(count - 2):
        copy = card - (firstdigit * pow(10, (count - 1)));
        while (copy > pow(10, (count - 2)))
        {
            // Sets copy to copy minus 10^(count - 2) and increases seconddigit by 1:
            copy = copy - pow(10, (count - 2));
            seconddigit ++;
        }
    }
    // Checks if the length of the number is 15 and it's syntactically valid and if the first digit is 3 and if either the second digit is 7 or 4 (AMEX):
    if ((count == 15 && ans == 0) && (firstdigit == 3 && (seconddigit == 7 || seconddigit == 4)))
    {
        option = 1;
    } 
    // Checks if the length of the number is 14 and the first digit is 4 or if the length is 16 and the first digit is 4 with it being syntactically valid (VISA):
    else if (((count == 13 && firstdigit == 4) || (count == 16 && firstdigit == 4)) && ans == 0)
    {
        option = 2;
    } 
    // Checks if the length is 16 with it being syntactically valid and the first digit being 5 with the second digit being either 1, 2, 3, 4, or 5 (MASTERCARD):
    else if ((count == 16 && ans == 0) && (firstdigit == 5 && ((seconddigit == 1 || seconddigit == 2) || (seconddigit == 3 
    || (seconddigit == 4 || seconddigit == 5)))))
    {
        option = 3;
    } 
    // Otherwise it's just INVALID:
    else 
    {
        option = 0;
    }
    // Returns the value of option:
    return option;
}
```
<strong>Demostration:</strong>
* Note: The Walkthrough is just an explanation of the project, NOT the solution code. You can find the video [here](https://youtu.be/dF7wNjsRBjI)

![1](https://github.com/BOLTZZ/C/blob/master/Images%20and%20Gifs/credit%20card%20verifier.gif)
