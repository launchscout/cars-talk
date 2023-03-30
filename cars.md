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

# Beyond LiveView
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

# Beyond LiveView
### Getting the Javascript you need while keeping the LiveView you love

---

# Goals of this talk
- What are custom elements (aka Web Components)
- Why are they the best option for LiveView integration
- How to do it
- When to do it
- Fun demo codez :)

---

# Have you heard the good news about Custom Elements?
- Supported in all the browsers
- They are really are just HTML
- Stylable via CSS (to the precise extent you decide)
- No framework committment required!
- There may already be one to do what you want

---

# Why are they a good fit with LiveView
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

---

# Common scenarios
- Using existing elements
- Rolling our own
- Wrapping a library

---

## LiveView and Custom Elements: The ~~Bad Parts~~ Challenges
- Writing custom hooks is tedious
- Passing complex data
- LiveView doesn't know about Custom Events

---

# We shall overcome..
- We can serialize JSON
- `phoenix-custom-event-hook` has your back
- Don't write your own hook :)

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

# Let's finally see some demos already!!

---