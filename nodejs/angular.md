# Angular Interview & Study Guide

## Table of Contents

1. [Core Angular Concepts & Questions](#core-angular-concepts--questions)
2. [Scenario-Based & Deep-Dive Questions](#scenario-based--deep-dive-questions)
3. [Code Snippet Interview Drills](#code-snippet-interview-drills)
4. [Angular vs React vs Vue: At a Glance](#angular-vs-react-vs-vue-at-a-glance)
5. [Why Choose Angular Over React and Vue?](#why-choose-angular-over-react-and-vue)
6. [Angular Lifecycle Hooks](#angular-lifecycle-hooks)
7. [State Management in Angular](#state-management-in-angular)
8. [Angular Routing](#angular-routing)
9. [Lifecycle Hooks — Basic Interview Questions](#lifecycle-hooks--basic-interview-questions)
10. [State Management — Basic Interview Questions](#state-management--basic-interview-questions)
11. [Routing — Basic Interview Questions](#routing--basic-interview-questions)
12. [Lifecycle Hooks — Answers](#lifecycle-hooks--answers)
13. [State Management — Answers](#state-management--answers)
14. [Routing — Answers](#routing--answers)
15. [Data Binding in Angular](#data-binding-in-angular)
16. [Directives](#directives)
17. [Component Scope & Interaction](#component-scope--interaction)
18. [Dependency Injection (DI)](#dependency-injection-di)
19. [Bonus: Quick Interview Drill Table](#bonus-quick-interview-drill-table)
20. [Data Binding Types Explained](#data-binding-types-explained)

---

## Core Angular Concepts & Questions

1. **What is Angular?**  
    *Why this question?*  
    Tests foundational understanding of the framework.

    **Sample Answer:**  
    Angular is a TypeScript-based front-end framework developed by Google for building single-page applications (SPAs). It provides features like components, routing, services, and dependency injection out of the box.

2. **What is a Component in Angular?**  
    *Why this question?*  
    Components are the basic building blocks of Angular applications.

    **Sample Answer:**  
    A component controls a section of the UI and consists of three parts:
    - A TypeScript class (business logic)
    - An HTML template (view)
    - A CSS style (design)

    **Example:**
    ```ts
    @Component({
      selector: 'app-hello',
      template: `<h1>Hello {{name}}</h1>`
    })
    export class HelloComponent {
      name = 'Angular';
    }
    ```

3. **What is a Module in Angular?**  
    *Why this question?*  
    To check if the candidate understands application structure.

    **Sample Answer:**  
    A module is a container for components, services, pipes, and directives. The AppModule is the root module in every Angular application.

    **Example:**
    ```ts
    @NgModule({
      declarations: [AppComponent],
      imports: [BrowserModule],
      bootstrap: [AppComponent]
    })
    export class AppModule {}
    ```

4. **What is Data Binding in Angular?**  
    *Why this question?*  
    To test understanding of template interaction with component logic.

    **Sample Answer:**  
    Angular supports four types of data binding:
    - Interpolation – `{{ name }}`
    - Property Binding – `[src]="imageUrl"`
    - Event Binding – `(click)="onClick()"`
    - Two-way Binding – `[(ngModel)]="username"`

    **Example:**
    ```html
    <input [(ngModel)]="username">
    <p>Hello, {{username}}</p>
    ```

5. **What is a Directive in Angular?**  
    *Why this question?*  
    Directives are a unique and powerful part of Angular’s template syntax.

    **Sample Answer:**  
    A directive is used to extend or modify the behavior of elements in the DOM.

    **Types:**
    - Structural Directives: Change DOM layout (e.g., *ngIf, *ngFor)
    - Attribute Directives: Change the appearance or behavior of an element (e.g., ngClass, ngStyle)
    - Custom Directives: Created by developers

    **Example:**
    ```html
    <div *ngIf="isLoggedIn">Welcome!</div>
    ```

6. **What are Services in Angular?**  
    *Why this question?*  
    Services are used to share data or logic across components.

    **Sample Answer:**  
    A service is a class with reusable logic (like fetching data from an API). Services are injected into components using Angular’s DI system.

    **Example:**
    ```ts
    @Injectable({ providedIn: 'root' })
    export class UserService {
      getUser() { return { name: 'John' }; }
    }
    ```

7. **What is Routing in Angular?**  
    *Why this question?*  
    Routing is essential for building SPAs.

    **Sample Answer:**  
    Routing allows navigation between different views (components) in an Angular app using the RouterModule.

    **Example:**
    ```ts
    const routes: Routes = [
      { path: 'home', component: HomeComponent },
      { path: '', redirectTo: '/home', pathMatch: 'full' }
    ];
    ```

8. **What is Angular CLI?**  
    *Why this question?*  
    A core developer tool in Angular apps.

    **Sample Answer:**  
    Angular CLI is a command-line interface tool to create, build, test, and deploy Angular applications easily.

    **Common commands:**
    - `ng new my-app` — create a new app
    - `ng serve` — run the app
    - `ng generate component user` — generate a component

9. **What is a Pipe in Angular?**  
    *Why this question?*  
    Pipes transform data in templates.

    **Sample Answer:**  
    A pipe transforms data in the template, like formatting dates, currency, or strings.

    **Example:**
    ```html
    <p>{{ today | date:'shortDate' }}</p>
    ```
    You can also create custom pipes.

10. **What is the purpose of ngOnInit() lifecycle hook?**  
     *Why this question?*  
     Lifecycle hooks are a basic but important part of Angular components.

     **Sample Answer:**  
     ngOnInit() is called after the component is initialized. It’s often used to fetch data from a service.

     **Example:**
     ```ts
     ngOnInit() {
        this.user = this.userService.getUser();
     }
     ```

11. **What is the role of @Injectable() decorator?**  
     *Why this question?*  
     Tests understanding of DI system.

     **Sample Answer:**  
     @Injectable() marks a class as available to be injected as a service. The providedIn: 'root' option makes it a singleton service at the root level.

12. **What is the difference between ngIf and ngSwitch?**  
     *Why this question?*  
     Shows candidate’s understanding of conditional rendering.

     **Sample Answer:**  
     - *ngIf shows/hides an element based on a boolean expression.
     - ngSwitch is used for multiple conditional views (like switch-case in JavaScript).

---

## Scenario-Based & Deep-Dive Questions

1. **💭 If Angular has two-way binding, why would you still use one-way binding in some cases?**  
    *What it tests:* Grasp of binding performance and control over state.

    **Sample Answer:**  
    Two-way binding is convenient, but can lead to complex state mutations. One-way binding ([value]="data") ensures the flow of data is controlled, especially in larger apps where debugging unintended changes can be difficult. It’s also more performant since fewer watchers are involved.

2. **🤔 Imagine your component isn't updating the UI after a data change. What could be the cause?**  
    *What it tests:* Understanding of change detection.

    **Sample Answer:**  
    Angular uses change detection to update the DOM. If a value is changed outside Angular’s zone (like inside a setTimeout or third-party callback), Angular might not detect it. Using ChangeDetectorRef.detectChanges() or NgZone.run() can manually trigger an update.

3. **🧠 What happens if you forget to unsubscribe from an observable in Angular?**  
    *What it tests:* Understanding of memory management and RxJS.

    **Sample Answer:**  
    Forgetting to unsubscribe can lead to memory leaks, especially with infinite observables (e.g., interval, Subject). The component might be destroyed, but the subscription remains active. This can also cause unexpected behavior or performance degradation.

    **Solution:** Use takeUntil, AsyncPipe, or ngOnDestroy.

4. **🕵️‍♂️ What’s the difference between ngOnInit() and a constructor?**  
    *What it tests:* Understanding Angular lifecycle hooks vs TypeScript class logic.

    **Sample Answer:**  
    The constructor is used for dependency injection and setting up simple values. ngOnInit() is called after Angular sets up the component’s inputs, so it’s the proper place for fetching data and interacting with the template.

5. **⚖️ Why might you choose standalone components instead of NgModules in a new Angular project?**  
    *What it tests:* Knowledge of Angular 14+ architecture and modern best practices.

    **Sample Answer:**  
    Standalone components reduce boilerplate by removing the need for NgModules, simplify lazy loading, and lead to a more modular and modern architecture. In Angular 19, it’s encouraged for faster builds and cleaner app structure.

6. **💡 If you wanted to reuse a button style and behavior across your app, would you use a component, directive, or pipe—and why?**  
    *What it tests:* Understanding Angular abstraction patterns.

    **Sample Answer:**  
    If it's just behavior, use a directive. If it's UI + behavior, use a component. Pipes are for transforming data, so not appropriate.  
    For example, a directive could handle button clicks with debounce logic, while a component could define a full `<app-button>` UI with styling.

7. **🧪 What makes Angular applications test-friendly?**  
    *What it tests:* Understanding of Angular’s architecture and developer tooling.

    **Sample Answer:**  
    Angular encourages testable code by using dependency injection, separation of concerns, and providing built-in testing utilities like TestBed. Services can be mocked easily, and the CLI provides ng test to run unit tests out of the box.

8. **🔄 How does Angular's change detection work, and how can you make it faster?**  
    *What it tests:* Understanding performance internals.

    **Sample Answer:**  
    Angular runs change detection on the entire component tree after any event. Using ChangeDetectionStrategy.OnPush tells Angular to only check a component if its inputs change, improving performance. You can also use signals in Angular 16+ for finer reactivity.

9. **🧩 Why is trackBy important in *ngFor loops?**  
    *What it tests:* Understanding of DOM rendering efficiency.

    **Sample Answer:**  
    Without trackBy, Angular re-renders every DOM element when a list changes. With trackBy, Angular tracks items by identity (like id), reducing DOM updates and improving performance, especially for large lists.

10. **🚀 How would you architect an Angular app that scales to hundreds of components and multiple teams?**  
     *What it tests:* Architectural thinking and real-world experience.

     **Sample Answer:**
     - Use feature modules or standalone components
     - Adopt shared/core module patterns or libraries
     - Use lazy loading for large features
     - Define code style guides and testing standards
     - Use NX monorepo or Micro Frontends for team scalability
     - Employ state management tools like NgRx or Signals

---

## Code Snippet Interview Drills

### 1. Two-Way vs One-Way Binding

**Code Snippet:**
```html
<input [value]="username" (input)="username = $event.target.value">
<p>Hello, {{ username }}</p>
```
**Ask:**  
This is one-way binding with manual event handling. Why might we prefer this over [(ngModel)], and when is [(ngModel)] more appropriate?

**Expected Explanation:**  
One-way binding gives more control and is more performant in complex forms. [(ngModel)] is simpler for basic use but less explicit and harder to debug in large apps.

---

### 2. Change Detection

**Code Snippet:**
```ts
setTimeout(() => {
  this.message = 'Updated!';
}, 0);
```
**Ask:**  
This code sets message but the UI doesn’t update. Why? How can we fix it?

**Expected Explanation:**  
The code runs outside Angular’s zone. The view won't detect the change. Fix with:
```ts
this.zone.run(() => this.message = 'Updated!');
```
or manually call ChangeDetectorRef.detectChanges().

---

### 3. Memory Leaks

**Code Snippet:**
```ts
ngOnInit() {
  this.subscription = this.myService.getData().subscribe(console.log);
}
```
**Ask:**  
What’s the issue with this approach? How can you prevent problems when the component is destroyed?

**Expected Explanation:**  
The subscription is never cleaned up, which causes memory leaks. Use:
```ts
ngOnDestroy() {
  this.subscription.unsubscribe();
}
```
Or use takeUntil, or better, use AsyncPipe in the template.

---

### 4. Constructor vs ngOnInit

**Code Snippet:**
```ts
constructor(private userService: UserService) {
  console.log(this.userService.getUser());
}

ngOnInit() {
  console.log('Component Initialized');
}
```
**Ask:**  
What’s the difference between these two blocks, and what kind of logic belongs where?

**Expected Explanation:**  
Use the constructor for DI and simple setup. Use ngOnInit() for anything involving @Input() or DOM interaction, since the inputs are not yet bound in the constructor.

---

### 5. Standalone vs NgModules

**Code Snippet:**
```ts
@Component({
  standalone: true,
  selector: 'app-hello',
  template: `<h1>Hello</h1>`,
  imports: [CommonModule]
})
export class HelloComponent {}
```
**Ask:**  
This is a standalone component. What are its advantages over NgModules?

**Expected Explanation:**  
Standalone components reduce boilerplate, make lazy loading easier, and simplify dependency declarations. Great for modern, modular Angular apps.

---

### 6. Directive vs Component vs Pipe

**Code Snippet:**
```ts
@Directive({
  selector: '[appDebounceClick]'
})
export class DebounceClickDirective { /* ... */ }
```
**Ask:**  
Why use a directive here instead of a component? What’s the benefit?

**Expected Explanation:**  
A directive is best for extending behavior of existing elements (like debouncing click). A component would be used if we needed to encapsulate UI and structure.

---

### 7. Testability

**Code Snippet:**
```ts
@Component({
  template: `<button (click)="add()">Add</button>`
})
export class CounterComponent {
  count = 0;
  add() { this.count++; }
}
```
**Ask:**  
How would you test this component? What makes Angular test-friendly?

**Expected Explanation:**  
Use TestBed to create the component, simulate click, and assert on count. Angular’s DI, clear separation of concerns, and CLI tools make unit testing easy.

---

### 8. Change Detection Strategy

**Code Snippet:**
```ts
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `<p>{{ name }}</p>`
})
export class UserComponent {
  @Input() name: string;
}
```
**Ask:**  
What does OnPush do, and how would Angular behave differently without it?

**Expected Explanation:**  
With OnPush, Angular only checks the component when inputs change or events are triggered. Without it, change detection runs more often, reducing performance.

---

### 9. *ngFor with trackBy

**Code Snippet:**
```html
<li *ngFor="let user of users; trackBy: trackById">{{ user.name }}</li>
```
**Ask:**  
Why do we use trackBy here? What happens if we don’t?

**Expected Explanation:**  
Without trackBy, Angular re-renders all DOM elements on data changes. With trackBy, it only updates changed items, improving performance for large lists.

---

### 10. App Scalability Architecture

**Code Snippet:**
```ts
@NgModule({
  imports: [UserModule, ProductModule, OrderModule],
})
export class AppModule {}
```
**Ask:**  
If your Angular app has 50+ features and many developers, how would you organize it for maintainability?

**Expected Explanation:**  
Use feature modules or standalone components per domain. Apply lazy loading, shared/core modules, consistent naming conventions, and state management (like NgRx or Signals). Optionally use monorepos like Nx.

---

## Angular vs React vs Vue: At a Glance

| Feature / Factor   | Angular                | React                        | Vue                              |
|--------------------|-----------------------|------------------------------|----------------------------------|
| Type               | Full-fledged framework| UI library                   | Progressive framework            |
| Language           | TypeScript            | JavaScript (TS optional)     | JavaScript (TS optional)         |
| Learning Curve     | Steep                 | Moderate                     | Easy to moderate                 |
| Structure          | Opinionated, CLI-driven| Flexible, minimal out-of-the-box | Balanced: simple with optional complexity |
| State Management   | RxJS, Signals, NgRx   | Redux, Zustand, Context API  | Vuex, Pinia                      |
| DOM                | Real DOM              | Virtual DOM                  | Virtual DOM                      |
| Community          | Large enterprise-focused| Largest, massive ecosystem   | Fast-growing and community-friendly |
| Suitability        | Enterprise-grade SPAs, large apps | Interactive UI, SPAs      | Quick prototypes, mid-sized SPAs |
| Tooling (CLI)      | Excellent (built-in testing, lazy loading) | Create React App / Vite / Next.js | Vue CLI / Vite                  |
| Performance        | Fast with Signals & OnPush | Fast, depends on diffing strategy | Fast, optimized with reactivity system |
| Mobile/Desktop Support | Angular + Ionic or NativeScript | React Native / Expo        | Vue Native (less popular)        |

---

## Why Choose Angular Over React and Vue?

Here are compelling reasons to choose Angular—especially for enterprise or large-scale development.

1. **🏢 Enterprise-Ready Framework**  
    Angular is a complete solution—it includes:
    - Dependency injection
    - Routing
    - HTTP client
    - Form handling (template + reactive)
    - Built-in internationalization
    - CLI for generating services, components, tests  
    No need to assemble third-party libraries as in React.

2. **🧱 Strong Architectural Patterns**  
    Angular enforces:
    - Component-based architecture
    - Separation of concerns (via services)
    - Module system (or standalone components from v14+)  
    This makes it ideal for large teams and long-term maintainability.

3. **🔒 TypeScript by Default**  
    Angular is built with TypeScript, not just compatible with it. This means:
    - Better tooling (autocompletion, refactoring)
    - Safer code
    - Catching bugs at compile time  
    React and Vue support TypeScript but require extra setup.

4. **🧰 Powerful CLI & Tooling**  
    Angular CLI supports:
    - AOT compilation
    - Lazy loading
    - Linting
    - Unit and e2e testing
    - Environment management  
    All of this is standardized and production-ready out of the box.

5. **🔁 Advanced Change Detection with Signals (Angular 16+)**  
    Angular 16+ introduces Signals, which are:
    - Fine-grained reactivity system
    - Comparable to Vue’s reactivity
    - More predictable than React’s hook model  
    This improves performance significantly while maintaining clarity.

6. **🛡️ Built-in Security and Best Practices**  
    Angular’s out-of-the-box protections:
    - XSS protection
    - Sanitization APIs
    - Content Security Policy support  
    It encourages best practices by design, reducing security risks in critical apps.

7. **🔍 Testability**  
    Angular is designed for unit and integration testing, with:
    - TestBed
    - Dependency injection
    - CLI-generated test stubs  
    In contrast, React and Vue require setting up test environments manually (Jest, RTL, etc.).

8. **🤝 Backed by Google and Used in Large-Scale Apps**  
    Angular is maintained by Google and used in:
    - Google Cloud Console
    - Microsoft Office Web apps
    - Deutsche Bank, BMW, McKinsey
    - Internal and government-grade systems  
    This gives it long-term support and confidence for large deployments.

**❗ When Not to Choose Angular**  
For simple apps or quick MVPs, Vue or React are easier to start with.  
Angular's learning curve is higher.  
If you want flexibility with tools and patterns, React might be preferable.

---

## Angular Lifecycle Hooks

Angular lifecycle hooks are special methods that get called at specific points in a component’s or directive’s life cycle—from creation to destruction.

> "Angular calls certain functions automatically while your component is being born, changing, or dying."

### 🧬 Common Angular Lifecycle Hooks (with Example)

Let’s use this simple component:
```ts
@Component({
  selector: 'app-example',
  template: `<p>{{message}}</p>`
})
export class ExampleComponent {
  message = 'Hello Angular!';
}
```
Now, let’s add lifecycle hooks to it.

1. **constructor()**  
    ✅ Called first, when the component is created  
    ❌ Angular doesn’t yet know @Inputs or render the template
    ```ts
    constructor() {
      console.log('Constructor: Component created');
    }
    ```

2. **ngOnInit()**  
    ✅ Called once after Angular initializes all @Input()s  
    ✅ Best for fetching data or setting up logic
    ```ts
    ngOnInit() {
      console.log('ngOnInit: Inputs ready, fetch data');
    }
    ```

3. **ngOnChanges(changes: SimpleChanges)**  
    ✅ Called when any @Input() value changes  
    ✅ Also called before ngOnInit() on first load
    ```ts
    @Input() data: string;

    ngOnChanges(changes: SimpleChanges) {
      console.log('ngOnChanges: Input changed', changes);
    }
    ```

4. **ngDoCheck()**  
    ✅ Called on every change detection cycle  
    ❌ Use carefully — it runs often
    ```ts
    ngDoCheck() {
      console.log('ngDoCheck: Change detection ran');
    }
    ```

5. **ngAfterContentInit()**  
    ✅ Called after `<ng-content>` projected content is added
    ```ts
    ngAfterContentInit() {
      console.log('ngAfterContentInit: Content projected');
    }
    ```

6. **ngAfterContentChecked()**  
    ✅ Called after every check of projected content
    ```ts
    ngAfterContentChecked() {
      console.log('ngAfterContentChecked: Projected content checked');
    }
    ```

7. **ngAfterViewInit()**  
    ✅ Called after component’s view (template) is rendered  
    ✅ Good place to access ViewChild
    ```ts
    @ViewChild('myElement') myElement!: ElementRef;

    ngAfterViewInit() {
      console.log('ngAfterViewInit: View is ready', this.myElement);
    }
    ```

8. **ngAfterViewChecked()**  
    ✅ Called after every check of the view (e.g. DOM changes)
    ```ts
    ngAfterViewChecked() {
      console.log('ngAfterViewChecked: View checked again');
    }
    ```

9. **ngOnDestroy()**  
    ✅ Called just before Angular destroys the component  
    ✅ Use to clean up subscriptions, intervals, etc.
    ```ts
    ngOnDestroy() {
      console.log('ngOnDestroy: Component destroyed');
    }
    ```

### 🧠 Simple Flow Summary

```
1. constructor()
2. ngOnChanges()     // if @Input
3. ngOnInit()
4. ngDoCheck()
5. ngAfterContentInit()
6. ngAfterContentChecked()
7. ngAfterViewInit()
8. ngAfterViewChecked()
9. ngOnDestroy()
```

### ✅ Real Example in Practice

```html
<app-user [name]="userName"></app-user>
```
```ts
@Component({
  selector: 'app-user',
  template: `<p>Hello {{name}}</p>`
})
export class UserComponent implements OnInit, OnDestroy {
  @Input() name: string;

  ngOnInit() {
     console.log('Component Initialized with name:', this.name);
  }

  ngOnDestroy() {
     console.log('Component will be destroyed');
  }
}
```
**📌 Tip:**  
You don’t need to implement all lifecycle hooks. Only use the ones you need. Angular will ignore the rest.

---

## State Management in Angular

State is the data your application uses, such as:
- A logged-in user
- A list of products
- A cart in an e-commerce app

**State Management** means keeping track of that data, updating it, and sharing it between components in a clean, consistent way.

### 👶 Without State Management (Example)

Let’s say we have two components:
- ProductListComponent
- CartComponent

You want to add products to cart from ProductList and display the total items in cart in CartComponent.

If you don’t use a state management pattern, you may:
- Pass data through @Input() and @Output() (messy with many components)
- Use a shared service (simpler, but can grow complicated)

### ✅ With Simple State Management (Using a Service + BehaviorSubject)

Let’s use a shared service with RxJS BehaviorSubject.

#### 🧱 Step 1: Create the Service

```ts
@Injectable({ providedIn: 'root' })
export class CartService {
  private cartItems = new BehaviorSubject<Product[]>([]);
  cartItems$ = this.cartItems.asObservable();

  addToCart(product: Product) {
     const currentItems = this.cartItems.getValue();
     this.cartItems.next([...currentItems, product]);
  }

  clearCart() {
     this.cartItems.next([]);
  }
}
```

**🔁 What’s Happening Here?**
- BehaviorSubject holds the current cart state
- cartItems$ is an Observable other components can subscribe to
- addToCart() updates the cart state

#### 🧱 Step 2: Add to Cart from ProductListComponent

```ts
@Component({ /* ... */ })
export class ProductListComponent {
  constructor(private cartService: CartService) {}

  add(product: Product) {
     this.cartService.addToCart(product);
  }
}
```

#### 🧱 Step 3: Display Cart Count in CartComponent

```ts
@Component({ /* ... */ })
export class CartComponent {
  cartCount = 0;

  constructor(private cartService: CartService) {}

  ngOnInit() {
     this.cartService.cartItems$.subscribe(items => {
        this.cartCount = items.length;
     });
  }
}
```

```
 ┌──────────────────────────────┐
 │      ProductListComponent    │
 │  [Add to Cart] button        │
 └────────────┬─────────────────┘
                  │
                  ▼
        Calls cartService.addToCart(product)
                  │
                  ▼
 ┌──────────────────────────────┐
 │         CartService          │
 │  - cartItems: BehaviorSubject│
 │  - addToCart(product)        │
 │  - cartItems$ (Observable)   │
 └────────────┬─────────────────┘
                  │
      Emits updated cart state
                  ▼
 ┌──────────────────────────────┐
 │        CartComponent         │
 │  Subscribes to cartItems$    │
 │  Displays cartCount          │
 └──────────────────────────────┘
```

---

## Angular Routing

Angular Routing allows you to navigate between different components (or "pages") without reloading the whole page.

> Think of it like switching screens in a mobile app — you're not reloading the whole app, just changing what's shown.

### 🧱 Step-by-Step Example: Basic Routing

#### 👨‍🏫 Scenario:
We want to build a site with these "pages":
- `/home` → HomeComponent
- `/about` → AboutComponent
- `/contact` → ContactComponent

#### 🧰 Step 1: Create Components

```bash
ng generate component home
ng generate component about
ng generate component contact
```

#### 🗺️ Step 2: Set Up Routing

In `app-routing.module.ts`:
```ts
const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: 'contact', component: ContactComponent },
  { path: '', redirectTo: 'home', pathMatch: 'full' }, // default route
  { path: '**', redirectTo: 'home' } // wildcard (not found)
];
```
Then import it into your app:
```ts
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

#### 📦 Step 3: Add `<router-outlet>` in App Template

In `app.component.html`:
```html
<nav>
  <a routerLink="/home">Home</a> |
  <a routerLink="/about">About</a> |
  <a routerLink="/contact">Contact</a>
</nav>

<!-- Page content will be shown here -->
<router-outlet></router-outlet>
```

#### 🧠 What’s Going On?
- `<router-outlet>` is where Angular will render the component that matches the current route.
- `<a routerLink="...">` is used instead of normal `<a href="...">` to prevent full page reloads.

#### 🏃 Navigating with Code

You can navigate from TypeScript code like this:
```ts
constructor(private router: Router) {}

goToContact() {
  this.router.navigate(['/contact']);
}
```

#### 🧪 Optional: Route Parameters

URL: `/product/42`
```ts
{ path: 'product/:id', component: ProductComponent }
```
In ProductComponent:
```ts
constructor(private route: ActivatedRoute) {}

ngOnInit() {
  const id = this.route.snapshot.paramMap.get('id');
  console.log('Product ID:', id);
}
```

---

## Lifecycle Hooks — Basic Interview Questions

### Q1: What will be the order of execution of the following lifecycle hooks?

```ts
export class TestComponent implements OnInit, OnDestroy, OnChanges {
  @Input() data: string;

  constructor() {
     console.log('Constructor called');
  }

  ngOnChanges() {
     console.log('ngOnChanges called');
  }

  ngOnInit() {
     console.log('ngOnInit called');
  }

  ngOnDestroy() {
     console.log('ngOnDestroy called');
  }
}
```
**❓ Follow-up:**
- What is the purpose of each hook?
- Will ngOnChanges be called before or after ngOnInit?
- When will ngOnDestroy be triggered?

---

### Q2: What’s the difference between ngOnInit() and constructor()? Can you give a use case for each?

```ts
constructor() {
  console.log('Constructor runs first');
}

ngOnInit() {
  console.log('ngOnInit is for logic after inputs are available');
}
```
**❓ Follow-up:**
- Why shouldn’t we use constructor to call an API?
- Which is better for initializing component input values?

---

## State Management — Basic Interview Questions

### Q3: This service holds cart data. What will be the output when you add two products?

```ts
@Injectable({ providedIn: 'root' })
export class CartService {
  private cartItems = new BehaviorSubject<string[]>([]);
  cartItems$ = this.cartItems.asObservable();

  addItem(item: string) {
     const updated = [...this.cartItems.getValue(), item];
     this.cartItems.next(updated);
  }
}
```
```ts
cartService.addItem('Apple');
cartService.addItem('Banana');

cartService.cartItems$.subscribe(items => console.log(items));
```
**❓ Follow-up:**
- What is a BehaviorSubject, and why is it used here?
- What would be the difference if you used a Subject instead?

---

### Q4: Modify this service to remove an item from the cart

```ts
removeItem(item: string) {
  // candidate to implement
}
```
**❓ Follow-up:**
- How would you ensure the state remains immutable?
- Why is immutability important in state management?

---

## Routing — Basic Interview Questions

### Q5: What route will be matched for the following path? What is rendered?

```ts
const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  { path: '**', component: NotFoundComponent }
];
```
**❓ Follow-up:**
- What does pathMatch: 'full' mean?
- What happens if you change it to 'prefix'?

---

### Q6: What does `<router-outlet>` do in the below code?

```html
<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
</nav>

<router-outlet></router-outlet>
```
**❓ Follow-up:**
- What happens if you remove `<router-outlet>`?
- Can you have multiple router-outlets?

---

### Q7: How do you read route parameters in a component?

Given route:
```ts
{ path: 'product/:id', component: ProductComponent }
```
Component:
```ts
ngOnInit() {
  const id = this.route.snapshot.paramMap.get('id');
}
```
**❓ Follow-up:**
- What will id contain if the route is /product/123?
- What is the difference between snapshot and paramMap.subscribe()?

---

## Lifecycle Hooks — Answers

### Q1: Lifecycle Hook Order

**Code:**
```ts
export class TestComponent implements OnInit, OnDestroy, OnChanges {
  @Input() data: string;

  constructor() {
     console.log('Constructor called');
  }

  ngOnChanges() {
     console.log('ngOnChanges called');
  }

  ngOnInit() {
     console.log('ngOnInit called');
  }

  ngOnDestroy() {
     console.log('ngOnDestroy called');
  }
}
```
**Output (when input changes):**
```
Constructor called
ngOnChanges called
ngOnInit called
```
**Explanation:**
- constructor: Initializes class properties. No DOM or data is available yet.
- ngOnChanges: Called whenever input-bound properties change (runs before ngOnInit).
- ngOnInit: Ideal for initialization logic like API calls.
- ngOnDestroy: Called just before the component is destroyed (used for cleanup like unsubscribing).

---

### Q2: ngOnInit vs constructor

**Answer:**
- constructor: Used for dependency injection and setting up basic properties.
- ngOnInit: Used when you need to access @Input() properties, make HTTP requests, or do any initialization that relies on Angular bindings.

**Use Case:**
```ts
constructor(private service: UserService) {
  // OK: Inject dependencies
}

ngOnInit() {
  // Correct: Fetch data from API after bindings are ready
  this.service.getUser().subscribe();
}
```

---

## State Management — Answers

### Q3: BehaviorSubject Output

**Code:**
```ts
cartService.addItem('Apple');
cartService.addItem('Banana');

cartService.cartItems$.subscribe(items => console.log(items));
```
**Output:**
```ts
['Apple', 'Banana']
```
**Explanation:**
- BehaviorSubject holds the current state and emits it to any new subscribers.
- getValue() fetches the current state, and next() updates it.
- State is updated immutably using spread syntax ([...]).

---

### Q4: Remove Item from Cart

**Answer:**
```ts
removeItem(item: string) {
  const updated = this.cartItems.getValue().filter(i => i !== item);
  this.cartItems.next(updated);
}
```
**Explanation:**
- We use filter() to create a new array without the item.
- This maintains immutability, which prevents side effects and improves predictability.

---

## Routing — Answers

### Q5: Route Matching Logic

**Routes:**
```ts
const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  { path: '**', component: NotFoundComponent }
];
```
**Explanation:**
- Visiting `/` will redirect to `/home` (because of pathMatch: 'full').
- If the user goes to an unknown path like `/random`, it renders NotFoundComponent.

**Difference between full vs prefix:**
- full: Matches the entire path.
- prefix: Matches the beginning of the path — may lead to unexpected redirects.

---

### Q6: `<router-outlet>` Role

**Answer:**
- Acts as a placeholder where Angular injects the component that matches the current route.

**Explanation:**
```html
<!-- Displays HomeComponent if current route is /home -->
<router-outlet></router-outlet>
```
Without `<router-outlet>`:
- Nothing will render from routing, even if routes are set correctly.

---

### Q7: Reading Route Parameters

**Code:**
```ts
ngOnInit() {
  const id = this.route.snapshot.paramMap.get('id');
}
```
**Explanation:**
- If the route is `/product/123`, id will be `"123"`.

**Difference:**
```ts
// Snapshot – one-time read
this.route.snapshot.paramMap.get('id');

// Subscribe – tracks changes on the fly
this.route.paramMap.subscribe(params => {
  const id = params.get('id');
});
```
Use snapshot for static routes and subscribe for dynamic routes (e.g., when navigating to the same component with different params).

---

## Data Binding in Angular

### ✅ Q1: What are the types of data binding in Angular? Explain with examples.

**Answer:**

Angular supports 4 types of data binding:

| Type             | Syntax                    | Purpose                        |
|------------------|--------------------------|--------------------------------|
| Interpolation    | `{{ value }}`            | Display data in the view       |
| Property Binding | `[property]="value"`      | Bind a property of an element  |
| Event Binding    | `(event)="handler()"`     | Listen to DOM events           |
| Two-way Binding  | `[(ngModel)]="value"`     | Sync data between view & comp. |

**Code Snippet:**
```html
<!-- Interpolation -->
<h1>{{ title }}</h1>

<!-- Property Binding -->
<img [src]="imageUrl" />

<!-- Event Binding -->
<button (click)="handleClick()">Click Me</button>

<!-- Two-way Binding -->
<input [(ngModel)]="name" />
<p>Hello, {{ name }}</p>
```

---

## Directives

### ✅ Q2: What are structural and attribute directives? Give examples.

**Answer:**

| Type        | Purpose                   | Example                |
|-------------|--------------------------|------------------------|
| Structural  | Change the DOM layout     | *ngIf, *ngFor          |
| Attribute   | Change appearance/behavior| ngClass, ngStyle       |

**Code Snippet:**
```html
<!-- Structural Directive -->
<div *ngIf="isVisible">I am visible!</div>

<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>

<!-- Attribute Directive -->
<p [ngClass]="{'highlight': isImportant}">Text</p>
<p [ngStyle]="{color: 'red'}">Styled Text</p>
```
**Explanation:**
- *ngIf removes or adds the element from the DOM.
- ngClass dynamically adds/removes CSS classes.
- *ngFor repeats elements.

---

## Component Scope & Interaction

### ✅ Q3: How does Angular handle component scopes?

**Answer:**  
Angular uses component-based architecture where each component has its own isolated scope. Communication happens via:
- @Input() – Parent to Child
- @Output() – Child to Parent

**Code Snippet:**

**Parent Template**
```html
<app-child [title]="parentTitle" (notify)="onNotified($event)"></app-child>
```
**Child Component**
```ts
@Input() title: string;
@Output() notify = new EventEmitter<string>();

sendNotification() {
  this.notify.emit('Message from child');
}
```

---

## Dependency Injection (DI)

### ✅ Q4: What is Dependency Injection in Angular and how does it work?

**Answer:**  
Dependency Injection is a design pattern Angular uses to supply classes (like services) with their dependencies, instead of creating them manually.

Angular's DI system:
- Registers services via the @Injectable() decorator.
- Injects them into constructors of components or other services.

**Code Snippet:**
```ts
@Injectable({ providedIn: 'root' })
export class LoggerService {
  log(message: string) {
     console.log(message);
  }
}

@Component({ ... })
export class AppComponent {
  constructor(private logger: LoggerService) {
     this.logger.log('AppComponent created');
  }
}
```
**Explanation:**
- Angular injects LoggerService into AppComponent.
- This promotes modularity and testability.

---

## Bonus: Quick Interview Drill Table

| Concept      | Quick Question                                     | Expected Response                                   |
| ------------ | -------------------------------------------------- | --------------------------------------------------- |
| Data Binding | How does `[(ngModel)]` work?                       | Two-way binding — sync between view and model       |
| Directive    | Difference between `*ngIf` and `hidden` attribute? | `*ngIf` removes element from DOM, `hidden` hides it |
| Scope        | How do components share data?                      | `@Input`, `@Output`, or shared service              |
| DI           | Why use a service instead of creating objects?     | Reusability, testability, centralized logic         |

---

## Data Binding Types Explained

### 1. Interpolation (`{{ expression }}`)

**Purpose:**  
Display component data inside the HTML template.

**How It Works:**  
Angular evaluates the expression inside `{{ }}` and renders the result in the DOM.  
It's one-way: from component to view.

**Example:**
```ts
export class AppComponent {
  title = 'Angular Data Binding';
}
```
```html
<h1>{{ title }}</h1> <!-- Output: Angular Data Binding -->
```

---

### 2. Property Binding (`[property]="expression"`)

**Purpose:**  
Bind a DOM property to a component property.

**How It Works:**  
Angular sets the element property (e.g., src, disabled, value) to the value from the component.  
Also one-way: from component to view.

**Example:**
```ts
export class AppComponent {
  imageUrl = 'https://example.com/image.png';
}
```
```html
<img [src]="imageUrl" /> <!-- Output: image loads from imageUrl -->
```

---

### 3. Event Binding (`(event)="handler"`)

**Purpose:**  
Respond to user actions or DOM events like clicks, keypresses, etc.

**How It Works:**  
Angular listens to the specified event and executes the method defined in the component.  
One-way: from view to component.

**Example:**
```ts
export class AppComponent {
  count = 0;

  increment() {
     this.count++;
  }
}
```
```html
<button (click)="increment()">Add</button>
<p>{{ count }}</p>
```

---

### 4. Two-way Binding (`[(ngModel)]="property"`)

**Purpose:**  
Create a synchronized link between the view and the component.

**How It Works:**  
Combines property binding (`[value]="value"`) and event binding (`(input)="value = $event.target.value"`).  
Updates the component when the user types and updates the view when the component value changes.

**Example:**
```ts
export class AppComponent {
  name = '';
}
```
```html
<input [(ngModel)]="name" />
<p>Your name is: {{ name }}</p>
```
**Note:** To use `[(ngModel)]`, you need to import the FormsModule in your module.
```ts
import { FormsModule } from '@angular/forms';
@NgModule({
  imports: [FormsModule],
})
```

---

### 🧠 Summary Table

| Type             | Syntax                    | Direction        | Use Case Example               |
| ---------------- | ------------------------- | ---------------- | ------------------------------ |
| Interpolation    | `{{ title }}`             | Component ➡ View | Show a value in a tag          |
| Property Binding | `[src]="imgUrl"`          | Component ➡ View | Set element attributes         |
| Event Binding    | `(click)="doSomething()"` | View ➡ Component | Handle user input or actions   |
| Two-way Binding  | `[(ngModel)]="name"`      | View ⬄ Component | Form inputs and instant update |

