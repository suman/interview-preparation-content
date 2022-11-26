Explored the following topics for solution architect interview

Note: I made notes and did code pratices during the prepartion for interview of solution architect, these info might be perfectly articulated, if you found any errors and want to give any suggestion please ping at sumanbogati@gmail.com

# ES6 Features

- Spread Operator
- Destructring 
- Promise
- Rest operator
- String template
- IIFE (immidiately invoked function expression)
- Named export and default export
- Bbubling and caputrig the event
- Babel
- Difference between const and Object.freeze()
- Webpack


# Interesting factor in JavaScript

### Hositing:

When JavaScript engine starts to execute code, it creates global execution context. It has two phase:
Creation
Execution
During Creation, the javascript engine moves the variable and function declaration towards the top, for example:

```
Const age = 30;
var name = “raj”

This above code equivalent to this:
var name;
const age = 30;
name = “raj”
```

When the engine moves the variable declaration towards the top, it’s called variable hoisting.

Similar thing is applied with the function declaration.

### Clousre

When we create the one function into another function, then the inner function is called closure. We all know that in javascript, inner function can access the variable of outer function. But what interesting part with the closure is, even after invoking the outer function, the inner function can access the variable of outer function. Let’s understand this with the example.

For example we have the outer function called parent
```
function parent()  {
  let fatherName = “shyam”;
  console.log(“triggered outer function”)

  return function child() {
    let child = “raj” 
    console.log(“father ”, fatherName, “child”, child)
  }
}

const parentObj = parent();

parentObj();
```
### Event Loop

 JavaScript is single thread language with asynchronous behaviour. Let’s understand the event loop with the example. Here we have three line of codes

``` 
console.log(“hello Sachin”)
getApiCall((response) => {
	console.log(“data received”)
})

console.log(“Dhoni”)
```
While JavaScript  executes the code, it involves some process, for example,

- Stack
- Event Loop
- Task Queue

When the engine starts to create the above code, it puts the first console inside the callStack, so first console does not have any async behaviour such as network, data from db and etc, so it’s executed and returnt  the vlaue to the caller and finally remove the console sachin from the stack.

Now when it goes to line number second, the engine puts the second line  getApiCall into stack which has the network call, which means it has asyncronous behaviour, we don’t know how much time it will take to complete this network request, so the engine remove this code from stack and again goes back to 3rd line of code, which has console dhoni, and put this line into the stack and executed it. As of now the stack does not have anything to executed meanwhile let say the network request is completed and the call back funciton would be stored into the task queue with the response. Now the event loop checks that if callstack is empty then it just fetches callback function from task queue and put  i nto th stack and finally response back to the original caller.

