from flask import Flask, request, jsonify
import openai

app = Flask(__name__)

# Replace with your OpenAI GPT API key
openai.api_key = "YOUR_OPENAI_API_KEY"

# Example resource FAQs and templates
resource_templates = {
    "scheduling": "Please confirm your availability for the following events: {events}",
    "onboarding": "Welcome, {name}! Here are your onboarding steps: {steps}",
    "donor": "Thank you, {donor}! Your donation of {amount} supports {project}.",
    "reporting": "Here is your weekly report summary: {summary}"
}

def generate_response(user_message):
    prompt = f"""You are a helpful nonprofit resource manager assistant. Based on the query below, respond appropriately:
    Query: "{user_message}"
    If the query references scheduling, onboarding, donor updates, or reports, use the matching template.
    Otherwise, respond as a friendly chatbot for nonprofits.
    """
    completion = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    return completion["choices"][0]["message"]["content"]

@app.route('/chat', methods=['POST'])
def chat():
    user_message = request.json.get("message", "")
    response = generate_response(user_message)
    return jsonify({"response": response})

if __name__ == '__main__':
    app.run(port=5000)
    
