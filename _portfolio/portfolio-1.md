---
title: "Tohono O'odham FLEx Dictionary"
excerpt: "Digitalization of the Tohono O'odham dictionary by Madeleine Mathiot<br/><img src='/images/papagoDictpdf.png' width='300'>"
collection: portfolio
---


## Introduction

The main focus of this project was to digitalize a dictionary of the O'odham language, spoken in the Sonoran desert of Arizona and northern Mexico by the Tohono O'odham ("Desert People"). The source text is in a flat, text-based format, and my goal was to transform it into a structured representation that could be more easily analyzed and useful to the Tohono O'odham and linguists. While the original dictionary contains rich lexical and grammatical information, its lack of consistent structure makes it difficult to use for both linguistic research and computational applications.


## Background

Tohono O’odham is an Indigenous language spoken in the southwestern United States and northern Mexico, with significant cultural and linguistic importance. Linguistic resources for such languages are often stored in legacy formats that are not immediately compatible with modern tools. One such tool is FLEx (FieldWorks Language Explorer), which is widely used for lexical database management and language documentation. Dictionary entries typically include multiple components such as headwords, parts of speech, morphological information, example sentences, and cross-references. However, these elements are not always clearly separated in raw text, which introduces challenges for computational processing.

## Problem Statement

The primary challenge of this project lies in converting semi-structured dictionary text into a fully structured format. The source data contains inconsistencies, such as varying use of punctuation, abbreviations, and embedded notes. Additionally, certain patterns—such as “see” references or parenthetical notes—can be difficult to distinguish from core lexical information. These issues make it difficult to reliably extract fields like part of speech, senses, and morphological features using straightforward methods. As a result, a more nuanced parsing approach was required to handle these ambiguities. Below is a snippet from the first page of the dictionary, in the format it was given to me (.docx/.pdf). You can see from this snippet the structure I had to contend with: boldface, page numbers, guide words, and the alphabetical range header. 

<img src='/images/papagoDictpdf.png'>

## Approach

To address these challenges, I developed a multi-step parsing pipeline that processed each dictionary entry individually. The approach begins by identifying entry boundaries and then progressively extracting specific components such as headwords, parts of speech, and definitions. A key design decision was to represent each entry as a Lexeme object, allowing for a clear and extensible data structure. Regular expressions and rule-based heuristics were used to identify patterns within the text. Special attention was given to ambiguous cases, where multiple interpretations of the text were possible.


## Implementation

The parser was implemented in Python, using built-in libraries such as *re* for regular expression pattern matching. Each dictionary entry is processed and converted into a structured object with predefined fields. One of the main challenges was correctly handling nested or overlapping annotations, such as parentheses containing additional metadata. Another difficulty involved distinguishing between true lexical content and cross-references introduced by terms like “see.” To address these issues, I implemented custom logic to isolate and categorize different types of information. The resulting data structure allows for easier manipulation and export to other formats. 

(add in about mapping to the Standard lexical data format)

## Results

The final output is a usable dictionary in the FLEx dictionary software. In many cases, the parser successfully extracted key components such as headwords, parts of speech, and definitions. For example, an originally unstructured entry can be transformed into a format where each element is explicitly labeled and accessible. However, some edge cases remain challenging and may require additional refinement.

### Example 1

