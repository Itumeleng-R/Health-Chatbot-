# Health-Chatbot-
# --- FOL Healthcare Chatbot ---

# Knowledge base using FOL-style rules
knowledge_base = {
    "flu": ["fever", "cough", "sore_throat"],
    "common_cold": ["sneezing", "runny_nose", "mild_fever"],
    "malaria": ["fever", "chills", "sweating", "headache"],
    "covid19": ["fever", "cough", "shortness_of_breath", "loss_of_taste"],
    "strep_throat": ["sore_throat", "swollen_lymph_nodes", "fever"]
}

# Advice base for each disease
advice_base = {
    "flu": [
        "Rest and drink plenty of fluids.",
        "Use fever reducers if needed.",
        "Avoid contact with others."
    ],
    "common_cold": [
        "Get adequate rest.",
        "Stay warm and hydrated.",
        "Use over-the-counter cold remedies."
    ],
    "malaria": [
        "Seek medical attention immediately.",
        "Take prescribed antimalarial medication.",
        "Rest and monitor your fever closely."
    ],
    "covid19": [
        "Self-isolate and get tested.",
        "Monitor symptoms and oxygen levels.",
        "Consult a healthcare provider if symptoms worsen."
    ],
    "strep_throat": [
        "See a doctor for antibiotics.",
        "Avoid sharing personal items.",
        "Stay home until 24 hours after antibiotics begin."
    ]
}

# Function to get symptoms from user
def get_user_symptoms():
    print("Welcome to HealthBot!")
    print("Enter your symptoms (comma-separated): ")
    user_input = input("Symptoms: ").lower()
    
    # Clean and split the input
    symptoms = [symptom.strip().replace(" ", "_") for symptom in user_input.split(",") if symptom.strip()]
    return symptoms

# Function to infer disease(s) based on user symptoms
def infer_disease(user_symptoms):
    possible_diseases = []

    for disease, symptoms in knowledge_base.items():
        if all(symptom in user_symptoms for symptom in symptoms):
            possible_diseases.append(disease)

    return possible_diseases

# Main chatbot function
def run_chatbot():
    user_symptoms = get_user_symptoms()
    diseases = infer_disease(user_symptoms)

    if diseases:
        print("\nBased on your symptoms, you might have:")
        for disease in diseases:
            print(f"- {disease.replace('_', ' ').title()}")
            print("  Advice:")
            for advice in advice_base[disease]:
                print(f"    • {advice}")
    else:
        print("\nNo matching disease found.")
        print("Please consult a healthcare professional.")

# Start the chatbot
if __name__ == "__main__":
    run_chatbot()
