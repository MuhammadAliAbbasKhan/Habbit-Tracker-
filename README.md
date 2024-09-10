
Cycling Graph Project - Pixela API Integration

This project demonstrates how to integrate with the Pixela API to create a graph that tracks cycling distances. Pixela (https://pixe.la/) is a service that allows you to visualize daily habits by creating graphs and updating them with data.

Project Overview
This Python script connects to the Pixela API to:

Create a new user.
Create a graph to track cycling data.
Post daily updates on the number of kilometers cycled.
Update a day's data.
Delete a day's data.


Prerequisites
Python 3.x
requests library (pip install requests)
A Pixela account (create one at Pixela)

Required Variables
USERNAME: Your Pixela username.
TOKEN: A self-generated authentication token (used to authenticate API requests).
GRAPH_ID: A unique ID for your graph (must be a lowercase string of 1–16 characters).

How to Use
Install Dependencies: You need to install the requests library if you haven't already:

Bash Code
pip install requests
Update Variables:

Replace the following placeholders in the code with your actual Pixela username, token, and desired graph ID:

USERNAME = "YOUR USERNAME"
TOKEN = "YOUR SELF GENERATED TOKEN"
GRAPH_ID = "YOUR GRAPH ID"
User Creation (Optional)

If you haven't created a Pixela account programmatically, uncomment and run the following block in the script:

Bash Code
response = requests.post(url=pixela_endpoint, json=user_params)
print(response.text)
This will create a new Pixela user with the username and token you've provided.

Create a Graph

After setting up your username and token, you can create a graph to track your cycling distances by uncommenting the following lines:

Bash Code
response = requests.post(url=graph_endpoint, json=graph_config, headers=headers)
print(response.text)
Log Daily Cycling Data

To log the number of kilometers you cycled today, run the script, and it will prompt you to input the data:

Bash Code
quantity = input("How many kilometers did you cycle today? ")
The data will be sent to Pixela and added to your graph.

Update Data for a Specific Day

If you need to update the cycling data for a specific day, uncomment the following code:

Bash Code
response = requests.put(url=update_endpoint, json=new_pixel_data, headers=headers)
print(response.text)
This will update the cycling data for the current day.

Delete Data for a Specific Day

To delete data for a specific day, uncomment and run the following code:

Bash Code
response = requests.delete(url=delete_endpoint, headers=headers)
print(response.text)
Code Explanation
User Creation

Bash Code
user_params = {
    "token": TOKEN,
    "username": USERNAME,
    "agreeTermsOfService": "yes",
    "notMinor": "yes",
}
response = requests.post(url=pixela_endpoint, json=user_params)
This block of code creates a new Pixela user. It requires agreeing to the terms of service and confirming that you're not a minor.

Graph Creation

Bash Code
graph_config = {
    "id": GRAPH_ID,
    "name": "Cycling Graph",
    "unit": "Km",
    "type": "float",
    "color": "ajisai"
}
response = requests.post(url=graph_endpoint, json=graph_config, headers=headers)
This creates a graph with the specified GRAPH_ID, tracking kilometers cycled. The graph will display data as floating-point numbers and use the "ajisai" color.

Adding Data to the Graph

Bash Code
pixel_data = {
    "date": today.strftime("%Y%m%d"),
    "quantity": input("How many kilometers did you cycle today? "),
}
response = requests.post(url=pixel_creation_endpoint, json=pixel_data, headers=headers)
This block allows the user to input how many kilometers they cycled today, and then it sends that data to Pixela, adding it to the graph.

Updating Data

Bash Code
new_pixel_data = {
    "quantity": "4.5"
}
response = requests.put(url=update_endpoint, json=new_pixel_data, headers=headers)
This block updates the cycling data for a specific day, which is useful if you need to correct the value.

Deleting Data

Bash Code
response = requests.delete(url=delete_endpoint, headers=headers)
This block deletes the data for a specific day from the graph.

Conclusion
This script is a simple yet powerful way to track and visualize your daily habits using the Pixela API. You can extend the project to track more types of activities or habits and automate the process of adding data each day.

Reference:
Pixela API Documentation: https://docs.pixe.la