Here is an example of a typically structured dictionary entry that was correctly parsed in my parser, with all the necessary items being mapped to the correct fields in FLEx. The headword maps to Lexeme Form, definition to definition, Part of speech to Grammatical Info, and the examples which map to a field for the sentence in the vernacular (Tohono O'odham), and the translation (English).

<img src='/images/normal entry txt file.png'>
<img src='/images/normal entry flex.png'>

### Example 2

Here is an example of an entry where the headword is actually part of a phrase, but the phrase itself is not a part of the lexicon. 

<img src='/images/in phrase dict.png'>

This was a structure that I did not take into account when I was writing my parser, and therefore did not get parsed correctly. The parser recognized "'o'ohon in Jios-'O'ohon" as the entire headword. 

<img src='/images/flex entry in phrase.png'>

I fixed entries like this manually, by putting "in Jios-'O'ohon" in the *Restrictions* field, to show that this particular usage of *'o'ohon* is restricted to its use in the whole phrase "Jios-'O'ohon."

<img src='/images/flex in phrase fixed.png'>

### Example 3

Here is another example of a common incorrect parsing. In the below image, the headword is *'i'ihugga*, followed by a cross reference to another entry *vud 'ihugga*. My parser should be easily able to handle this entry because it fits the standard format of *headword* "see" *POS* *Cross-referenced word* "=" *definition*. The problem with this particular case is that the word order of *vud 'ihugga* is not in the same format that the actual entry for that lexical item is in.

<img src='/images/vud word.png'>

Below is how *vud 'ihugga* actually appears in the dictionary. It is entered as *'ihugga vud*, which the parser did not recognize to be the same thing as *vud 'ihugga*. 

<img src='/images/word vud.png'>

This is how this was parsed in FLEx. This is another case where I manually fixed entries of this variety. 

<img src='/images/flex entry parse of vud word.png'>

Here is how the final entry looked after I manually fixed the croff-reference.

<img src='/images/iihugga fixed.png'>

## Bonus

I also turned this project into an Android application, using the Dictionary App Builder software by SIL. This is available [here](https://github.com/lizuhle/Tohono-O-odham-Dictionary/releases/tag/v1.0/Tohono_O.odham-1.0.apk) for download, and I hope to have it available on the Google Play Store too. This app will hopefully serve as a useful tool for anyone needing to access Tohono O'odham language data. Here are some screenshots from the application. 

<img src='/images/app_a_list'> <img src='/images/app_entry_ex.png'> 
<img src='/images/app_search_function.png'> <img src='/images/app_search_results.png'>

#### Download instructions
##### How to install:

1. Download APK
2. Open file
3. Allow unknown apps
4. Install

## Conclusion

One of the most challenging aspects of this project was dealing with inconsistencies in the source data. Small variations in formatting often required additional rules or exceptions in the parser. This highlighted the difficulty of working with real-world linguistic data, which rarely conforms to strict standards. At the same time, the project provided valuable insight into the structure and complexity of dictionary entries. It also reinforced the importance of balancing precision with flexibility when designing parsing systems. In summary, this project demonstrates a method for converting unstructured dictionary data into a structured format suitable for computational use. By developing a custom parser, it is possible to extract meaningful linguistic information from complex text. This work contributes to broader efforts in language documentation and the development of tools for under-resourced languages. Ultimately, structuring this data makes it more accessible for both linguistic analysis and practical applications, and is hopefully a useful tool for the Tohono O'odham people.

## Future Work

Future improvements could focus on increasing the robustness of the parser, particularly in handling edge cases. Additionally, a user interface could be developed to allow for easier browsing and searching of the dictionary. More advanced techniques, such as machine learning, could also be explored to improve parsing accuracy. There remain a few issues in the dictionary entries themselves, as I was not able to look at every single entry to ensure that everything parsed 100% correctly. I plan to do a more comprehensive review in the future and make an update to the app. 






### Evaluation criteria
Remember that each of the two projects in your portfolio will be evaluated on these points:

* **Length**: A summary of the project goals, technology used, and outcomes, as appropriate for a general technical audience, between 1000 and 3000 words (not counting code)
* **Content**: student’s experience demonstrates the learning outcomes for the MSHLT program [^note]
* **Code**: Code is contained in the site, or a link to the code (such as in a GitHub repository) exists on the site.
* **Above and beyond**: How well does this component communicate the most relevant features?

[^note]: The learning outcomes of the MSHLT program are:
    
    1. Students will demonstrate programming skills for the workplace.
    2. Students will be able to use fundamental algorithms and concepts in Natural Language Processing.
    3. Students will show knowledge of tools and packages used in Natural Language Processing.
