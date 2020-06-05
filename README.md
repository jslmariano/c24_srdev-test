Cafe24 Philippines Inc.
===

### SENIOR DEVELOPER - Take Home/Practical Test

Applicant Guidelines
===
* Inform HR when you plan to start the test. The start date should be agreed between the applicant and HR.
* On the agreed start date, HR will give you access to the test repository in GitLab.
* Fork this repository immediately to your personal GitLab account once HR confirmed your access.
* Do not clone the original repository and only push changes to your forked repository.
* HR will inform you of your exam deadline.
* Make sure that your forked repository is private and add cafe24ph username as a Developer.
* Do not clone the repository. Your forked repository should appear in the original repository's fork list.
* Branch out from the master branch of your forked repository and name the new branch with your name.
* Follow the instructions and answer the four (4) questions within your branch.
* When you're done, create a merge request to the **master branch of your forked repository** and send an email to HR with the following details:
  * Working Branch Name
  * Merge Request Link
  * Final Commit Hash
* If you have any issues, kindly contact HR.

##### WARNING: Do not send a merge request to the original repository. Use your forked repository for changes and merge request. Thank you.


Question # 1 - Site Optimization and Server Skills
---
__Scenario:__<br>
You have a website that tracks a lot of statistics about the population in general. The average number of visitors to your site is about 200 a day worldwide. Due to this small number, you haven’t thought about improving anything on your website since you’ve started up the website. Due to the outbreak of coronavirus, you had an idea to provide other statistics on your website. So you added a new section for coronavirus statistics on your website and deployed it. Suddenly, the number of visitors per day jumped from 200 to 200,000 a day worldwide. Your site monitoring logs started sending HTTP errors, and finally, your hosting server went down.

__Questions:__<br>
1. What could be the reasons why there were a lot of HTTP errors, and finally, your hosting server went down? Enumerate all possible reasons you can think of.
2. How will you solve each enumerated reasons?
3. What will be your priorities in resolving each issue? List your enumerated action plans and order them from highest priority to lowest.

__Answer: <#List of issues and action plans ordered by priority>__

1. If the data displayed on the website is coming from a 3rd-party api.
    - Check the 3rd party APIS doc if it has rate-limiting terms.
    - If it has a rate-limiting term, you can try contacting the provider to request an increase for the said API
1. If the hosting provider has a QUOTA per request marked on your account
    - File a quota increase on your provider so you can accept requests more than the limit within your accounts quota
1. If the error was **HTTP 429 Too Many Requests**
    - Adjust web service (nginx/apache) configuration files to accept many  requests
    - Use AB load testing to tune the correct configuration
1. If the error is someother like 4xx and 5xx
    - Check/Configure the database to accept simultaneous connections ( if data is in database )
    - Optimize the database queries ( if data is in database )
    - Check/Optimize the codes if poorly written
    - Consider using a CDN for resources like CSS, JS, Images to reduce bandwidth on your server, high bandwidth can strain your server eventually returning some few HTTP Code errors in general
1. Assuming there is no rate-limit, quota on account, application is optimized, and query is optimized, then consider enhancements below
    - Consider using REDIS and store datasets that are rarely updated from the database
    - Use a load balancer and a group of instances to tame high volume requests
    - Use database caching for common queries
    - Use database replication with multiple read-only slaves ( For heavy selects )
    - Use database connection pooler ( For heavy connection rate )
    - Check latency between application and database as this may cause 5xx sometimes or HTTP REQUESTS time outs. Consider moving the database and instances under the same region


