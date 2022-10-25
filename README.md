# rockpapersciccors.lanaalpachachi
My personal repository for Rock Paper Scissors

# My keras.model predictions:

from ast import main
import random
import cv2
from keras.models import load_model
import numpy as np
import time
from enum import IntEnum 
import random 

model = load_model('keras_model.h5')
cap = cv2.VideoCapture(0)
data = np.ndarray(shape=(1, 224, 224, 3), dtype=np.float32)

while True: 
    ret, frame = cap.read()
    resized_frame = cv2.resize(frame, (224, 224), interpolation = cv2.INTER_AREA)
    image_np = np.array(resized_frame)
    normalized_image = (image_np.astype(np.float32) / 127.0) - 1 # Normalize the image
    data[0] = normalized_image
    prediction = model.predict(data)
    cv2.imshow('frame', frame)
    # Press q to close the window
    print(prediction)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
            
# After the loop release the cap object
cap.release()
# Destroy all the windows
cv2.destroyAllWindows()


# My code to play against the computer:

# while True:
    
#     possible_actions = ['rock', 'paper', 'scissors']
#     user_choice = input("Enter a choice (rock, paper, scissors): ")
#     computer_choice = random.choice(possible_actions)

#     print(f"\nYou chose {user_choice}, and the computer chose {computer_choice}.\n")

#     if user_choice == computer_choice:
#         print(f"Both players selected {user_choice}. It's a tie!")
        
#     elif user_choice == "rock":
#         if computer_choice == 'scissors':
#             print("Rock smashes scissors! You win!")
#         else:
#             print("Paper covers rock! You lose.")

#     elif user_choice == 'paper':
#         if computer_choice == 'rock': 
#             print("Paper covers rock! You win!")
#         else: print("Scissors cuts paper! You lose.")

#     elif user_choice == "scissors":
#         if computer_choice == "paper": 
#             print("Scissors cuts paper! You win!")
#         else: 
#             print("Rock smashes scissors! You lose")
        
#     play_again = input("Play again? (y/n): ")
#     if play_again.lower() != "y": 
#         break

import random 
from enum import IntEnum 

class Action(IntEnum): 
    Rock = 0 
    Paper = 1
    Scissors = 2
    Nothing = 3 

def get_user_choice():
    user_choice = input("Enter a choice (rock[0], paper[1], scissors[2])")
    selection = int(user_choice)
    action = Action(selection)
    return action 

def get_computer_selection():
    selection = random.randint(0, len(Action) -1)
    action = Action(selection)
    return action 

def get_winner(user_choice, computer_choice): 
    if user_choice == computer_choice:
        print(f"Both players selection {user_choice}. It's a tie!")
    elif user_choice == Action.Rock:
        if computer_choice == Action.Scissors:
            print("Rock smashes scissors! You win!")
        else:
            print("Paper covers rock! You lose.")
    elif user_choice == Action.Paper:
        if computer_choice == Action.Rock:
            print("Paper covers rock! You win!")
        else:
            print("Scissors cuts paper! You lose.")
    elif user_choice == Action.Scissors:
        if computer_choice == Action.Paper:
            print("Scissors cuts paper! You win!")
        else: print("Rock smashes scissors! You lose.")

def play(): 
    while True: 
        try:
            user_choice = get_user_choice()
        except ValueError as e:
            range_str = f"0, {len(Action) -1}"
            print(f"Invalid selection. Enter a value in the range {range_str}")
            continue 

        computer_choice = get_computer_selection()
        get_winner(user_choice, computer_choice)

        play_again = input("Play again? (y/n):" )
        if play_again.lower() != "y":
            break 



# Get prediction / play with video camera 
class_map = {
        'rock': 0, 
        'paper': 1, 
        'scissors': 2, 
        'nothing': 3 
}
 
def get_predictions(play, ):

# a way to find highest value in those four elements 
# index the list of numbers and find the highest probability and use that 


# Countdown method before showing hands
    def countdown(time_sec):
        while time_sec:
            mins, secs = divmod(time_sec, 60)
            timeformat = '{:02d}:{:02d}'.format(mins, secs)
            print(timeformat, end='\r')
            time.sleep(1)
            time_sec -= 1

        print("stop")

# Add the 'you chose user choice print later

    

    if __name__ == "__main__":
        play()
