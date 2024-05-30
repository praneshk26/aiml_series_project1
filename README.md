# aiml_series_project1
import random

class SimpleChatBot:
    def __init__(self):
        self.memory = {"prev_message": "", "prev_response": ""}
        self.greeted = False

    def greet(self):
        greetings = [
            "Hello! I'm your friendly chatbot. How can I help you today?",
            "Hi there! How can I assist you?",
            "Hey! What can I do for you?"
        ]
        return random.choice(greetings)

    def farewell(self):
        farewells = [
            "Goodbye! Have a great day!",
            "See you later! Take care!",
            "Bye! Have a wonderful day!"
        ]
        return random.choice(farewells)

    def respond_to_basic_questions(self, user_message):
        responses = {
            "hello": "Hi there! How can I assist you?",
            "how are you": "I'm fine. Thanks for asking!",
            "what's your name": "I'm a chatbot. You can call me Sara.",
            "who created you": "I was created by Pranesh.",
            "what can you do": "I can help you with information, answer your questions, or just have a chat. Feel free to ask me anything!",
            "who is the best cricketer in the world":"with no doubt,Mahendrasingh Dhoni"
        }
        return responses.get(user_message.lower(), None)

    def remember_context(self, user_message):
        if self.memory["prev_message"]:
            return f"You previously said: '{self.memory['prev_message']}'\n"
        return ""

    def respond(self, user_message):
        response = self.respond_to_basic_questions(user_message)
        if response:
            return response

        if "bye" in user_message.lower():
            return self.farewell()

        context_response = self.remember_context(user_message)
        response = context_response + "Sorry, I'm not sure how to respond to that."

       
        self.memory["prev_message"] = user_message
        self.memory["prev_response"] = response
        return response

    def ask_questions(self):
        questions = [
            "What's your favorite color?",
            "Do you have any hobbies?",
            "What's your favorite food?"
        ]
        for question in questions:
            print("Sara:", question)
            user_response = input("You: ")
            print("Sara:", f"That's interesting! You said your favorite {question.split()[-2].lower()} is {user_response}.")
    
    def chat(self):
        if not self.greeted:
            print(self.greet())
            self.greeted = True

        self.ask_questions()

        while True:
            user_message = input("You: ")
            if "bye" in user_message.lower():
                print("Sara:", self.respond(user_message))
                break
            else:
                print("Sara:", self.respond(user_message))


if __name__ == "__main__":
    chatbot = SimpleChatBot()
    chatbot.chat()
