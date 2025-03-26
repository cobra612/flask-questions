# flask-questions
from flask import Flask, render_template, request
import sqlite3

app = Flask(__name__)

# Initialize database
def init_db():
    with sqlite3.connect("answers.db") as conn:
        cursor = conn.cursor()
        cursor.execute('''CREATE TABLE IF NOT EXISTS responses (
                            id INTEGER PRIMARY KEY AUTOINCREMENT,
                            question1 TEXT,
                            question2 TEXT,
                            question3 TEXT)''')
        conn.commit()

init_db()

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        q1 = request.form.get('question1')
        q2 = request.form.get('question2')
        q3 = request.form.get('question3')
        
        with sqlite3.connect("answers.db") as conn:
            cursor = conn.cursor()
            cursor.execute("INSERT INTO responses (question1, question2, question3) VALUES (?, ?, ?)", (q1, q2, q3))
            conn.commit()
        
        return "Thank you for your submission!"
    
    return '''
        <form method="post">
            <label>Are you a gooner? <input type="text" name="question1" required></label><br>
            <label>Are you a sigma? <input type="text" name="question2" required></label><br>
            <label>Who are you? <input type="text" name="question3" required></label><br>
            <input type="submit" value="Submit">
        </form>
    '''

if __name__ == '__main__':
  app.run(host='0.0.0.0', port=5000)
