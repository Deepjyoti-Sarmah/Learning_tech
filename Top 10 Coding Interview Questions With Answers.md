[youtuve video link](https://www.youtube.com/watch?v=8fG1FZXKT9U&list=TLPQMDQwNTIwMjPt_uSF-Ifllg&index=2) #jobtips #interview #interview_questions 
- ## Q) Difference between let/const/var
	- ways to create variables
	- const - constant variable
	- let and var - can be used and value can be changed
	- var - variable value can be use outside the scope 
	- let- varibale value cannot be changed outside the scope
	 <br> 
	- `let`, `const`, and `var` are used for declaring variables in JavaScript. However, there are some differences between them in terms of scope, hoisting, and re-assignment.

	-   `var`: The `var` keyword is used to declare a variable in JavaScript. It has a function-level scope, which means that a variable declared with `var` inside a function is not accessible outside that function. However, if a variable is declared with `var` outside a function, it is a global variable and can be accessed from anywhere in the code. The `var` declarations are hoisted, which means that the declaration is moved to the top of the scope. `var` allows re-assignment of the value.
	    
	-   `let`: The `let` keyword is also used to declare a variable, but it has a block-level scope, which means that a variable declared with `let` inside a block is not accessible outside that block. The `let` declaration is not hoisted, which means that it is not moved to the top of the scope. `let` allows re-assignment of the value.
	    
	-   `const`: The `const` keyword is used to declare a constant variable in JavaScript. It also has a block-level scope like `let`. However, unlike `let`, `const` variables cannot be re-assigned once they are declared. `const` declaration also isn't hoisted, which means that it is not moved to the top of the scope.
	    
	
		In summary, `var` has a function-level scope, `let` and `const` have a block-level scope, `var` declarations are hoisted, while `let` and `const` declarations are not hoisted. Additionally, `let` allows re-assignment of the value, whereas `const` does not.
	<br> <br>

- ## Q) is the code given below vaalid ? if yes, what property of js does it use?
	```
	x = 5; // Assign 5 to x
	eles = document.getElementById("demo"); //Find an element
	eles.innerHTML = x;
	
	var x; //Declared x
	```
	
	 - Yes this code is valid this uses a property called hoisting 
		 - the property says that even if you declare a variable at the end it get hoisted at the top 
	- but using let it cannot be done because of the scope it starts after it get initalized
	<br>
	- Yes, the code is valid. This code demonstrates the concept of variable hoisting in JavaScript.
	
		Even though the `var x` declaration appears after the assignment `x = 5`, the JavaScript interpreter moves the declaration to the top of the current scope (in this case, the global scope). This process is called hoisting, and it allows you to use a variable before it is declared.
		
		So, when the code is executed, the `var x` declaration is hoisted to the top of the scope, and then the value `5` is assigned to the variable `x`. Finally, the value of `x` is assigned to the `innerHTML` property of an HTML element with the id `demo`.
		
		It's worth noting that relying on hoisting can make your code harder to read and maintain. Therefore, it's generally recommended to declare your variables at the beginning of their scope to avoid confusion and potential bugs. 
	<br>
	- ### **what is hoisiting**
		- Hoisting is a default behavior of the JavaScript interpreter, in which the declarations of variables and functions are moved to the top of their respective scopes during the compilation phase of code execution.
	
			In other words, before executing any code, the JavaScript engine scans the entire code and moves the declarations of all variables and functions to the top of their respective scopes, regardless of where they were actually declared in the code.
			
			For example, if you declare a variable inside a function, the declaration of that variable will be moved to the top of the function's scope, even if the declaration appears later in the code. Similarly, function declarations are also hoisted to the top of their scope.
			
			It's important to note that hoisting only moves the declarations, not the assignments. So, if you declare a variable without assigning a value to it, its value will be `undefined` until you assign a value to it later in the code.
			
			While hoisting can be a convenient feature, it can also cause confusion and bugs if not used carefully. Therefore, it is recommended to always declare your variables and functions at the beginning of their respective scopes, to avoid any unexpected behavior.
	<br>
	<br>
- ## Q) is this fn correct or incorrect
	
	```
		const arr = [1,2,3]
		arr.forEach(function(val) {
			if (val%2 === 0){
				break;
			} 
			console.log(val);
		})
	```
	- forEach is not exactly a for loop
	- In any language usually when writing a for we can break through the for loop if certain conditions are met 
	- but the argument here is a function and is not valid inside  a fun, it is only valid inside a loop
	- to do so we can do it like
		
	```
		const arr = [1,2,3]
		let done = false;
		arr.forEach(function(val) {
			if (val%2 === 0){
				done = true;
			} 
			if (!done){
				console.log(val);
				
			}
		})
	
	```
	- or
	```
		for(let i = 0; i< arr.length; i++) {
			if (arr[i]%2 === 0) {
				break;
			}
			console.log(val);
		}
	```
	- This function is incorrect because the `break` statement cannot be used inside a function passed to the `forEach` method.
		
		The `forEach` method is used to iterate over an array and execute a provided function on each element of the array. The provided function can accept three arguments: the current element, the index of the current element, and the array itself.
		
		However, the `break` statement is used to exit a loop prematurely, such as a `for` or `while` loop. It cannot be used to exit a function or a `forEach` loop.
		
		If you want to terminate the `forEach` loop based on a condition, you can use the `return` statement instead. For example, you can modify the function as follows to log only the odd numbers in the array:
	
	```
	const arr = [1, 2, 3];
	arr.forEach(function(val) {
	    if (val % 2 === 0) {
	        return;
	    }
	    console.log(val);
	});
	```
	<br><br>
- ## Q) is javascript single threaded ? can your browser only run a single thread ?
	-  Yes, javasript is single threaded , but we can spawn out other proceses from it , but javascript is running in single thread
	- If your machine is single thread or multithread javascript will perfirm the same unless other process are running
	- microsoft multithred js
	- multiple instance of same node js process are runned
	- In browsers there are ways to spawn more threads and delegate the processes to **web workers** 
	- like video processing like background detection in google meet 
	<br>
	- JavaScript is mostly single-threaded, which means that it runs on a single call stack and processes one piece of code at a time. This is often referred to as the "event loop" model, where JavaScript code runs in response to events triggered by user actions, timer events, or other asynchronous events.
	- However, modern browsers provide support for running JavaScript code in multiple threads using **web workers**. ***A web worker is a separate JavaScript file that can be executed in a separate thread, allowing heavy computations to be performed without blocking the UI thread.***
	- Web workers are designed to run scripts in a separate thread, which means that they can run in parallel with the main JavaScript thread, providing a way to execute CPU-intensive tasks without blocking the UI thread or slowing down the performance of the web page.
		
	<br><br>
- ## Q) What language does a browser understand
	- Could understand html , css, javascript along it can now understand webAssembly (runs assembly code inside a browser) -- language like c/c++, rust can be converted into assembly language and run into browser
	- eg FFMPeg (video processing libarary ) VLCPlayer build on top of it . Not written in javascript but now runs in browser/web worker
		- website where you put youtube video and it downloads it for you 
		- all the processing is done inside the browser
		<br>
	- What is **WebAssembly**
		- WebAssembly is a low-level programming language that is designed to be portable and platform-independent. It can be used to create software modules that can be executed in a variety of environments, including browsers, servers, and standalone applications.
		- One example of a software application that uses WebAssembly is Figma, a browser-based design and prototyping tool. Figma uses WebAssembly to run a native C++ engine that performs complex design tasks, such as rendering vector graphics and handling complex animations.
		- Another example is the Unity game engine, which has a WebAssembly runtime that allows games developed using Unity to be run directly in a browser without the need for plugins or downloads. The WebAssembly runtime in Unity provides near-native performance, enabling developers to create complex and immersive games that can be played directly in a browser.
		Overall, WebAssembly is a versatile technology that can be used in many different software applications to improve performance, portability, and security
	<br><br>
- ## Q) What are middlewares in javascript
	- also known as extractors
	- used accross languages
	- preprocess a request that come to your server
	```
		app.get("/project", auth, admin, (req, res) => {
			db.update("project", req.title)
		})
		const auths = (req, res) => {
			const coocie = req.cookie;
			const userName = check(cookie)
			if (userName) {
				return true
			}
			return false
		}
		const admin = (req, res) => {
			const isAdmin = isAdmin(req.userName)
			if(isAdmin) {
				return true
			}
			return false
		}
	```
	-  In web development, middleware is a concept that refers to a software layer that sits between different components of an application and enables communication between them. It acts as a bridge, connecting different systems, applications, or services together and facilitating the exchange of data or messages.
		- Middlewares are commonly used in web frameworks and libraries, such as Express, to add additional functionality to a web application, such as authentication, logging, error handling, and more. A middleware function is a function that sits between a web application's request and response objects and performs some specific task. It intercepts the request and modifies or enhances the response before it is returned to the client.
			- For example, a middleware function can be used to authenticate users before allowing them to access certain parts of the application. This can be done by checking the user's credentials, such as their username and password, and verifying that they are authorized to access the requested resource. Another example of middleware is logging, which involves recording information about each request and response to help with debugging and performance analysis.
	- Overall, middleware is an important concept in web development as it enables different components of an application to work together seamlessly and efficiently.
	- Let's say we have a web application built using Node.js and the Express framework. The application allows users to view and post messages to a public message board. However, we want to add authentication to the application to prevent unauthorized users from posting messages.
	- To implement authentication, we can use a middleware function that checks if the user is authenticated before allowing them to post a message. Here's an example of what the middleware function might look like

	```
		function authMiddleware(req, res, next) {
		  // Check if the user is authenticated
		  if (req.session && req.session.authenticated) {
		    // User is authenticated, continue to next middleware
			next();
		  } else {
		    // User is not authenticated, redirect to login page
		    res.redirect('/login');
		  }
		}
	```
	<br><br>
- ## Q) Have you written backend systems in your previous jobs? How did they talk to each other? Were they synchronous or asynchronous
	- ###  Tell your experience in the interview <br>
	- In a backend system, various components often need to communicate with each other to perform tasks and exchange data. The communication between these components can be synchronous or asynchronous, depending on the specific requirements of the application.

	- Synchronous communication means that each component waits for a response from the other component before proceeding. For example, if one component needs to make a request to another component to perform a task, it will wait for the response before continuing. This type of communication can be useful in situations where timing is critical, and each component needs to know the status of the other component before proceeding.
		
	- Asynchronous communication means that components can communicate with each other without waiting for a response. For example, if one component needs to perform a long-running task, it can initiate the task and continue with other work while the task is running. This type of communication can be useful in situations where components need to work independently and not block each other.
		
	- In modern backend systems, asynchronous communication is becoming more common, as it allows for more scalability and responsiveness. Asynchronous communication can be achieved through various mechanisms, such as message queues, event-driven architectures, and reactive programming paradigms.
		
	- Overall, the choice of synchronous or asynchronous communication between components in a backend system depends on the specific requirements and constraints of the application.
	<br><br>
- ## Q) Have you ever contranerise apps ? Do you understand docker? Can you explain it in brief? #devops #docker  [[2023-05-06#^d42829]]
	- Backend (Rust, Go, NodeJs) --> Compiled to binary (in case of JS in bundle of Js) --> Run anywhere on a Machine(AWS, GCP) 
	- Code --> Github --> AWS --> Runs there
	- Problem is we might need bunch of frameworks 
		- like need nodejs installed for npm, nvm but machine in cloud are basic ubuntu machine with no dependencies 
	- What if you can define a machine 
		- I want a very small part of the ubuntu machine
		- my app needs nodejs , npm 
		- hence give me a very small machine which have npm installed , node installed and my code which can and have secrect environment variables and thats it
	- what if you can write all this down into a spec into a file and create images which effectively are like ISO files
		- like mini machine that runs inside your main machine 
		- has all the dependicies we need
	- Usefull because no need to install nojeJs in every async machine 
	- Just tell that machine run this docker container 
	- That docker container (small image) has all your dependencies
	 <br>
	- Docker is a platform that enables developers to easily build, deploy, and run applications in containers. **A container is a lightweight, standalone executable package of software that includes everything needed to run an application, including code, libraries, and system tools. Containers allow applications to run consistently across different environments, such as development, testing, and production, without requiring any changes to the underlying infrastructure.**
	- Docker provides a containerization engine that can create and manage containers, as well as a container registry that stores container images. Developers can use Docker to build container images that encapsulate their applications and all of their dependencies, including operating system components and runtime libraries. They can then deploy these container images to any environment that supports Docker, such as a cloud-based platform like Amazon Web Services or Microsoft Azure, or an on-premises server.
	- One of the key benefits of Docker is that it enables developers to easily package their applications and all of their dependencies into a single container image, which can then be shared and run on any machine that supports Docker. This makes it easier to manage dependencies and ensures that applications run consistently across different environments.
	- In summary, Docker is a platform that provides developers with an easy way to build, deploy, and run applications in containers. Containers enable applications to run consistently across different environments and can help simplify the management of dependencies and infrastructure.
	<br><br>
- ## Q) What is state in react ? How it  is different from the main DOM ?
	- State variables are variables that react runtime sort of looking at and making sure anytime state variable is changes it rerender the  components that have now changed
	<br>
	-  In React, "state" refers to an object that contains data that is used by a component to render its output. It represents the current state of the component and can be updated by the component itself or by its parent component.
	- State is a fundamental concept in React, as it enables components to manage their own data and respond to user interactions. When the state of a component changes, React automatically re-renders the component and updates the output to reflect the new state.
	- Here's an example of how state works in React:
		```
		import React, { useState } from 'react';

		function Counter() {
		  // Define a state variable called count, initialized to 0
		  const [count, setCount] = useState(0);

		  // Define a function to handle button click events
		  function handleClick() {
		    // Update the state variable count by incrementing it by 1
			setCount(count + 1);
		  }

		  // Render the component output, using the current value of count
		  return (
		    <div>
		      <p>You clicked {count} times</p>
		      <button onClick={handleClick}>Click me</button>
		    </div>
		  );
		}

		```
	- In this example, the `useState` hook is used to define a state variable called `count`, which is initialized to 0. The `handleClick` function is defined to update the `count` state variable when the button is clicked, and the current value of `count` is displayed in the component output using the JSX syntax.
	- Overall, state is an essential part of building interactive and dynamic user interfaces in React, as it allows components to manage their own data and respond to user interactions in real-time.	
		[youtube](https://www.youtube.com/watch?v=569YZm0X5-0)
	<br><br>
- ## Q) What is a Virtual DOM ? How it is different from the main DOM ?
	- #### What is virtual DOM ?
		- In web development, the DOM (Document Object Model) is a tree-like structure that represents the HTML code of a web page. Each node in the DOM tree represents an HTML element, and it can have child nodes that represent its nested elements.
		- The Virtual DOM is an abstract, lightweight copy of the actual DOM tree that is created and maintained by React (a popular JavaScript library for building user interfaces). Whenever there is a change in the state of a React component, a new Virtual DOM is created to represent the updated UI.
		- The Virtual DOM is called "virtual" because it is not the actual DOM that is displayed in the browser window, but rather a copy of it that React uses to compare with the previous version. By comparing the previous and current versions of the Virtual DOM, React can identify the differences (or "diffs") between the two versions and determine the minimal set of changes that need to be made to update the actual DOM.
		- The benefits of using the Virtual DOM are twofold. First, because the Virtual DOM is a lightweight copy of the actual DOM, it can be manipulated much more quickly and efficiently than the actual DOM. Second, by only updating the necessary parts of the DOM, React can minimize the number of changes that need to be made, resulting in faster and more efficient updates.
		- Overall, the Virtual DOM is a key concept in React that enables efficient updating of the UI and contributes to the performance of React applications.
	- ####  How virtual Dom works ?
		1.  Whenever there is a change in the state of a React component (for example, when a user clicks a button), React creates a new Virtual DOM that represents the updated UI.
		2.  React then compares the new Virtual DOM with the previous Virtual DOM to identify the differences between the two.
		3.  Specifically, React looks for nodes in the new Virtual DOM that are different from the nodes in the previous Virtual DOM, and marks those nodes as "dirty".
		4.  React then computes the minimal set of changes (or "diffs") needed to update the actual DOM based on the "dirty" nodes in the Virtual DOM.
		5.  Finally, React applies those changes to the actual DOM, updating the UI on the screen
	- By using the Virtual DOM to compare and update the UI, React can perform updates much more efficiently than if it were to directly manipulate the actual DOM. This is because the Virtual DOM is an abstract representation of the UI that can be manipulated much more quickly and easily than the actual DOM, which involves rendering and reflowing elements on the screen.
	- Furthermore, because React only updates the necessary parts of the UI based on the diffs in the Virtual DOM, it can minimize the number of changes that need to be made and reduce the amount of work the browser has to do. This makes React applications faster and more efficient than traditional web applications. 
	- ####  What is DOM ?
		- he Document Object Model, or DOM for short, is a programming interface for web documents. It represents a hierarchical structure of HTML or XML elements in a web page, and defines a standard way for programs to access and manipulate these elements.
		- In simpler terms, when a web page is loaded in a browser, the browser creates a DOM tree based on the HTML code of the web page. The DOM tree is a hierarchical structure that represents each element in the web page as a node in the tree. For example, the HTML `<body>` element would be represented as a node in the DOM tree, with child nodes representing any nested elements inside the `<body>`.
		- Developers can use various programming languages, including JavaScript, to access and manipulate the DOM tree, allowing them to change the content and appearance of a web page dynamically based on user interactions or other events. For example, a JavaScript function could be used to update the text of a heading element in response to a button click, by accessing and modifying the appropriate node in the DOM tree.
		- Overall, the DOM is a crucial part of web development, as it enables dynamic, interactive web pages that can respond to user input and other events.
	- #### How Virtual DOM is different from the main DOM ?
		1.  Performance: The Virtual DOM is generally faster than the main DOM because it updates the minimum number of nodes required to reflect the changes. The main DOM, on the other hand, has to update every node, which can be a slow process, especially for complex web pages
		2.  Manipulation: The Virtual DOM is an abstraction of the main DOM, meaning that it is not directly tied to the browser's rendering engine. This allows developers to manipulate the Virtual DOM more efficiently than the main DOM, which has to render elements on the screen.
		3.  Rendering: The Virtual DOM is not rendered on the screen, while the main DOM is. The Virtual DOM is an in-memory representation of the state of the UI, which is used to compute the minimal set of changes required to update the actual DOM.
		4.  Synchronization: The Virtual DOM is always in sync with the state of the UI, while the main DOM may not be. This is because the main DOM can be manipulated directly by JavaScript, while the Virtual DOM is only updated by React components.
		<br><br>
	
- ## Q)  Project based questions -
	- if the company is building , lets say a game, they'll ask you to write a test to


[[Job Interview Tips I Learned After I Became The Interviewer]]