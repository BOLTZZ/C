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
// Credit Card Verifier:
// Ojas Nimase
#include <stdio.h>
#include <cs50.h>
int get_card(long card);
int main(void)
{
    long card_num = get_long("Number:");
    int num = get_card(card_num);
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
int get_card(long card)
{
    long copy = card;
    int count = 1;
    while (copy > 10)
    {
        copy = copy / 10;
        count ++;
    }
    int lastDigit = card % 10;
    int x = 1;
    int z = 1;
    int first = 0;
    int next = 0;
    for (int i = count; i >= 1; i --)
    {
        if (count - x == i)
        {
            long second = card;
            for (int y = 1; y <= x; y ++)
            {
                second = (second - lastDigit) / 10;
                lastDigit = second % 10;
            }
            int under = 2 * (second % 10);
            if (under < 0)
            {
                under = under * -1;
            }
            if (under >= 10)
            {
                int ones = under % 10;
                under = ones + 1;
            }
            first = first + under;
            lastDigit = card % 10;
            x += 2;
        } 
        else 
        {
            long second = card;
            for (int y = 0; y <= (z - 2); y ++)
            {
                second = (second - lastDigit) / 10;
                lastDigit = second % 10;
            }
            int under = second % 10;
            if (under < 0)
            {
                under = under * -1;
            }
            if (under >= 10)
            {
                int ones = under % 10;
                under = ones + 1;
            }
            next = next + under;
            lastDigit = card % 10;
            z += 2;
        }
    }
    int ans = (first + next) % 10;
    int option = 0;
    int firstdigit = 0;
    int seconddigit = 0;
    if (count == 16 && ans == 0)
    {
        long create = card;
        while (create > 1000000000000000)
        {
            create = create - 1000000000000000;
            firstdigit ++;
        }
    }
    if (count == 15 && ans == 0)
    {
        long create = card;
        while (create > 100000000000000)
        {
            create = create - 100000000000000;
            firstdigit ++;
        }
        create = card - (firstdigit * 100000000000000);
        while (create > 10000000000000)
        {
            create = create - 10000000000000;
            seconddigit ++;
        }
    }
    if (count == 16 && ans == 0)
    {
        long create = card - (firstdigit * 1000000000000000);
        while (create > 100000000000000)
        {
            create = create - 100000000000000;
            seconddigit ++;
        }
    }
    if ((count == 15 && ans == 0) && (firstdigit == 3 && (seconddigit == 7 || seconddigit == 4)))
    {
        option = 1;
    } 
    else if (((count == 13 && firstdigit == 4) || (count == 16 && firstdigit == 4)) && ans == 0)
    {
        option = 2;
    } 
    else if ((count == 16 && ans == 0) && (firstdigit == 5 && ((seconddigit == 1 || seconddigit == 2) || (seconddigit == 3 
    || (seconddigit == 4 || seconddigit == 5)))))
    {
        option = 3;
    } 
    else 
    {
        option = 0;
    }
    return option;
}
```
