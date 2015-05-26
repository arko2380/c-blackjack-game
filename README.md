# c-blackjack-game
Blackjack Card Game in C
#include <stdio.h>
#include <string.h>
#include <time.h>
#include <stdlib.h> //the last 2 are RNG

struct card
{ char rank [15];
  char suit [15];
  int value;
};

typedef struct card Card;

int main()
{ Card deck [52];
  int player = 0, dealer = 0, i;
  char answer [4];
  Card c, dealerHoldCard;
  double bet, cash = 1000;
 
  char ranks[13][15] = { "Ace", "King", "Queen", "Jack",
                         "Ten", "Nine", "Eight", "Seven",
                         "Six", "Five", "Four", "Three",
                         "Two"};
 
  char suits[4][15] = { "Hearts", "Diamonds", "Clubs", "Spades" };
 
  int values[13] = { 11, 10, 10, 10, 10, 9, 8, 7, 6, 5, 4, 3, 2 };
 
  for(i = 0; i < 52; i++)
   { strcpy(deck[i].rank, ranks[i%13]);
     strcpy(deck[i].suit, suits[i%4]);
     deck[i].value = values[i%13];
    }
 
  srand(time(0));
  
  for(i = 0; i < 52; i++)
  { Card temp = deck[i];
    int ran = rand()%52;
    deck[i] = deck[ran];
    deck[ran] = temp;
   }
  
  printf("Place your bet ");
  scanf("%lf", &bet);
 
  c = deck[top++];
 
  printf("Your first card is %s of %s \n", c.rank, c.suit);
  player = player + c.value;
 
  c = deck[top++];
 
  printf("Dealer is showing %s of %s \n", c.rank, c.suit);
  dealer = dealer + c.value;
 
  c = deck[top++];
 
  printf("Your second card is %s of %s \n", c.rank, c.suit);
  player = player + c.value;
 
  c = deck[top++];
  daler = dealer + c.value;
  dealerHoldCard = c;
 
  printf("More cards ? ");
  scanf("%s", answer);
 
  while(strcmp(answer, "yes") == 0 && player < 21)
   { c = deck[top++]
    
     printf("Your third card is %s of %s \n", c.rank, c.suit);
     player = player + c.value;
    
     printf("More cards ? ");
     scanf("%s", answer);
    }
 
  printf("Dealer's hold card is %s of %s \n", dealerHoldCard.rank, dealerHoldCard.suit);
 
  while(dealer < 17)
   { c = deck[top++];
    
     printf("Dealer takes %s of %s \n" c.rank, c.suit);
     dealer = dealer + c.value;
    }
   
  if(player <= 21 && dealer <= 21 && player > dealer)
   { cash = cash + bet;
     printf("You WIN and your cash is now %7.2f \n", cash);
    }
  else if(player <= 21 && dealer <= 21 && player < dealer)
   { cash = cash - bet;
     printf("You LOSE and your cash is now %7.2f \n", cash);
    }
  else if(player <= 21 && dealer <= 21 && player == dealer)
   { printf("The round is a draw \n"); }
  else if(player <= 21 && dealer > 21)
   { cash = cash + bet;
     printf("Dealer busted. You WIN. Your cash is now %7.2f \n", cash);
    }
  else if(player > 21 && dealer <= 21)
   { cash = cash - bet;
     printf("You busted. Your cash is now %7.2f \n", cash);
    }
  else
    printf("Dual bust. No winners. Your cash is %7.2f \n", cash);
   
  return 0;
 }
