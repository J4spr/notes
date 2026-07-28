# Programming Patterns in Java: Course Summary

## 1. JavaFX Fundamentals
* **Concept**: JavaFX is a framework for building desktop applications with a Graphical User Interface (GUI) .
* **Architecture**: It uses a theater metaphor where a `Stage` (the window) contains a `Scene`, which is constructed using a `Scenegraph` made up of individual `Nodes` .
* **Nodes**: Nodes can be UI `Controls` (like Button, Label, TextField, ComboBox) or layout `Panes` (like BorderPane, VBox, HBox, GridPane) .

## 2. Events & The Observer Pattern
* **Events**: Actions such as mouse clicks (`MouseEvent`), button presses (`ActionEvent`), or typing (`KeyEvent`) trigger events .
* **Event Handlers**: These are classes or lambda functions that implement the action to be taken when a specific event occurs .
* **Observer Pattern**: This design pattern allows components (observers) to automatically listen and react to state changes in observables without tight coupling . JavaFX heavily relies on this pattern for its internal event handling .

## 3. Model-View-Presenter (MVP) Architecture
MVP is a design pattern that separates the application into three layers to keep GUI and business logic strictly independent .
* **Model**: Contains all the business logic, data, and calculations . It must be completely independent of the GUI, meaning absolutely no JavaFX code or imports are allowed in Model classes .
* **View**: Contains the UI code and layout . It contains no business logic and no event handlers . UI controls are exposed to the Presenter via package-private getters .
* **Presenter**: Acts as the intermediary linking the Model and View . It initializes event handlers, reacts to user interactions, executes Model methods, and refreshes the View with new data .
* **Handling Multiple Screens**: Screen navigation is handled by Presenters . To switch screens on the same window, the Presenter replaces the root of the current `Scene` . For pop-ups or entirely new windows, the Presenter creates a new `Stage` .
* **Common Mistakes**: Common MVP pitfalls include placing business logic in Views or Presenters, directly printing error stack traces to the console instead of using JavaFX Alerts, and failing to use private encapsulation for variables .

## 4. Exception Handling
* **Types of Exceptions**: 
  * *Unchecked Exceptions* (e.g., `RuntimeException`, `NullPointerException`) represent bugs and will crash the application if not caught .
  * *Checked Exceptions* (e.g., `IOException`, `SQLException`) must be explicitly caught or declared in the method signature .
* **Try-Catch-Finally**: Exceptions are handled using `try-catch-finally` blocks, where the `finally` block will always execute to clean up resources, regardless of whether an error occurred .
* **Exceptions in MVP**: In the MVP architecture, exceptions should be thrown by the Model and gracefully caught by the Presenter . The Presenter should then notify the user using a visual UI `Alert` rather than outputting raw errors to the console .

## 5. Databases: JDBC and DAO
* **JDBC (Java DataBase Connectivity)**: A framework used for connecting Java applications to SQL databases, such as PostgreSQL or HSQLDB .
* **JDBC Workflow**: The standard database workflow involves loading the database driver, establishing a `Connection`, creating a `Statement`, executing the query, processing the returning `ResultSet`, and safely closing the connection .
* **DAO (Data Access Object) Pattern**: This pattern centralizes all database access into specific DAO classes . This prevents raw SQL queries from scattering throughout the application and keeps the business logic layer clean .
* **ORM (Object Relational Mapping)**: Used alongside DAO to smoothly map relational database records into Java Transfer Objects .