Applicant Guidelines
===
* Inform HR when you plan to start the test. The start date should be agreed between the applicant and HR.
* On the agreed start date, HR will give you access to the test repository in GitLab. 
* Fork this repository immediately to your personal GitLab account once HR confirmed your access.
* HR will inform you of your exam deadline.
* Make sure that your forked repository is private and add cafe24ph username as a Developer.
* Do not clone the repository. Your forked repository should appear in the original repository's fork list.
* Branch out from the master branch and name the new branch with your name.
* Follow the instructions and answer the five questions within your branch.
* When you're done, create a merge request to the master branch and send an email to HR with the following details:
  * Working Branch Name
  * Merge Request Link
  * Final Commit Hash
* If you have any issues, kindly contact HR.


Question # 1 - Site Traffic Scenario
---
__Scenario:__<br>
You have a website that tracks a lot of statistics about the population in general. The average number of visitors to your site is about 200 a day worldwide. Due to this small number, you haven’t thought about improving anything on your website since you’ve started up the website. Due to the outbreak of coronavirus, you had an idea to provide other statistics on your website. So you added a new section for coronavirus statistics on your website and deployed it. Suddenly, the number of visitors per day jumped from 200 to 200,000 a day worldwide. Your site monitoring logs started sending HTTP errors, and finally, your hosting server went down.

__Questions:__<br>
1. What could be the reasons why there were a lot of HTTP errors, and finally, your hosting server went down? Enumerate all possible reasons you can think of.
2. How will you solve each enumerated reasons?
3. What will be your priorities in resolving each issue? List your enumerated action plans and order them from highest priority to lowest.

__Answer: <#List of issues and action plans ordered by priority>__


Question #2 - Optimized SQL Query
---
Refer to q2-erd.png in this repository.

With the given ERD, construct an optimized SQL query to gather the following results in the most efficient way.

##### Rider Delivery Information
* Order No:
* Branch:
* Branch Address:
* Food List (with price and count):
* Total Amount:
* Customer Contact No:
* Customer Address:

__Answer: <#Optimized SQL query>__
```$sql

```

Question #3 - Search Algorithm
---
Given the multi-dimensional array:
```$php
$posts = [
    "1001" => [
        "title" => "Siargao Moments",
        "subtitle" => "Surf all you want.",
        "content" => "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas egestas euismod nisl sollicitudin efficitur.",
        "author" => ["name" => "John Smith", "points" => 205,],
        "likes" => 19,
        "tags" => ["travel", "siargao", "surfallyouwant"],
        "images" => [
            ["caption" => "The beach", "src" => "/images/the-beach-travel-thumb.jpg", "link" => "/the-beach-travel.jpg"],
            ["caption" => "Island view", "src" => "/images/island-view-thumb.jpg", "link" => "/images/island-view.jpg"]
        ]
    ],
    "1002" => [
        "title" => "Travelling to Mt. Pulag",
        "subtitle" => "Luzon's highest summit.",
        "content" => "Curabitur eros eros, convallis id tortor ac, imperdiet pulvinar erat. In semper, sem non pulvinar tempor, odio ex auctor purus, id venenatis mauris arcu ac augue.",
        "author" => ["name" => "Juan Dela Cruz", "points" => 125,],
        "likes" => 37,
        "tags" => ["mountains", "summit"],
        "images" => [
            ["caption" => "The summit view", "src" => "/images/travel-thumb.jpg", "link" => "/images/image1.jpg"],
            ["caption" => "Mountain travels", "src" => "/images/mountain-travels-thumb.png", "link" => "/images/mountain-travels.png"]
        ]
    ],
    "1003" => [
        "title" => "Sumilon Island",
        "subtitle" => "Swim with the whale sharks.",
        "content" => "Praesent a odio sed lacus blandit porta ac sit amet ex. Pellentesque eu posuere diam. Proin vestibulum aliquam laoreet. Duis at posuere magna.",
        "author" => ["name" => "Pinoy Travels", "points" => 517,],
        "likes" => 118,
        "tags" => ["cebu", "whalesharks"],
        "images" => [
            ["caption" => "Island Hopping", "src" => "/images/island-hopping-thumb.jpg", "link" => "/images/island-hopping.jpg"],
            ["caption" => "Whale Sharks", "src" => "/images/whale-sharks-thumb.png", "link" => "/images/whale-sharks.png"]
        ]
    ],
];
```

Create a search algorithm within a function that will satisfy the following requirements:
* Actual code is not needed. Write the specific step by step algorithm in pseudo-code.
* Search keyword: island
* The search algorithm should search in all post array elements except the author and likes.
* The search algorithm should search image captions only from the image element.
* The search result should be sorted in descending order based on likes, then based on author points.
* The algorithm should search for a partial match and should be case-insensitive.

__Answer: <#Search function in pseudocode>__


Question #4 - Online Course Registration App Design
---
__Specifications:__
* Courses can be equal to 1 to 3 units.
* Each student must apply for courses which total 18 to 21 units.
* Courses that are 1-2 units will be taught for 2 hours a week, while courses with 3 units will be taught for 2 hours twice a week.
* For every course, the system will provide 3 classes.
* Each class can accommodate 20-50 students.
* The Schedule of each class of a course should not overlap with each other.
* Class hours are Monday to Friday, 7 AM up to 9 PM, and each day must consist of 1-8 classes.
* Students must not be able to enroll in a class if the class hour overlaps with an already enrolled class.
* Students may cancel on a class they are enrolled in.

__Requirements:__<br>
* Provide a flowchart of the application design and commit it in the root directory with a filename of "q4-answer".

__Instructions:__<br>
* Use app.diagrams.net and export your flowchart and ERD to an image and commit in the given directory.

__Answer: <#App Design Flowchart>__
