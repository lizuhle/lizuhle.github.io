---
title: "Spanish Conjugation API"
excerpt: "A Flask-based web API that generates Spanish verb conjugations. <br/><img src='/images/SpanishConjugationAPI.png' width='300'>"
collection: portfolio
---


### Introduction

This Spanish Conjugation API is a Flask-based web application that generates verb conjugation tables for Spanish verbs. Users can enter a verb in its infinitive form, and the API returns its conjugated forms in a structured JSON response. There is a simple HTML interface so the API can be tested directly in the browser. What makes this project more than just a basic API is that it does not rely entirely on hardcoded data. Instead, it includes a scraping component that automatically collects conjugation data from an external source and stores it in a database. This turns the project into a small but complete system that handles data collection, storage, and retrieval. This project combines backend development with linguistic concepts to create a practical and useful language tool.



### Background

Verb conjugation is a core part of language, but it is also one of the more complex areas for learners. Verbs change depending on tense, person, and number, and there are many irregular forms that do not follow predictable patterns. This is essential information that any language learner needs to be able to reference easily. When working with language data, one of the biggest challenges is obtaining structured and reliable datasets. Manually entering conjugation data for every verb and tense would be extremely time-consuming and not scalable. Because of this, I wanted to explore how to automate the process of collecting linguistic data while still maintaining a clean and usable structure for the API. In computational linguistics, handling this type of variation correctly is an important part of language-related applications. I built this project to explore how linguistic rules can be represented in code while also learning API, database, and HTML design.



### Goal

The goal of this project was to create a working API that could take a Spanish verb (in the infinitive) as input and return its conjugated forms in a clear and structured way. In addition to that, I had several other goals:

* Store conjugation data in a database for easy recall
* Automatically populate that database using scraped data
* Represent linguistic information in a structured and reusable format
* Design the system in a modular way so it can be expanded in the future

I also wanted the project to reflect real-world development practices. That meant organizing the code cleanly, separating logic into different components, creating tests, and making sure the system could realistically scale if more data or features were added.



### Approach

I structured the project using a layered design. Flask handles incoming requests, a service layer processes the input and organizes the logic, and a MySQL repository handles database interactions. This separation keeps the code organized and easier to maintain.

On the linguistic side, I mapped Spanish pronouns (like “yo” and “tú”) to standardized grammatical categories (such as first person singular). This makes the output more consistent and easier to work with programmatically. 

Another key part of the approach was automating data collection. Instead of manually entering conjugations, I used web scraping to retrieve them from an external source. This required parsing HTML, identifying the correct table structure, and extracting the relevant information. Once extracted, the data is inserted into the database so it can be reused without needing to scrape again.



### Implementation

The backend is written in Python using Flask, with MySQL used to store conjugation data. A custom repository class handles database operations such as creating tables and inserting records.

To represent linguistic structure, I defined enums for tense and grammatical person, along with a Verb class that stores conjugations in a nested dictionary format. This allows conjugations to be accessed by both tense and person.

A key part of the implementation is the scraping module. Using requests and BeautifulSoup, the program sends a request to a conjugation website (wordreference.com), parses the HTML table containing verb forms, and extracts pronoun–conjugation pairs. These are then inserted into the MySQL database.

Currently, the system supports present tense conjugations for the verb *hablar* and includes all standard subject forms, including “vos.” Once the data is stored, the API retrieves it and returns it as a structured JSON response.



### Results

The system successfully handles both data collection and retrieval. When the program processes a verb like “hablar,” the scraper extracts the conjugations from the website, stores them in the database, and the API returns them in a structured format.

For example, here is the output for the verb *hablar* when entered by the user:

yo: hablo
tú: hablas
él/ella/usted: habla
nosotros: hablamos
vosotros: habláis
ellos/ellas/ustedes: hablan
vos: hablás

This output is returned as JSON, which makes it easy to integrate with other tools, such as language-learning apps or frontend interfaces. The inclusion of “vos” is especially useful, since it is often omitted in simpler conjugation tools. The project also demonstrates that the scraping pipeline works reliably for extracting structured data from HTML. Once the data is stored, it can be reused without repeated scraping, which improves efficiency.



### Conclusion

This project demonstrates how backend development, data collection, and linguistic modeling can work together in a single system. By combining an API, a database, and a scraping pipeline, the application goes beyond a static dataset and becomes a more dynamic tool. It also gave me hands-on experience with API design, database management, and structuring and testing code in a clean, modular way. Overall, this project serves as a strong foundation for more advanced language-processing tools. It demonstrates both technical ability and an understanding of how to work with linguistic data in a structured way.



### Future Work

There are several ways this project could be expanded:

* Add more verbs 
* Add more tenses (past, future, subjunctive, etc.)
* Additional features for language learners (irregular verb patterns)
* Allow for the user to enter a conjugated verb form ("hablo"), and return the correct verb and tense that correspond ("hablar, present tense, singular, first person")
* Improve error handling for unknown or invalid inputs
* Enhance the frontend for a better user experience
* Deploy the API so it can be accessed publicly

With these improvements, the API could evolve into a more complete tool for language learning or other NLP applications.


### Link to the code repository

Click [here](https://github.com/lizuhle/SpanishConjugationAPI)