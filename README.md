import requests
import json
import os
from datetime import datetime

# ========= CONFIG =========
API_KEY = "your_api_key_here"
API_URL = "https://api.openai.com/v1/chat/completions"
MODEL = "gpt-4o-mini"

MEMORY_FILE = "memory.json"

# ========= LOAD MEMORY =========
def load_memory():
    if os.path.exists(MEMORY_FILE):
        with open(MEMORY_FILE, "r") as f:
            return json.load(f)
    else:
        return [
            {
                "role": "system",
                "content": "You are a smart, helpful, slightly witty AI assistant. Keep answers clear and useful."
            }
        ]

# ========= SAVE MEMORY =========
def save_memory(memory):
    with open(MEMORY_FILE, "w") as f:
        json.dump(memory, f, indent=2)

# ========= AI CALL =========
def chat_with_ai(memory, user_input):
    memory.append({"role": "user", "content": user_input})

    headers = {
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    }

    data = {
        "model": MODEL,
        "messages": memory,
        "temperature": 0.7
    }

    try:
        response = requests.post(API_URL, headers=headers, json=data)
        result = response.json()

        ai_reply = result["choices"][0]["message"]["content"]

        memory.append({"role": "assistant", "content": ai_reply})
        save_memory(memory)

        return ai_reply

    except Exception as e:
        return f"[Error]: {e}"

# ========= SIMPLE AGENT COMMANDS =========
def handle_commands(user_input):
    user_input = user_input.lower()

    if user_input == "time":
        return f"🕒 Current time: {datetime.now().strftime('%H:%M:%S')}"

    if user_input == "date":
        return f"📅 Today is: {datetime.now().strftime('%Y-%m-%d')}"

    if user_input.startswith("remember "):
        note = user_input.replace("remember ", "")
        with open("notes.txt", "a") as f:
            f.write(note + "\n")
        return "✅ I saved that in notes."

    if user_input == "notes":
        if os.path.exists("notes.txt"):
            with open("notes.txt", "r") as f:
                return "🧠 Your notes:\n" + f.read()
        return "No notes yet."

    return None

# ========= MAIN LOOP =========
def run_agent():
    memory = load_memory()

    print("\n🤖 AI Agent Ready! Type 'exit' to quit.\n")

    while True:
        user_input = input("You: ")

        if user_input.lower() == "exit":
            print("AI: Goodbye 👋")
            break

        # Check commands first
        command_response = handle_commands(user_input)
        if command_response:
            print("AI:", command_response)
            continue

        # Otherwise use AI
        reply = chat_with_ai(memory, user_input)
        print("AI:", reply)


# ========= START =========
if __name__ == "__main__":
    run_agent()