#### Event loo diagram
![Eventloop](https://raw.githubusercontent.com/suman/interview-preparation-content/solution-architect/Event-loop.jpg)



#### Reources
- https://medium.com/@mandeepkaur1/what-is-a-closure-in-javascript-53be508abfd3
- https://www.javascripttutorial.net/javascript-hoisting/
- https://www.interviewbit.com/es6-interview-questions/

# React

### Why React
	React is very popular and we can get good documentation of it and widely supported by community. You can make the application quickly in react.js. There are lot of open source modules that are supported in to react.js. React.js is sclable and it is best option when the application needs to be interactive. You can make faster application in react.js because it supports virtual dom. React.js with the next.js make top seo react application on google.

### Virtual DOM
When your application needs to be interactive, we need to do DOM manipulation. If you don’t do your DOM manipulation in correct way, there might be chances that your appliaiton might be slower. Reat.js cleverly works on dom part, whenever we changes for dom, react.js does the manipulation and update it into memory, and do only final update to the real dom when there is the best time to do it.

### Context Api

In react, we can pass the data from parent to child using props.  But when you have good amount of nested component hierarchy then it’s difficult to maintain the props from parent to younguest child. In this case, if you need change at one place, you have to change in all components. It’s also called props drilling.

To handle the situation, we can use the context api. So the context api is basically used to share the common data at any components directly.

For example let’s say we have the component hierarchy something like this,

```Dashboard -> main nav -> Top nav
			     	             -> Side nav 
```

Now let’s say we need the data user name, on dashboard and top nav component. One way to do it like we can pass the data through props, but if you have the long hierarchy of nested component, then, there would be the problem of props drilling. In that case we can use the context api. We got the user name on dashboard component, now through the provider we can pass the data from dashboard. Now we can get this user name directly on top nav component using useContext. So there is no any sync with main nav.
	

# Redux

Redux is used to share  the global data across the compoents. When your application becomes large, in that case, it’s hard to main the state for different components. Here would come the role of Redux. Following are the scenarios where the Redux is needed in application.
When the application is large
In application, the state is frequently changed
When we need to share common state over the various components

** Redux Diagram

![React-diagram](https://raw.githubusercontent.com/suman/interview-preparation-content/solution-architect/Redux.jpg)

### Followings are the terms that used for Redux.

- Action: It’s similar to the event, like what kind of event is this, like, mousedown and etc. It has also the payload.
- Reducer: It similar to the event handler. Reducer will receive the action when it’s been dispatched to it. Now it’s update the state and send it to the store.
- Store: It saves the current state of data. Once it’s updated. The binder state on ui will receive that data.
- State: When the state is updated the binder of UI will be re-rendered.

### Context Api Vs Redux


| Context Api  | Redux |
| ------------- | ------------- |
| Does not change the size of final building  | Influence the bundle size  |
| Additional installation is not required  | Additional installation required  |
| Designed for static data that is not frequently changed  | Works for both static and dynamic data  |
| Debbugging can be hard  | Debugging is easy with the tool  |
| Is for small project  | Content Cell  |
| Easy to learn  | Difficult to learn  |
| Suits for nested components and  handles prop drilling | Suits for the state management for large project and frequent state changes |

Redux

# React Life Cycle

React applicaiton is made through the collection of components and every react component has a life cycle. These life cycle can be categorized into following stages.

- Initialize
- Mounting
- Updating
- Unmounting

**Initialize** is the starting process, inside which the default value of state would be set. The is happened in class component when the constructor would be invoked. In short, in this stage, the initial value of the state would be assigned.

**Mounting** is the process throgh which, the component will be mounted into the dom. It has following stages:
ComponentWillMount: this funcion is invoked before the render method, which means it is invoked before the component is mounted into the DOM.

  - **Render** It basically mounts the component into the DOM.

  - **CompenntDidMount** It is invoked right after the component is mounted on the Dom.
  
**Updating** In this stage, the state wil be updated throguh the user interactivity and re-painted the component. It has following steps.
  - **ComponentWillReceveProps** we will receive the coming props, or we can say in this method we can get the to be updating state. 
  - **setState** In this method, the updated value will be set into the related state.
  - **ShouldComponentUpdate** Most of the time,  in updating cycle the component will be re-rendered. But there are some time we don’t need to do this, in this case we can return the false from this function
  - **Mounting** This cycle is same as Mounting as mentioned above


**React lifecycle diagram**

![React-life-cycle-dygram](https://raw.githubusercontent.com/suman/interview-preparation-content/solution-architect/React-life-cycle.jpg)

### React Hooks

React hooks are introduced in react 16.8. It lets you to use the react feature without using class. There are various react hooks we can find.

- **useState** is used to maintain the state on react component
- **useEffect** we can do some work through the call back passed into useEffect, this useEffect will be triggered after the specific condition met. For eg: let’s say  callback renders the users into table when it received the user list from api requested, so the dependency would be user list, and the action would be that callback
- **useRef** When we want to access dom directly for some manipulation, we attach the reference for that particular dom, and we can access this dom. Eg; we will focus the input
- **useCallback** is used increase the performance of component.
- **useMemo** is similar to callback but improves by caching the data from incentive cpu task.
- **useContext** is used to handle the props drilling, basically it’s used share the state
- **useReducer** is also used to share common data over the component using redux.

### Resource
- https://www.smashingmagazine.com/2020/06/higher-order-components-react/
- https://blog.logrocket.com/react-context-api-deep-dive-examples/
- https://redux.js.org/tutorials/essentials/part-1-overview-concepts
- https://redux.js.org/tutorials/quick-start
- https://www.geeksforgeeks.org/reactjs-lifecycle-components/
- https://www.freecodecamp.org/news/introduction-to-react-hooks/
- https://www.freecodecamp.org/news/react-hooks-cheatsheet/

# NodeJs

### What is nodejs and why we use it ?

Nodejs is a cross platform runtime environment. Ryan created nodejs into 2009 to execute the JavaScript outside the browser. Nodejs is used to create the application such as: network applications, gaming application, real time applications and i/o applications. 

Node js has asynchronous behavour, because of which we can create the scalable application, like if we want to creat the gaming application then there might be possible there are lot of con-current users, with the asynchros behaviour, the gaming application can be scaled. It’s also fast because it uses the V8 engine to execute the JavaScript, the V8 is created by Google chrome to improve the javascript performance.


### Thread pool

NoodeJs is known for single thread and asynchronous behaviour. NodeJs made of JavaScript and C++. When the aynchrnous request happened in the nodejs, C++(libuv) will request this to the Kernal or Thread pool. The request like network go to the kernel, and the request that can not be performed by the kernel (OS) will go to the thread pool, such as File read/write request, cpu intensive task and etc.

Thread pool is like a separate thread, there are 4 threads we can get by default on nodejs and it can be scaled upto 6 threads.

How multi thread can be created
 	We can create the multiple threads to transfer the cpu insensitive task to another thread that can be done using worker-threads. Using this module we can free main thread whale performing CPU i Insensitive task.

### What are the projects I have done?

I have few experience on nodejs, like. In aws (cloud), I worked on lambda, there let’s say I need to understand the api request and perform the required action accordingly, suppose we want to fetch some data using dynamo db. I got the request on lambda function, lambda function is nothing but nodejs environment, where I need to write Nodejs code for different tasks. In this scenario, I need to fetch the data from the database. Or there might some other request like I need to connect user’s request to s3 or SQS, then I write the code on the nodejs acccoridngly. This is one kind of  nodejs environment I have worked on and,  other like, I worked on nodejs to create the server for realtime application, like I create the server for the chat and whiteboard. I create the server on nodejs using webcoket, I mentioned the webocket port there on the server, through this port there will be the connection between client and server. This connection will be persist until some one is closed, and over this connection we can just exchange the data between server and client using webocket’s inbuilt methods like websocket on message, web socket send message. Let’s say server is the central thing for all client, It can broadcast the message to all client at a single request or it can send the message to particular client only. This is the another kind of work I have done on nodejs.

### The NodeJs request/respone and thread
![Nodejs-architecture](https://raw.githubusercontent.com/suman/interview-preparation-content/solution-architect/node-js-fast.jpg)

### Resource
- https://medium.com/@r_joydip/how-does-thread-pool-work-in-node-js-c48f3b3662a9
- https://www.youtube.com/watch?v=zphcsoSJMvM
- https://kariera.future-processing.pl/blog/on-problems-with-threads-in-node-js/
- https://github.com/ably-labs/websockets-cursor-sharing
- https://ably.com/blog/web-app-websockets-nodejs

# Typescript

[Very simple and incomplete Todo Applicaiton](https://suman.github.io/react-typescript-todo/) with React and TypeScript and you can found the source code [here](https://github.com/suman/react-typescript-todo)

JavaScript is dynamic typed language, which means JavaScript interpreter puts the type of value when executing/reading the code. When you run the javascript application in browser/other platform, then we see the result and came to know if there is any syntax, compilation or any other errors.
This is one shortcoming and other is like, JavaScript at earlier stage did not support the class, inhertiance, interface kind of keyword and mechanism in the language. To achieve the object oriented thing in programming language was difficult task, it became even worse when people came from other programing lanugages. 

Because of those shortcomings, it is difficult to create and maintain huge and complex application in JavaScript. Microsoft created the TypeScript to solve the issues. TypeScrilpt is nothing but the JavaScript and addtional features. You can categorize the typescript in following,

#### Strong Typed Language 
JavaScript is dynamic typed language whereas typescript is strongly typed language. You have to define the type of every variable, object, array, and the member of class which are used in the application. You have to define the the data such as string, number is being returned by particular function. 
So by doing this, we solve many errors such as syntax and etc when the typescript is being compiled to javascript. So we can get error at earlier stages, which saves good amount of time of everyone.

#### Compiled Language

Typescript is portable, it can be run on browser, nodejs, and operating system. Typescript is supported there where the javascript is supported. After compilation all the typescript code would be converted into JavaScript code.

### Object oriented language
Earlier version of javascript did not support the keyword such as Class, Interface and Inhertiance, so it was difficult task to implement the Object ortiented on large application. Typescript supported thse keywords in language from the beginning of its launch.

Typescript Simple Syntax Practice
```
// defined array type
const cars:string [] = ['bmw', 'hello', 'tata'];

// defined string type
const car:string = 'bmw';

// defined single number 
const year:number = 12;

// defined array number
const years:number [] = [3, 5, 12, 90];

// defined object type
const person:{
    name: string;
    occupation: string;
} = {
    name: 'suman',
    occupation: 'developer'
}

// defined array of object
const persons:{
    name: string;
    age: number;
}[] = [
    {
        name: 'raj',
        age: 30,
    },
    {
        name: 'mukesh',
        age: 19,
    },
    {
        name: 'raj',
        age: 20,
    },
];

// defined type of argument and returned value
const square = function (num:number):number {
    return num * 2;
}

// defined type of argument and returned value
const getName = function (name: 'string', age: number):string {
    return `${name }'s age is ${age}`;
}

// defined array type with 
const getNameArrow = (age:number):string => {
    return `age is $age`;
}

// defined type of argument and returned value
const getTotalCharactersLength = (word: string, word2:string):number => {
    return word.length + word.length;
}

// defined and use the interface
interface Car {
    name: string;
    price: number;
}

//destructre the object
function getPerson({name, age} : {name: string, age:number}) {
    console.log(name)
    console.log(age)
    return name;
}

//destructre the object using interface
interface Person {
    name: string,
    age: number,
}

function getPersonInterface({name, age} : Person) {
    console.log(name)
    console.log(age)
    return name;
}

// class declaration
class Employee {
    name: string;
    age: number;

    constructor(name:string, age: number) {
        this.name = name;
        this.age = age;
    }

    getName () : string{
        return this.name;
    }
}

// define arrow function with returning the number
const getNameArrowSecond =  (name: 'string', age: number):string => {
    return `${name }'s age is ${age}`;
}

// destructre the object
const getPersonArrow = ({name, age} : {name: string, age:number}):string => {
    console.log(name)
    console.log(age)
    return name;
}

// define optional parameter 
const getPersonNameOpetional = (name:string, age?:number):string => {
    return name;
}
```

# Graphql

Graphql is the query language for the API. It’s not same as RESTful apis, with the Graphql query you will fetch what you required. We mentioned what kind of data might be read/write on schema, if our query will fall under this schema then our query will be performed.

### The benefit of Grapqhl

We can fetch the only required data so it’s a client specific
We can fetch lot of data in one request so no need of multiple request as in REST ful apis.
The data type validation does not need to do, the graphql itself suggest that what kind of data we need to pass.
We might not need to maintain the version as we can mention any field as deprecated, and can be remove at later which does not affect any current field. 

These are might be the drawback for graphql
Cache can be the problem
It’s might not be suitable for the small application.

# Cloud computing

Under the cloud computing you can get the hardware, resources, software as a service. It won’t be the physical but you can get those kind of things on the internet. In cloud computing, as you need you have to pay for the service, you don’t need to hold the service when it’s not needed. In traditionally, we have to pay for the service for the fixed time, it does not matter whether we need it or not. 
There are few categories under the cloud computing.

### IAAS (Infrastructure as a service)
Under this category, you will get the hardware only, you have to maintain the operating system on it, you have to maintain the backup, failure, recover, security and many more. 
	    Like AWS’s EC2 is the best example of it, we can will get hardware, now we can use this hardware anyway we want.	
### PAAS (Platform as a service)
Platform as a service, we will get the platform according to this category. We don't have to worry about the hardware and operating system of it. We can make the application or software on it. In this category, we have to maintain the software.

### SAAS (Software as a service)
Under this category, we will get the service as services, eg office 365, Gmail and etc. For this service we have to pay as per our need. In this category, we don't worry about the maintenance of software or application.


### AWS Api Gateway:
It is used to create the RESTful and websocket apis on aws. API gateway supports various methods POST, GET, UPDATE, DELETE, PATCH. The cloudfront and edge location make these api areally scalable. It’s kind of front door to access many other AWS services. The flow of AWS api would be like.

Client request -> api gateway -> aws services (such as lambda) -> perform the action and send response back to the client.

### DyanamoDb
Dynamodb is nosql database service which is provided by AWS. When you require the the response in millisecond, when your traffic is not stable, when you need the storage in terabyte, when you don’t want to manage the database service then you can choose the Dynamodb. It’s scalable, up all the time, easy to use. It can be used to store the meta data of video stream service, it can be used store the data of application
It has primary and sorting key. By using the combination of this, you can get maximum data  in one query.

### Resources
https://aws.amazon.com/blogs/database/how-to-determine-if-amazon-dynamodb-is-appropriate-for-your-needs-and-then-plan-your-migration/

Github actions and workflow
# CI/CD
CI/CD stands for continues integration and continues deliver, every software goes through the different cycles till it reaches to the end customer. When the requirement is finialized, the development of software would be started and this phase, other stakeholders might be interested on followings points
- are the features on the way as client want
- are the securities being validated
- does software run on cloned of real enviroment Here comes the role of CI/CD.
- there are no any conflict just before major relases
- how the software will be accessible to different stakeholders during the development

To answers these kind of questions CI/CD plays the important role.

Let's understand the process from develpment to till release cycle. Once the development process is started it has different cycles, CI/CD makes those development relases are seamless. Once this release is done, other developver can provide the feedback, if there is any conflict between the code of different developers that can be merged. Now CI/CD makes the QA release and the developed features can be tested by QA team. QA team will test the features and raise the bugs which will be fixed by developers. After regression testing and bug fixed, now it's time CI/CD for production release.

After production release, the client evaluate the developed feature can provide the valuable feedback to developer partner. This is how CI/CD plays important role sucessfull prodoct development and delivery.

Following task can be categoriised under CI and CD

#### Under the CI
- Developer conintuesly push the changes into the main repository. By doing so it’s visible to other developers, they can provide the feedback. Continue integration of code into the main repo also reduce the chance of conflicting the code
- The code qaulity can be analysied and tested
- The bundling of software is done here

#### Under the CD
- Another round of testing can be performed
- Securities check can be done 
- Provisioning the clone environment of real environment and run the application on it
- Build the different software releases


### What is action and workflows in to github ?

Actions in github helps to automate your development and releases cycles. The tasks defined above **Under the CI/CD** title can be automated through github actions.

We can create the action file in folder .github/workflow/actionFileName in your project folder. In ths file we can define various jobs and on each job we can define the different steps, for example, below steps of action file, we are instructing that install node modules, set the orgin and finally deploy the bundled code.

```
 run: npm install
 run: git remote set-url origin https://suman:${{ secrets.GITHUB_TOKEN }}@github.com/suman/react-typescript-todo
 run: npm run deploy
```

The github action file can be linked to particaulr github event. Like we can link the above steps to the gihub push event of master branch, which means if someone does the push on the master branch then the product deploy action would be performed automatically. 

Here’s the automate of testing, building and realesing can be done by action file but these are not only things we can do, the other interesting stuff like you can send the email when the pull request comes up on repo, you can assign the ticket to particular person when some tickets will be raised by customers, so these kind of actions can go on.

### Resources
- https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions
- https://assets.ctfassets.net/wfutmusr1t3h/6IyfnYAidl3QUoX2xfGOgI/6aa9e5df02378f952f7c1ba5f42effc9/What-is-GitHub.Actions_.Benefits-and-examples.pdf
- https://about.gitlab.com/topics/ci-cd/


# Rest Apis vs XML Rpc vs Soap Apis

### The REST apis

- Stateless : No need of sync between client and server, server does not need to store any information about client.
- Scalability : The request and response between the client and server are both individual, so we can achieve the scalability here.
- Cacheable: As there is no state between server and client, we can cache the response from the server.
- Rest is suitable better for the CRUD operation
- Layering: We can send reset api to load balancer then to its destination
- It's lightweight 
- Human readable reqest and results
- Standard less, in long run it can be expensive to maintain
- Less bandwidth is required as compared to XML RPC and SOAP
- Easy to call than XML RPC and SOAP

### The XML RPC / SOAP apis
- It’s suitable for the application where the state is required
- It can be difficult to implement as it's required leanring curve and different tools
- It can be the robust
- The security is bettern than REST apis
- The Soap apis
- It has standard, like The request and response would be xml format so the data type can be predictable.
- It is suitable for distribute application
- Large data can be send through the SOAP, as it’s cumbersome throghh REST api


### Why REST api ?

The REST api is easy to use.It’s suitable for the application where the maintaining state between the client and server is not required. It useful for the application which needs the CURD operation.  If the security is not super major concern like, which parameters are going through GET do not matter then we can prefer for REST. It’s easy to use. If we want the user not to see any kind of information on request url then we may opt for soap. There are many benefits of using REST, like it’s light weight, cacheable, human readable results, and it’s scalable.


### Why RPC XML/SOAP ?

Soap is suitable there where maintaining the state is required between the clients and severs. Eg in distributed system, we might need store the information that how many server/devices are connected the centrailze server. In anther case, the server might need to store the information about client into server. It’s suitable for where the large data need to be passed into the request. The RPC/SOAP are more secure than REST. 
To receive and request the data we might need the rpc/soap tool kit.

Resources

- https://www.freelancinggig.com/blog/2018/11/02/what-is-the-difference-between-api-and-rest-api/
- https://www.geeksforgeeks.org/restful-routes-in-node-js/?ref=rp
- https://stackoverflow.com/questions/26830431/web-service-differences-between-rest-and-rp
- https://cloud.google.com/blog/products/application-development/rest-vs-rpc-what-problems-are-you-trying-to-solve-with-your-apis
- https://maxivak.com/rest-vs-xml-rpc-vs-soap/


# React vs Vue

React for big application. It's little complex as compared to Vue
Vue for small application. It’s easy to use.
