# Chapter 3: Start with the Right Data Layer

## Summary

__Do Fun Things With Big Loud Wombats__: "D" is for Data

### Chapter goals:
- Explore how foundational data structures shape your project
- Introduce problems that illustrate impact of data structures on design decisions
- How building data structures in FP is different than OOP
- Put learnings to work in "quiz engine" project

### Access Patterns Shape Data Structures

Tic tac toe example

Requirements:

- Small game, so less concerned about performance
- Frequent board updates

Which data structure should we use to represent the board?

- Tuples
  - Best for fixed length data structures
  - Good for random access reads (value at specific position)
  - Awkward to change the board
- Lists
  - Reading and writing have same level of complexity (`get_in`, `put_in`, `Access` module)
  - Nesting is awkward (flat > deep data)
- Maps
  - Avoid deep data structure (nesting)
  - Tuples as keys! Best of both worlds
  - Easy reads and writes

Takeaways:

- Choose the best data structure for your primary access pattern (based on requirements)
- Flat data > deep data
  - Easy to pattern match against
  - Supports simpler algorithms (simpler code in general)

### Immutability Drives Everything

- Variables in Elixir are immutable
- Compiler provides the "illusion of mutability"

> Each function has its own bindings and they can’t be changed by another function, or another process. In the end, we have immutability.

#### New Facts Don’t Invalidate Old Facts

Think of data as "facts" or "assertions about the world"

> Object oriented data structures change over time. Functional data structures are maps of stable values over time.

#### Write Data Structures Functionally

#### Processes Are Not Data

- Don't build datatype with processes (example: bank account with `read_balance` and `write_balance` functions)
- Instead get values at point in time (starting point + transactions)
- Example Seems very similar to State Machine / [Event Sourcing](https://www.martinfowler.com/eaaDev/EventSourcing.html)
- More deterministic, less ambiguous

### Try It Out

#### Break Nouns Into Data Structures

Quiz project:  
- Quiz has templates
- Templates belong to categories
- Templates have questions
- Questions have user responses
- Track responses and generate questions until user has mastered template
- Mastery == 3 correct answers in a row

Data structures:  
- Quiz: Struct
  - :title, String
  - :mastery, Integer
  - :current_question, Question
  - :last_response, Response
  - :templates, List of Templates
  - :used, List of Templates
  - :mastered, List of Templates
  - :record, Map
- Template: Struct
  - :name, Atom
  - :category, Atom
  - :instruction, String
  - :raw, String
  - :compiled, Macro
  - :generators, List or Function (??)
  - :checker, Function
- Question: Struct
  - :asked, String
  - :template, Template
  - :substitutions, Map
- Response: Struct
  - :quiz_title, String
  - :template_name, Atom
  - :to, String (same as `Question#asked` (??))
  - :email, String (User#email)
  - :answer, String
  - :correct, Boolean
  - :timestamp, Time
- Category: String
- User: String (email address)

#### Quizzes Ask Questions

Business requirements / functionality seem very similar to [Hickory Training](https://www.hickorytraining.com/)

> The representation of our data will drive how we think about managing the quiz.

### Start With the Right Data

- Data structures impact complexity of your code
- Keep it simple, aka flat
- In FP, you're working with many versions of a value over time, not mutating a single value

## Questions/Talking Points

* (from last week) Functions as a data type?
* Immutability in Elixir: can someone explain?
* Thinking of FP data structures as values at a point in time
  * Any good examples of this from our own apps?
  * How does this relate to Event Sourcing? (maybe it doesn't?)
* "...when we built this application, we didn’t magically land on the perfect data structure. We made mistakes, refactored our data, refactored our functions and them made more mistakes." Would it have been helpful to see those mistakes and refactoring?
* Why are we storing raw and compiled versions of a Template on the Template struct?


<p class='util--hide'>View <a href='https://learn.co/lessons/chapter-3'>Chapter 3</a> on Learn.co and start learning to code for free.</p>
