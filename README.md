# roulette-shutdown
Roulette Shutdown is a subtle background app that introduces an element of chance to your PC. Every 30 minutes, it randomly checks (with a 1% probability) to trigger a shutdown. Be aware, this is purely chance-based, (AND I AM NOT RESPONSIBLE) for any work loss or data issues resulting from a sudden shutdown. Use with caution.
Thank you for using my app :3
and now the code yipppp!!!


import random
import time
import os
import tkinter as tk
import winsound

def show_countdown():
    root = tk.Tk()
    root.title("WARNING")
    root.geometry("300x150")
    root.resizable(False, False)
    root.attributes("-topmost", True)

    label = tk.Label(root, text="You got unlucky!\nYour PC is shutting down in:", font=("Arial", 12))
    label.pack(pady=10)

    countdown_label = tk.Label(root, text="30", font=("Arial", 40, "bold"), fg="red")
    countdown_label.pack()

    def play_beep():
        winsound.Beep(1000, 500)
        root.after(1000, play_beep)

    def update_countdown(seconds):
        if seconds <= 0:
            root.destroy()
        else:
            countdown_label.config(text=str(seconds))
            root.after(1000, update_countdown, seconds - 1)

    play_beep()
    update_countdown(30)
    root.mainloop()

def maybe_shutdown():
    if random.random() < 0.01:
        os.system("shutdown /s /t 30")
        show_countdown()
    else:
        print("Safe this time... Next check in 30 minutes.")

while True:
    maybe_shutdown()
    time.sleep(30 * 60)
