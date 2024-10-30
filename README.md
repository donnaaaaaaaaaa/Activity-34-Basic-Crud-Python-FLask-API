# Activity-34-Basic-Crud-Python-FLask-API
Create app.py

Run Your Application

import flask
from flask import Flask, jsonify, request

app = Flask(__name__)
Create a List of Dictionaries
# Sample data: list of students
students = [
    {
        "name": "Juan Carlos",
        "section": "BSIT-4B",
        "id": 1,
        "email": "juan@gmail.com",
        "age": 22
    },
    {
        "name": "Jose Rizal",
        "section": "BSIT-2A",
        "id": 2,
        "email": "jose@gmail.com",
        "age": 21
    },
    {
        "name": "Juan Luna",
        "section": "BSIT-3A",
        "id": 3,
        "email": "juan@gmail.com",
        "age": 20
    },
    {
        "name": "Andres Bonifacio",
        "section": "BSIT-3A",
        "id": 4,
        "email": "andres@gmail.com",
        "age": 20
    },
    {
        "name": "Justin Bieber",
        "section": "BSIT-2A",
        "id": 5,
        "email": "justin@gmail.com",
        "age": 21
    },
    {
        "name": "Michael Jordan",
        "section": "BSIT-4A",
        "id": 6,
        "email": "michael@gmail.com",
        "age": 19
    },
    {
        "name": "Andrew Jordan",
        "section": "BSIT-3A",
        "id": 7,
        "email": "andrew@gmail.com",
        "age": 20
    },
    {
        "name": "Jessa Boe",
        "section": "BSIT-2B",
        "id": 8,
        "email": "jessa@gmail.com",
        "age": 18
    },
    {
        "name": "Ted Talk",
        "section": "BSIT-3B",
        "id": 9,
        "email": "ted@gmail.com",
        "age": 19
    }
]
Get All Student
GET /students: Retrieve all students.

@app.route('/students', methods=['GET'])
def get_students():
    return jsonify(students)
Get All Students (GET /students): Returns a list of all students in JSON format.



GET STUDENT BY ID
# READ: Get a specific student by ID
@app.route('/students/<int:student_id>', methods=['GET'])
def get_student(student_id):
    student = next((student for student in students if student["id"] == student_id), None)
    if student:
        return jsonify(student)
    else:
        return jsonify({"message": "Student not found"}), 404
GET /students/<id>: Retrieve a specific student by ID.


ADD STUDENT
@app.route('/students', methods=['POST'])
def add_student():
    new_student = request.get_json()
    new_student['id'] = max(student['id'] for student in students) + 1  # Generate new ID
    students.append(new_student)
    return jsonify(new_student), 201
POST /students: Create a new student, send a JSON body.


UPDATE STUDENT
@app.route('/students/<int:student_id>', methods=['PUT'])
def update_student(student_id):
    student = next((student for student in students if student["id"] == student_id), None)
    if student:
        data = request.get_json()
        student.update(data)
        return jsonify(student)
    else:
        return jsonify({"message": "Student not found"}), 404
PUT /students/<id>: Update a specific student by ID, send a JSON body.


DELETE: Remove a student by ID
# DELETE: Remove a student by ID
@app.route('/students/<int:student_id>', methods=['DELETE'])
def delete_student(student_id):
    student = next((student for student in students if student["id"] == student_id), None)
    if student:
        students.remove(student)
        return jsonify({"message": "Student deleted"})
    else:
        return jsonify({"message": "Student not found"}), 404

if __name__ == '__main__':
    app.run(debug=True)
DELETE /students/<id>: Delete a student by ID.


REMEMBER ADD THIS CODE
if __name__ == '__main__':
    app.run(debug=True)
Using Postman, you can test each endpoint by sending the appropriate requests.
This API provides a simple and clean structure to manage students’ data with CRUD operations.





