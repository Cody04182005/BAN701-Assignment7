"""Number Guessing Game - BAN 701 Assignment 7.

Concepts demonstrated: variables, input, conditionals, loops,
functions, lists, and random values.
"""

import random

MAX_ATTEMPTS = 7
LOWEST = 1
HIGHEST = 100


def get_guess(low, high):
    """Keep asking until the player enters a valid whole number."""
    while True:
        text = input(f"Enter your guess ({low}-{high}): ").strip()
        if not text.isdigit():
            print("Please enter a whole number.")
        elif not low <= int(text) <= high:
            print(f"Your guess must be between {low} and {high}.")
        else:
            return int(text)


def play_round():
    """Play one round and return True if the player won."""
    secret = random.randint(LOWEST, HIGHEST)
    guesses = []  # list of every guess made this round

    print(f"\nI'm thinking of a number from {LOWEST} to {HIGHEST}.")
    print(f"You have {MAX_ATTEMPTS} attempts.\n")

    for attempt in range(1, MAX_ATTEMPTS + 1):
        guess = get_guess(LOWEST, HIGHEST)
        guesses.append(guess)

        if guess == secret:
            print(f"Correct! You got it in {attempt} attempt(s).")
            print(f"Your guesses: {guesses}")
            return True
        elif guess < secret:
            print("Too low.")
        else:
            print("Too high.")
        print(f"Attempts left: {MAX_ATTEMPTS - attempt}\n")

    print(f"Out of attempts! The number was {secret}.")
    print(f"Your guesses: {guesses}")
    return False


def main():
    print("=== Number Guessing Game ===")
    wins = 0
    rounds = 0

    while True:
        rounds += 1
        if play_round():
            wins += 1

        again = input("\nPlay again? (y/n): ").strip().lower()
        if again != "y":
            break

    print(f"\nFinal score: {wins} win(s) out of {rounds} round(s). Thanks for playing!")


if __name__ == "__main__":
    main()
