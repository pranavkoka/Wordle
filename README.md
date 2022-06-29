# Wordle
Code for Wordle using Python

```

import random
from words import words

print('If a letter is displayed in uppercase, it means that it is in its correct position. If it is displayed in lowercase, it means that it is in an incorrect position.')

def get_5_letter_word(words):
	word = random.choice(words)
	while len(word)!= 5 or ' ' in word or '-' in word:
		word = random.choice(words)
	return word.upper()

def removecommon(word1,word2):
	word3=word1
	for i in range(0,5):
		for j in range(0,5):
			if word1[i] in word2[j]:
				word3 = word3[0:i] + '-' + word3[i+1:5]
				word2 = word2[0:j] + '-' + word2[j+1:5]
	return(word3)

def wordle():
	
	word = get_5_letter_word(words)
	final_word = '-----'
	tries = 6
	
	while tries > 0 and (final_word.isupper() == False or '-' in final_word): 
		final_word = '-----'
		if tries == 1:
			print(f"You have {tries} try remaining.")
		else:
			print(f"You have {tries} tries remaining.")
		guess = input("Enter a 5 letter word: ").upper()

		for i in range(0,5):
			if guess[i] == word[i]:
				final_word = final_word[0:i] + guess[i] + final_word[i+1:5]
		
		rc = removecommon(word,final_word)
		for j in range(0,5):
			if guess[j] != word[j] and guess[j] in list(rc):
			 	final_word = final_word[0:j] + guess[j].lower() + final_word[j+1:5]
			 	for k in range(0,5):
			 		if rc[k]==guess[j]:
			 			rc = rc[0:k] + '-' + rc[k+1:5]

		print(final_word)
		tries = tries - 1
	
	if tries == 0 and (final_word.isupper() == False or '-' in final_word):
		print(f"You lost! The word was {word}.")
	else:
		print(f"You won! The word is {word}.")

wordle()

```
