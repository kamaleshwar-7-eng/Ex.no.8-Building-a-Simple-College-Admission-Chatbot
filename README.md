# Ex.No.8 – Building a Simple Saveetha College Admission Chatbot

## AIM

To design, implement and test a simple rule-based chatbot in Python that answers frequently asked questions related to Saveetha Engineering College admissions, such as courses offered, eligibility criteria, fees, application process, required documents, important dates, hostel facilities, location and contact details.

## INTRODUCTION

A chatbot is a software application that simulates a conversation with a human user, typically through text.

A rule-based chatbot works by comparing the user's message against a predefined set of keywords or patterns and returning a suitable pre-written response. It does not require a large training dataset or complex machine learning model, making it a simple and beginner-friendly approach for understanding the basic working of conversational AI.

In this experiment, a Saveetha Engineering College Admission Chatbot is developed to act as a virtual help-desk assistant. It can identify common admission-related questions and provide suitable predefined responses.

## PROCEDURE

### Step 1: Import Required Libraries

- `re` – Python's regular expression module, used to search for keyword patterns in the user's message.
- `random` – used to randomly select one response when multiple responses are available for the same intent.



### Step 2: Design the Knowledge Base

The chatbot knowledge base is stored as a Python dictionary.

Each intent represents a particular admission-related topic, such as:

- Greeting
- Courses
- Eligibility
- Fees
- Application process
- Required documents
- Important dates
- Hostel
- Location
- Contact details
- About the college
- Goodbye

Each intent contains:

1. **Patterns** – keywords or phrases that may appear in the user's question.
2. **Responses** – predefined answers that the chatbot can provide.

This structure makes the chatbot easy to extend because additional admission topics can be added to the knowledge base.


### Knowledge Base Summary

| Intent | Purpose |
|---|---|
| Greeting | Handles greetings from the user |
| Courses | Provides information about courses |
| Eligibility | Handles eligibility-related questions |
| Fees | Handles fee-related queries |
| Application | Provides application process information |
| Documents | Provides information about required documents |
| Dates | Handles admission dates and deadlines |
| Hostel | Provides hostel-related information |
| Location | Provides college location |
| Contact | Handles contact-related queries |
| About | Provides general college information |
| Goodbye | Ends the conversation |


### Step 3: Function to Match User Input to an Intent

The `match_intent()` function identifies the topic of the user's question.

The function:

- Converts the user's input into lowercase.
- Removes unnecessary spaces.
- Checks the input against the predefined patterns.
- Uses `re.search()` to identify matching patterns.
- Returns the corresponding intent when a match is found.
- Returns `None` when no matching intent is identified.


### Step 4: Define the Chatbot Response Function

The `get_response()` function generates the chatbot's response.

The function:

- Calls `match_intent()` to identify the user's intention.
- Selects a response from the corresponding intent.
- Uses `random.choice()` when multiple responses are available.
- Provides a fallback response when the chatbot cannot identify the user's query.

### Step 5: Build the Interactive Conversation Loop

The `chat()` function creates the interactive conversation between the user and the chatbot.

The function:

- Displays a welcome message.
- Uses `input()` to receive questions from the user.
- Sends each question to `get_response()`.
- Displays the generated response.
- Continues the conversation until the user enters `bye`, `exit`, or `quit`.
- Terminates the conversation with a suitable goodbye message.


### Step 6: Test the Chatbot with Sample Queries

A list of sample admission-related questions is used to test the chatbot.

The sample queries cover different intents such as:

- Greeting
- Courses
- Eligibility
- Fees
- Application process
- Documents
- Admission dates
- Hostel
- Location
- Contact
- College information
- Goodbye

Each query is passed through the same response-generation function used by the live chatbot.


### Step 7: Run the Chatbot

The complete Python script is executed in Google Colab.

The program first performs automated testing using predefined sample queries. After testing, the interactive `chat()` function is started, allowing the user to communicate with the chatbot in real time.

