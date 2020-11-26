# VIT-SoftwareDev
#include <stdio.h> 
#include <stdlib.h> 
#include <stdbool.h> 

#define P1 
#define P2

struct move 
{ 
	int player1; 
	int player2; 
}; 
void showPlayer (int player[], int n) 
{ 
	int i; 
	printf ("Current Game Status -> "); 
	for (i=0; i<n; i++) 
		printf ("%d ", player[i]); 
	printf("\n"); 
	return; 
} 
bool gameOver(int player[], int n) 
{ 
	int i; 
	for (i=0; i<n; i++) 
		if (player[i]!=0) 
			return (false); 

	return (true); 
} 

void declareWinner(int whoseTurn) 
{ 
	if (whoseTurn == P1) 
		printf ("\nP1 won\n\n"); 
	else
		printf("\P2won\n\n"); 
	return; 
}  
int calculateGame(int player[], int n) 
{ 
	int i, game = player[0]; 
	for (i=1; i<n; i++) 
		game = game ^ player[i]; 
	return(game); 
} 

void makeMove(int player[], int n, struct move * moves) 
{ 
	int i, game_played = calculateGame(player, n);  
	if (game_played != 0) 
	{ 
		for (i=0; i<n; i++) 
		{ 
			 
			if ((player[i] ^ game_played) < player[i]) 
			{ 
				(*moves).player1 = i; 
				(*moves).player2 = 
								player[i]-(player[i]^game_played); 
				player[i] = (player[i] ^ game_played); 
				break; 
			} 
		} 
	} 

	else
	{  
		int non_zero_indices[n], count; 

		for (i=0, count=0; i<n; i++) 
			if (player[i] > 0) 
				non_zero_indices [count++] = i; 

		(*moves).player1 = (rand() % (count)); 
		(*moves).player2 = 
				1 + (rand() % (player[(*moves).player1])); 
		player[(*moves).player1] = 
		player[(*moves).player1] - (*moves).player2; 

		if (player[(*moves).player1] < 0) 
			player[(*moves).player1]=0; 
	} 
	return; 
} 
void playGame(int player[], int n, int whoseTurn) 
{ 
	printf("\nGAME STARTS\n\n"); 
	struct move moves; 

	while (gameOver (player, n) == false) 
	{ 
		showPlayer(player, n); 

		makeMove(player, n, &moves); 

		if (whoseTurn == P2) 
		{ 
			printf("Player 1 "
				"at index %d\n", moves.player2, 
				moves.player1); 
			whoseTurn = P1; 
		} 
		else
		{ 
			printf(""
				"index %d\n", moves.player2, 
				moves.player1); 
			whoseTurn = P2; 
		} 
	} 

	showPlayer(player, n); 
	declareWinner(whoseTurn); 
	return; 
} 

void knowWinnerBeforePlaying(int player[], int n, 
							int whoseTurn) 
{ 
	printf("P1 playing the game -> "); 

	if (calculateGame(player, n) !=0) 
	{ 
		if (whoseTurn == P2) 
			printf("P2 will win\n"); 
		else
			printf("P1 will win\n"); 
	} 
	else
	{ 
		if (whoseTurn == P2) 
			printf("P1 will win\n"); 
		else
			printf("P2 will win\n"); 
	} 

	return; 
} 

int main() 
{ 
	int player[] = {3, 4, 5}; 
	int n = sizeof(player)/sizeof(player[0]); 
 
	knowWinnerBeforePlaying(player, n, P1);  
	playGame(player, n, P1);  
	int player[] = {3, 4, 7}; 
	int n = sizeof(player)/sizeof(player[0]); 
	knowWinnerBeforePlaying (player, n, P2);  
	playGame (player, n, P1); */

	return(0); 
}


Problem Statement:  
https://docs.google.com/document/d/16CNXNQ-VLLSoVe7CvJFBzueawgrCjWorB7zMLNvOF94/edit?usp=sharing
