from flask import Flask, render_template, request, jsonify

app = Flask(__name__)
feedbacks = []

@app.route('/')
def home():
    return render_template("index.html")

@app.route('/submit', methods=['POST'])
def submit_feedback():
    name = request.form.get("name")
    feedback = request.form.get("feedback")
    if name and feedback:
        feedbacks.append({"name": name, "feedback": feedback})
        return jsonify({"message": "Thank you for your review!"})
    return jsonify({"error": "Please enter all fields."})

@app.route('/feedbacks', methods=['GET'])
def get_feedbacks():
    return jsonify(feedbacks)

if __name__ == '__main__':
    app.run(debug=True)