The chatbot identifies the user's query based on predefined patterns and returns an appropriate response.
## PROGRAM
```python

import re
import random


intents = {

    "greeting": {
        "patterns": [
            r"\bhi\b",
            r"\bhello\b",
            r"\bhey\b",
            r"good morning",
            r"good afternoon",
            r"good evening"
        ],
        "responses": [
            "Hello! Welcome to the Saveetha Engineering College Admission Chatbot.",
            "Hi! How can I help you with Saveetha Engineering College admissions?",
            "Welcome! I can help you with common admission-related queries."
        ]
    },

    "courses": {
        "patterns": [
            r"courses",
            r"course offered",
            r"courses offered",
            r"programs",
            r"programmes",
            r"branches",
            r"departments",
            r"what can i study"
        ],
        "responses": [
            "Saveetha Engineering College offers various undergraduate and postgraduate engineering programmes.",
            "The college offers engineering programmes in multiple disciplines. Please refer to the official college admission information for the current list of programmes.",
            "You can ask about a specific engineering branch to get more information."
        ]
    },

    "eligibility": {
        "patterns": [
            r"eligibility",
            r"eligible",
            r"qualification",
            r"qualifications",
            r"who can apply",
            r"eligibility criteria",
            r"requirements"
        ],
        "responses": [
            "Eligibility requirements depend on the programme and admission category. Students should check the current admission guidelines of Saveetha Engineering College.",
            "The required academic qualification varies depending on the course. Please verify the current eligibility criteria before applying.",
            "For accurate eligibility requirements, check the official admission guidelines for the selected programme."
        ]
    },

    "fees": {
        "patterns": [
            r"\bfees\b",
            r"fee structure",
            r"tuition fee",
            r"course fee",
            r"college fee",
            r"how much does it cost",
            r"fees details"
        ],
        "responses": [
            "Fee details depend on the programme and admission category.",
            "The fee structure may vary according to the selected course and admission category. Please check the current official fee details.",
            "For the latest tuition and other fee details, refer to the official Saveetha Engineering College admission information."
        ]
    },

    "application": {
        "patterns": [
            r"application",
            r"apply",
            r"how to apply",
            r"application process",
            r"admission process",
            r"how can i join",
            r"how do i apply"
        ],
        "responses": [
            "To apply, students should follow the current admission process provided by Saveetha Engineering College.",
            "The admission process generally involves selecting a programme, providing the required information and completing the application procedure.",
            "Please use the official college admission process for the current application procedure."
        ]
    },

    "documents": {
        "patterns": [
            r"documents",
            r"required documents",
            r"documents required",
            r"what documents",
            r"certificates",
            r"proof documents",
            r"document required"
        ],
        "responses": [
            "Admission may require academic certificates, identification documents, photographs and other documents specified by the college.",
            "Please keep your academic records and required identification documents ready for the admission process.",
            "The exact document list depends on the admission category and programme. Check the current admission instructions."
        ]
    },

    "dates": {
        "patterns": [
            r"admission date",
            r"admission dates",
            r"important dates",
            r"last date",
            r"deadline",
            r"when is admission",
            r"application deadline",
            r"last date to apply"
        ],
        "responses": [
            "Admission dates and application deadlines can change each academic year. Please check the current official admission schedule.",
            "For the latest application and admission dates, refer to the current Saveetha Engineering College admission announcement.",
            "The exact deadline depends on the admission cycle. Please verify the current dates before applying."
        ]
    },

    "hostel": {
        "patterns": [
            r"hostel",
            r"hostel facility",
            r"hostel facilities",
            r"accommodation",
            r"stay",
            r"hostel available"
        ],
        "responses": [
            "Hostel facilities are available for students. Details such as accommodation, rules and fees should be checked with the college.",
            "Students can enquire about hostel availability, facilities and fees through the college administration.",
            "For current hostel details, please refer to the college's official information."
        ]
    },

    "location": {
        "patterns": [
            r"where is the college",
            r"college location",
            r"location",
            r"where is saveetha",
            r"address",
            r"college address"
        ],
        "responses": [
            "Saveetha Engineering College is located at Thandalam, Chennai, Tamil Nadu.",
            "The college campus is located in Thandalam, Chennai, Tamil Nadu.",
            "Saveetha Engineering College is situated in Thandalam, Chennai."
        ]
    },

    "contact": {
        "patterns": [
            r"contact",
            r"contact details",
            r"contact number",
            r"phone number",
            r"email",
            r"admission contact",
            r"how can i contact"
        ],
        "responses": [
            "For admission-related contact details, please refer to the current official Saveetha Engineering College admission information.",
            "You can contact the college admission office using the contact details provided on the official college website.",
            "For the latest admission contact information, please check the official college admission page."
        ]
    },

    "about": {
        "patterns": [
            r"about college",
            r"about saveetha",
            r"tell me about saveetha",
            r"what is saveetha",
            r"college information"
        ],
        "responses": [
            "Saveetha Engineering College is an engineering institution located in Thandalam, Chennai, Tamil Nadu.",
            "Saveetha Engineering College provides undergraduate and postgraduate programmes in engineering and related disciplines."
        ]
    },

    "goodbye": {
        "patterns": [
            r"\bbye\b",
            r"\bgoodbye\b",
            r"\bexit\b",
            r"\bquit\b",
            r"see you"
        ],
        "responses": [
            "Thank you for using the Saveetha Engineering College Admission Chatbot. Goodbye!",
            "Thank you for your enquiry. Have a great day!",
            "Goodbye! Best wishes for your admission process."
        ]
    }
}


def match_intent(user_input):

    user_input = user_input.lower().strip()

    for intent, data in intents.items():

        for pattern in data["patterns"]:

            if re.search(pattern, user_input):
                return intent

    return None

def get_response(user_input):

    intent = match_intent(user_input)

    if intent is not None:

        return random.choice(
            intents[intent]["responses"]
        )

    return (
        "Sorry, I could not understand your question. "
        "You can ask about courses, eligibility, fees, "
        "application process, documents, admission dates, "
        "hostel, location or contact details."
    )


def chat():

    print("=" * 65)
    print("   SAVEETHA ENGINEERING COLLEGE ADMISSION CHATBOT")
    print("=" * 65)

    print(
        "\nHello! Welcome to the Saveetha Engineering College "
        "Admission Chatbot."
    )

    print(
        "You can ask me about courses, eligibility, fees, "
        "application process, documents, dates, hostel and contact details."
    )

    print("Type 'bye', 'exit' or 'quit' to end the conversation.\n")

    while True:

        user_input = input("You: ")

        response = get_response(user_input)

        print("Chatbot:", response)

        if match_intent(user_input) == "goodbye":
            break


sample_queries = [

    "Hello",

    "What courses are offered?",

    "What is the eligibility criteria?",

    "How much are the college fees?",

    "How can I apply for admission?",

    "What documents are required?",

    "What is the last date to apply?",

    "Does the college have hostel facilities?",

    "Where is Saveetha Engineering College located?",

    "How can I contact the admission office?",

    "Tell me about Saveetha Engineering College",

    "Bye"
]


print("\n")
print("=" * 65)
print("             AUTOMATED CHATBOT TEST")
print("=" * 65)

for query in sample_queries:

    print("\nYou:", query)

    response = get_response(query)

    print("Chatbot:", response)



print("\n")
print("=" * 65)
print("             STARTING LIVE CHAT")
print("=" * 65)

chat()
```

