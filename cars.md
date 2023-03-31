---
marp: true
style: |

  section h1 {
    color: #6042BC;
  }

  section code {
    background-color: #e0e0ff;
  }

  footer {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100px;
  }

  footer img {
    position: absolute;
    width: 120px;
    right: 20px;
    top: 0;

  }
  section #title-slide-logo {
    margin-left: -60px;
  }
---

# LiveView and Custom Elements
### Getting the Javascript you need while keeping the LiveView you love

### Chris Nelson
### Co-Founder, Launch Scout
![h:200](full-color.png#title-slide-logo)

---

# Who am I?
- Long time Web Developer
- Big fan of:
  - Elixir
  - Web components
- Co-Founder, Launch Scout

---

# Goals of this talk
- What are custom elements (aka Web Components)?
- Why are they the best option for LiveView integration?
- How to do it
- When to do it
- Fun demo codez :)

---

# Hot take:
## It's not the Javascript that makes SPAs suck
### It's building two apps!

---

# Have you heard the good news about Custom Elements?
- Supported in all the browsers
- They are really are just HTML
- Stylable via CSS (to the precise extent you decide)
- No framework commitment required!
- There may already be one to do what you want

---

# Why they are a good fit with LiveView
- LiveView is good at rendering HTML
- They are HTML
- Easy integration path
  - Pass data in via attributes
  - Communicate back out via Custom Events

---

# [Hello Custom Element](./custom_elements1.html)

```js
class HelloCars extends HTMLElement {
  connectedCallback() {
    this.innerHTML = "Hello, Cars!";
  }
}
window.customElements.define('hello-cars', HelloCars);
```

---

# What's not here
- A lot of code
- Any framework or library

---

# Don't fear the [spoooky Shadow DOM](./custom_elements2.html)

```js
class CarsShadow extends HTMLElement {
  connectedCallback() {
    this.attachShadow({mode: 'open'});
    this.shadowRoot.innerHTML = `
      <style>
        h1 { color: red; }
      </style>
      <h1>Hi Cars.com peeps!</h1>
      <div class="body">It's great to meet <slot></slot> of you</div>
    `;
  }
}
window.customElements.define('cars-shadow', CarsShadow);
```

---

# Your custom element has something to say...
- Custom Events are what you need!
- Just a plain ol' DOM Event with:
  - A name (anything you want!)
  - A detail property (payload)

```ts
  addTodo(_event : Event) {
    this.dispatchEvent(new CustomEvent('add_todo', {
      detail: {todo: this.todoInput.value}
    }));
  }
```
---

# Custom element guidance
- Pass information in as attributes/props
- Send information out using events
- Custom events are your friend!
- Libraries like [Lit](https://lit.dev) can help
  - but you can choose whatever you like!

---

# Integrating Custom Elements with LiveView
- Include the JS
  - esbuild makes this pretty easy
- Add the element to the page
- Profit?

--- 

# Challenges we might encouner
- Passing in complex data
  - Serialize as JSON
- LiveView doesn't know about Custom Events
  - `phoenix-custom-event-hook` has your back
- If all else fails, we write a hook

---

# That's all cool but..
- Could it be even easier?
- Have you ever noticed how `<.function_components>` 
look like `<custom-elements>`?

---

# Meet LiveElements
- declaratively creates `<.functional_components>` from `<custom-elements>` 
- serializes all non-primitive attributes as JSON
- auto-wires Custom Events using `phoenix-custom-event-hook`
- call per element with `custom_element` macro
- or read custom elements manifest file at compile time

---

# Common scenarios
- Rolling our own
- Using existing elements
- Wrapping a library

---

# Let's finally see some demos already!!

---

# Rolling our own: `<todo-list>`

---

# Out of the box [data table](https://web-components.carbondesignsystem.com/?path=/story/components-data-table--sortable-with-pagination)

---

# In which [chart.js](https://www.chartjs.org/) becomes a custom element...

---

# Bonus round: testing with wallaby

---

# Resources
- [LiveElements](https://github.com/launchscout/live_elements)
- [LiveElements Testbed project (contains all the demos)](https://github.com/launchscout/live_elements_testbed)

---