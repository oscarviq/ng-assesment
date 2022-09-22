# Angular Technical Assessment

 Create a [stackblitz](https://stackblitz.com/) account if you don't already have one and afterwards visit this URL https://stackblitz.com/edit/angular-tech-assesment?devtoolsheight=33&file=README.md

Click on the **Fork** button in the upper left corner of the code editor to copy the project to your account.

Once you're done with the assessment you can click the **Share** button also at the upper left corner of the code editor and copy the **Editor URL**

Send back and email with the URL that you copied in order for the code to be reviewed.

### Useful Documentation
 - **JSON Placeholder** (used as API) [website](https://jsonplaceholder.typicode.com/guide/), [github](https://github.com/typicode/json-server)
 - **Akita** (used as state manager) [website](https://datorama.github.io/akita/), [github](https://github.com/datorama/akita/)
---
## 1 - Interfaces and Types

- Add the correct typing of the embedded user data in the interface **ITodo** located in `src/app/shared/interfaces/todo.interface.ts`. The **ITodo** interface defines the **user** property as `any` which is not a good practice.

> If you look at the url of the request for todo items
> [https://jsonplaceholder.typicode.com/todos?_page=1&_limit=8&_sort=title&_order=desc&_expand=user](https://jsonplaceholder.typicode.com/todos?_page=1&_limit=8&_sort=title&_order=desc&_expand=user)
> you can see the properties of the **embedded user object** that should be defined in the property typing.

```
{
    "userId": 3,
    "id": 55,
    "title": "voluptatum omnis minima qui occaecati provident nulla voluptatem ratione",
    "completed": true,
    "user": {
      "id": 3,
      "name": "Clementine Bauch",
      "username": "Samantha",
      "email": "Nathan@yesenia.net",
      "address": {
        "street": "Douglas Extension",
        "suite": "Suite 847",
        "city": "McKenziehaven",
        "zipcode": "59590-4157",
        "geo": {
          "lat": "-68.6102",
          "lng": "-47.0653"
        }
      },
      "phone": "1-463-123-4447",
      "website": "ramiro.info",
      "company": {
        "name": "Romaguera-Jacobson",
        "catchPhrase": "Face to face bifurcated interface",
        "bs": "e-enable strategic applications"
      }
    }
  }
  ```

## 2 - Components, Inputs and Outputs

- Take the todo list that exists in `src/app/features/home/pages/home-page` **without the pagination**, extract it to a new component in `src/app/features/home/components/todo-list` that receives the **todos array as an input** and use that newly created todo-list component in the homepage. Make sure the list displays **10** todos **without modifying the TodoService.getAllTodos() method**.

- Take the pagination that exists in `src/app/features/home/pages/home-page`, extract it to a new component in `src/app/shared/components/pagination` that receives a **page number as an input** that **emits an output when the previous or next button are clicked** and use that newly created pagination component in the homepage. 

##  3 - Services, Network Requests and Observables

- Create a **UserService** in `src/app/shared/services/user.service.ts` with a **getUserCount()** method that returns **the amount of existing users** doing a request to [https://jsonplaceholder.typicode.com/users](https://jsonplaceholder.typicode.com/users) and **piping the observable result with an rxjs operator**.

- Use the created **UserService.getUserCount()** method in to display the correct number of users in `src/app/features/home/pages/home-page`.

- Use the **outputs** from the **pagination component** created in step #2 to handle the previous and next events **in the parent component** in order to fetch the next page of todos. Use the existing **TodoService.getAllTodos()** method to process the requests that need to be made.

- Update the **todo list component** created in step #2 to display the new set of todos that were fetched from the previous or next output handlers.

> As a bonus but not required, prevent the user from clicking the previous button if there is no previous page and display an error and disable the next button when the next page has no more todos.

- Create an **updateTodo()** method in the **TodoService** located in: `src/app/shared/services/todo/todo.service.ts` to be able to update a Todo to be marked as completed or not completed when clicking the checkmark in the UI, after the request is successful the UI needs to be updated to reflect the change. Look at the **Updating a resource** section of the [JSON Placeholder Guide](https://jsonplaceholder.typicode.com/guide/)

## 4 - Routes and Modules

- Create a new **notes** feature with a **notes page** page in `src/app/features/notes` following the same folder structure as the home feature.

- Use the following html for the template of the notes page component and add any notes or comments you have about the assessment as items in the **ul ** element.

```
<main>

  <header class="mb-4">  

    <h1  class="text-2xl font-bold text-gray-900 flex items-center">

      <svg  xmlns="http://www.w3.org/2000/svg"  class="h-5 w-5 mr-1"  viewBox="0 0 20 20" fill="currentColor">
        <path  d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z"  />
        <path  fill-rule="evenodd"  d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z"  clip-rule="evenodd"  />
      </svg>

      Notes

    </h1>  

  </header>

  <div>

    <ul>

      <li><pre>Add note #1 Here</pre></li>

    </ul>

  </div>

</main>
```

- Modify the **app-routing.module.ts** file to add a new **/notes** route that points to that feature.

- Modify the navigation component in `src/app/core/components/navigation` to add a menu item for the new notes feature.

## 5 - Interceptors ([docs](https://angular.io/guide/http#intercepting-requests-and-responses))
- Create an http interceptor called **LoggerInterceptor**  in `src/app/shared/interceptors/logger.interceptor.ts` that outputs the response of every http request to the browser's developer console using **console.log()** 

## Bonus - State Management ([Akita](https://opensource.salesforce.com/akita/))

- Tap into the **UserService.getUserCount()** observable **using an rxjs operator** and populate the **UsersStore**. Look at the **Entity Store** section of the akita docs for guidance: https://datorama.github.io/akita/docs/entities/entity-store