## OUTPUT
<img width="1234" height="364" alt="image" src="https://github.com/user-attachments/assets/8dbdc8e6-95dd-4852-ab4f-45a7fe38d585" />
<img width="1531" height="469" alt="image" src="https://github.com/user-attachments/assets/66fa59d3-c6b1-4b52-9f82-9b5d96407a2c" />

<img width="1517" height="528" alt="image" src="https://github.com/user-attachments/assets/c38e3bbf-7ee7-4d36-a07e-d57e05261f86" />

## OBSERVATION

The chatbot successfully identifies user queries by matching predefined keywords and patterns with the knowledge base.

The use of multiple responses for an intent allows the chatbot to provide varied responses instead of displaying exactly the same response every time.

The fallback response allows the chatbot to handle questions that do not match any predefined intent.

## RESULT

The Saveetha Engineering College Admission Chatbot was successfully designed, implemented and tested using Python.

The chatbot was able to identify common admission-related queries and provide appropriate predefined responses using pattern matching and a structured knowledge base.

## CONCLUSION

Thus, a simple rule-based Saveetha Engineering College Admission Chatbot was successfully developed using Python.

The experiment demonstrates the fundamental components of a conversational chatbot, including knowledge-base design, intent identification, pattern matching, response generation, fallback handling, and interactive conversation.

The experiment also provides a basic foundation for developing more advanced NLP- and AI-based conversational systems.