Question #2 - Database Schema and SQL
---
Refer to q2-erd.png in this repository. https://gitlab.com/cafe24ph/srdev-test/-/blob/master/q2-erd.png

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
```
select
    -- Order No
    invoice.id as "Order No"
    -- Branch
    ,branch.name as "Branch"
    -- Branch Address
    ,branch.address as "Branch Address"
    -- Food List (with price and count)
    ,group_concat(concat("Name: ", food.name), concat(" Price: " , food.price), concat(" Count: " , order_food.count) SEPARATOR ', ') as "Food List ( with price and count )"
    -- Total Amount
    ,invoice.total_amount as "Total Amount"
    -- Customer Contact No
    ,customer.contact_number as "Customer Contact No"
    -- Customer Address
    ,customer.address as "Customer Address"
from
    invoice
left join branch on branch.id = invoice.branch_id
left join delivery on delivery.invoice_id = invoice.id
left join customer on customer.id = delivery.customer_id
left join order_food on order_food.invoice_id = invoice.id
left join food on food.id = order_food.food_id
left join rider on rider.id = delivery.rider_id
where rider.name = "<Input RIDER NAME>" -- You can also comment this to show all orders
group by invoice.id, customer.id
;

```

Question #3 - Logic and Algorithm Skills
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

1. **FUNCTION** search_exam
1. **ACCEPT** array argument current_posts
1. **ACCEPT** string argument search_this
1. **DECLARE** array sorted_posts
1. **DECLARE** array search_results
1. **DECLARE** array sort_maps
1. **FOR EVERY** current_post **WITH** post_key **IN** current_posts
    1. **DECLARE** string search_in
    1. **ASSIGN** search_in = search_in & "\<space\>" & current_post[ 'title' ]
    1. **ASSIGN** search_in = search_in & "\<space\>" & current_post[ 'subtitle' ]
    1. **ASSIGN** search_in = search_in & "\<space\>" & current_post[ 'content' ]
    1. **FOR EVERY** tag **IN** current_post[ tags ]
        1. **ASSIGN** search_in = search_in & "\<space\>" & tag
    1. **ENDFOR**
    1. **FOR EVERY** image **IN** current_post[ images ]
        1. **ASSIGN** search_in = search_in & "\<space\>" & image[ 'caption' ]
    1. **ENDFOR**
    1. **SET** search_in **TO LOWERCASE**
    1. **SET** search_this **TO LOWERCASE**
    1. **IF** search_in **CONTAINS** search_this **THEN**
          1. **ASSIGN** search_results[ post_key ] = current_post
    1. **ENDIF**
1. **ENDFOR**
1. **FOR EVERY** search_result **WITH** result_key **IN** search_results
    1. **DECLARE** array sort_map
    1. **ASSIGN** sort_map[ 'result_key' ] = result_key
    1. **ASSIGN** sort_map[ 'likes' ] = search_result[ 'likes' ]
    1. **ASSIGN** sort_map[ 'points' ] = search_result[ 'author' ][ 'points' ]
    1. **PUSH** array sort_map **IN** array sort_maps
1. **ENDFOR**
1. **FOR** J = 0 **TO** sort_maps size **STEP INCREMENT** J
    1. **FOR** I = 0 **TO** sort_maps size - 1 **STEP INCREMENT** I
        1. **IF** sort_maps[ i ][ 'points' ] is less than sort_maps[ i + 1 ][ 'points' ] **THEN**
            1. **ASSIGN** temp = sort_maps[ i + 1 ]
            1. **ASSIGN** sort_maps[ i + 1 ] = sort_maps[ i ]
            1. **ASSIGN** sort_maps[ i ] = temp
        1. **ENDIF**
        1. **IF** sort_maps[ i ][ 'likes' ] is less than sort_maps[ i + 1 ][ 'likes' ] **THEN**
            1. **ASSIGN** temp = sort_maps[ i + 1 ]
            1. **ASSIGN** sort_maps[ i + 1 ] = sort_maps[ i ]
            1. **ASSIGN** sort_maps[ i ] = temp
        1. **ENDIF**
    1. **ENDFOR**
1. **ENDFOR**
1. **FOR EVERY** sort_map **IN** sort_maps
    1. **ASSIGN** key = sort_map[ 'result_key' ]
    1. **ASSIGN** sorted_posts[ key ] = search_results[ key ]
1. **ENDFOR**
1. **RETURN** array sorted_posts
1. **END**

Question #4 - App Design Flowchart
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
* Use app.diagrams.net and export your flowchart to an image and commit in the given directory.

__Answer: <#App Design Flowchart>__
