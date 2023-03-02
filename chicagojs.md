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

# Hey! You got your web app in my web app!
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

# Agenda
- What's an Embedded Web App?
- A better approach for building them
- Shopping cart example
- And then again on steroids :)

---
<!-- footer: ![](full-color.png) -->
# What's an Embedded Web App?
- Adds functionality to a larger application
- Examples
  - Contact form
  - Job app
  - Survey
  - Comments
  - Buy button
- You could also lump in Micro Front Ends

---

# Current state of the art
- Third party javascript
- Often `iframe` based
- Proprietary, limited customization

---

# There's a better way
- Custom Elements are here
- Supported by all the browsers
- Superior customization options
- The right tool for the job!

---

# Great Developer Experience
- Your website is already made of HTML
- No framework commitment required!
- Superior customization
  - Shadow parts
  - Slots

---

# Custom elements [crash course](custom_elements1.html) :)

```js
class ChicagoJSElement extends HTMLElement {
  connectedCallback() {
    this.attachShadow({mode: 'open'});
    this.shadowRoot.innerHTML = `
      <style> div { color: blue; } </style>
      <h1 part="header">Hi Chicago JS!</h1>
      <div>It's great to meet you! </div>
    `;
  }
}
window.customElements.define('chicago-js', ChicagoJSElement);
```
---

# Slots and Parts, [oh my!](custom_elements2.html)
- `<slot></slot>` in a shadow DOM, will render inner tag content
- `<div part="foo"></div>` allows external CSS to style this 

---

# [Litelement](lit.dev)
- A very small library to make Custom Elements even easier
- properties bound to attributes that trigger re-renders
- nice templating syntax
- If you don't like it there are X hundred others :)

---

# What about the backend?
- Typically JS calling API
- REST vs GraphQL
- Managing state on both tiers :(
- Building two apps :(

---

# Here is what I'd like:
- State on the server is the source of truth
- Client code:
  - renders the current state
  - dispatches events to the server
  - receives state updates (and other events)

---

# How do I get there? LiveState!
- npm package for the client (phx-live-state)
  - sends (and receives) custom events over WebSockets
  - receives state updates
  - (optionally) manages state on custom element props
- Elixir library for the server (live_state)
  - handle events over WebSockets
  - computes new state
  - sends state updates to clients

---

# What the heck is Elixir?
- A functional language on the Erlang VM
- Ruby inspired developer friendliness
- Really good at extremely high concurrency, high availability apps
- Excellent web app framework in Phoenix
- Channels for WebSockets

---

# Introducing `phx-live-state`
- javascript (typescript) npm
- increasing levels of abstraction:
  - `LiveState` - lower level API
  - `connectElement()` allows you to "wire up" a Custom Element
  - `@liveState` TS decorator lets you declaratively annotate a Custom Element class

---

## `@liveState` config 
- url
- topic
- optional params
- properties to manage
- events to send/receive
- provide/consume context (for sharing)

---

# Our example project: `<stripe-cart>`
## The scenario:
- You have website that uses an SSG (or just plain old html files)
- You have a stripe account with products to sell
- You want to add a truly interactive shopping cart experience
  - As in better than a one item "Buy Now" button
- What would we need?

---

# Two custom elements
- `<stripe-cart>`
  - Displays cart.
  - Pops a modal for details
  - Checkout button redirects to stripe to complete the checkout session
- `<stripe-cart-additem>`
  - Adds an item to the cart. Takes a price id as an attribute.

---

# On the server
- Stripe API key from config
- Handle events:
  - add_cart_item - updates state with new item added
  - checkout - creates checkout session w/Stripe and sends redirect event to client

---

# [Let's see it!](http://localhost:5173)

---

# Launch Elements: `<stripe-cart>` all growed up
## What would it take to "productionalize" this?
- hosting
- persisting cart
- connect your own Stripe account
- modify your cart items
- checkout message
- email receipt (thanks Stripe!)

---

# [elements.launchscout.com](https://elements.launchscout.com)

---

# Elements demo store!

---

# How you can help!
- If you are building an Embedded app, let's talk!
- Help us test Launch Elements (elements.launchscout.com)
- Tell me where I should eat dinner :)

---

# Links:
- This talk: https://github.com/launchscout/chicago-js-03-2023
- live_state elixir library: https://github.com/launchscout/live_state
- phx-live-state client npm: https://github.com/launchscout/live-state
- stripe-cart front end: https://github.com/launchscout/stripe-cart
- stripe-cart back end: https://github.com/launchscout/stripe_cart
- Launch Elements: https://github.com/launchscout/launch_cart

---
 
![h:400px](https://cdn.discordapp.com/attachments/564951236311253042/1012446048599416903/qr-chris-elixirconf-22.png)
### github.com/launchscout/elixirconf_2022_livestate

---
