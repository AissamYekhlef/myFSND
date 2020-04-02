
Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

## GET /categories
* Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category.
* Request Arguments: None
* Returns: List of available categories.
##### Example Response
```json 
{
  "categories":
     {
      "1":"Science",
      "2":"Art",
      "3":"Geography",
      "4":"History",
      "5":"Entertainment",
      "6":"Sports" 
     },
  "success":true
}

```

## GET /questions?page=<page_number>
* Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category.
* Fetches a dictionary of questions in which the keys are the answer, category, difficulty, id and question.
* Request Arguments: Page Number
* Returns: List of questions, number of total questions, current category and categories, total available pages.
##### Example Response 
```json 
{
  "categories":
    {
      "1":"Science",
      "2":"Art",
      "3":"Geography",
      "4":"History",
      "5":"Entertainment",
      "6":"Sports"
    },
  "page": "2/4",  
  "current_category":null,
  "questions":[
    {
      "answer":"f",
      "category":1,
      "difficulty":4,
      "id":34,
      "question":"d"
     }
    ],
  "success":true,
  "totalQuestions":21
}
```
## DELETE /questions/<question_id>
* Delete question from the questions list.
* Request Arguments: Question Id
* Returns: true if successfully deleted and total questions.
##### Example Response 
```json
{
  "deleted":12,
  "success":true,
  "totalQuestions":19
}
```
## POST /questions
* Create a new question
* Request Body: question, answer, difficulty and category.
* Returns: true if successfully created, id of created question and total questions.
##### Example Request Payload 
```json 
{
  "question":"a",
  "answer":"b",
  "difficulty":"3",
  "category":1
}
```
##### Example Response 
```json 
{
  "created":23,
  "success":true,
  "totalQuestions":20
}
```
## POST /questions?page=<page_number>
* Searches for the questions
* Request Arguments: Page Number
* Request Body: search_data
* Returns: List of questions, number of total questions and current category, total available pages.
##### Example Request Payload 
```json 
{
  "searchTerm":"what" 
}
```
##### Example Response 
```json 
{
  "current_category":null,
  "page": "1/4",
  "questions":[
      {
        "answer":"Lake Victoria",
        "category":3,
        "difficulty":2,
        "id":13,
        "question":"What is the largest lake in Africa?"
      },
      {
        "answer":"Mona Lisa",
        "category":2,
        "difficulty":3,
        "id":17,
        "question":"La Giaconda is better known as what?"
      },
      {
        "answer":"The Liver",
        "category":1,
        "difficulty":4,
        "id":20,
        "question":"What is the heaviest organ in the human body?"
      },
      {
        "answer":"Blood",
        "category":1,
        "difficulty":4,
        "id":22,
        "question":"Hematology is a branch of medicine involving the study of what?"
      }
   ],
  "success":true,
  "totalQuestions":4
 }
```
## GET /categories/<int:category_id>/questions
* To get questions based on category
* Request Arguments: Category Id and Page Number.
* Returns: List of questions, number of total questions and current category, total available pages.
##### Example Response 
```json 
{
  "current_category":
    {
      "id":1,
      "type":"Science"
    },
  "page": "1/4",
  "questions":[
      {"answer":"The Liver","category":1,"difficulty":4,"id":20,"question":"What is the heaviest organ in the human body?"},
      {"answer":"Alexander Fleming","category":1,"difficulty":3,"id":21,"question":"Who discovered penicillin?"},
      {"answer":"Blood","category":1,"difficulty":4,"id":22,"question":"Hematology is a branch of medicine involving the study of what?"},
      {"answer":"scs","category":1,"difficulty":1,"id":26,"question":" x"},
      {"answer":"de","category":1,"difficulty":1,"id":33,"question":"de"},
      {"answer":"aa","category":1,"difficulty":4,"id":35,"question":"aa"}
     ],
  "success":true,
  "totalQuestions":6
}
```
## POST /quizzes
* To get questions to play the quiz.
* Request Body: quiz_category and previous_questions.
* Returns: Random questions within the given category.
##### Example Request Payload
```json 
{
"previous_questions":[],
"quiz_category":
  {
    "type":"Science",
    "id":1
  }
}
```
##### Example Response 
```json 
{
  "question":
  {
    "answer":"Blood",
    "category":1,
    "difficulty":4,
    "id":22,
    "question":"Hematology is a branch of medicine involving the study of what?"
  },
  "success":true
}
```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
