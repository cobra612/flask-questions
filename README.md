# flask-questions
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        q1 = request.form.get('question1')
        q2 = request.form.get('question2')
        q3 = request.form.get('question3')
        
        # Process or display the answers, without saving them
        return f'''
            <h1>Thank you for your submission!</h1>
            <p>Are you a gooner? {q1}</p>
            <p>Are you a sigma? {q2}</p>
            <p>Who are you? {q3}</p>
        '''
    
    return '''
        <form method="post">
            <label>Are you a gooner? <input type="text" name="question1" required></label><br>
            <label>Are you a sigma? <input type="text" name="question2" required></label><br>
            <label>Who are you? <input type="text" name="question3" required></label><br>
            <input type="submit" value="Submit">
        </form>
    '''

if __name__ == '__main__':
    app.run(debug=True)

