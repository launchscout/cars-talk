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
* Slightly fossilized web developer (full stack)
  * Perl in the 90s
  * Java in the naughties
  * Ruby in the 10s
  * Elixir nowadays
  * and Javascript (almost) the whole time :)
* Co-Founder, Launch Scout
---
<!-- footer: ![](full-color.png) -->
# What's an Embedded Web App?
* Adds functionality to a larger application
* Examples
  * Live support
  * Buy button
  * Comments
  * Surveys
* You could also lump in Micro Front Ends

---

# Current state of the art
* Third party javascript
* Often `iframe` based
* Proprietary, limited customization

---

# There's a better way
* Custom Elements are here
* Supported by all the browsers
* Superior customization options
* The right tool for the job!

---

# Great Developer Experience
* Your website is already made of HTML
* No framework commitment required!
* Superior customization
  * Shadow parts
  * Slots

---

# Example time!

---

# What about the backend?
* Typically JS calling API
* REST vs GraphQL
* Managing state on both tiers :(
* Building two apps :(

---

# Here is my crazy dream:
* State on the server is the source of truth
* Client code:
  * renders the current state
  * dispatches events to the server
  * receives state updates

---

# How do I get there? LiveState!
* npm package for the client (phx-live-state)
* Elixir library for the server (live_state)
  * a tiny process for the state of each conversation
  * lots of messages over WebSockets
  * Elixir makes this practical

---

# Introducing `phx-live-state`
* javascript (typescript) npm
* increasing levels of abstraction:
  * `LiveState` - lower level API
  * `connectElement()` allows you to "wire up" a Custom Element
  * `@liveState` TS decorator lets you declaratively annotate a Custom Element class

---

## `@liveState` typescript decorator
* decorates a Custom Element class
* takes a single `object` param
  * url: (optional, defaults to `url` prop of element)
  * channelName: (optional, defaults to `channelName` prop on element)
  * properties - list of properties to set from state
  * attributes - list of attributes to set from state
  * events
    * send - Custom Events to send from this element
    * receive - Custom Events to receive and then dispatch on this element

---

## Server side LiveState: The Event/State reducer pattern
* Functional pattern for managing state
* Redux
* Elm
* (etc)

---

# Key elements
* Events
  * Name, payload
* State
* Reducers: functions which take
  * event
  * current state
  * return a new state

---

# Does this seem familiar?
* Redux
* Elm
* `GenServer`
* LiveView

---

# Our example project: `<stripe-cart>`
## The scenario:
* You have website that is just plain old html files
* You want to add a truly interactive shopping cart experience
* What would we need?

---

# Two custom elements
* `<stripe-cart>`
  * Displays cart.
  * Pops a modal for details
  * Checkout button redirects to stripe to complete the checkout session
* `<stripe-cart-additem>`
  * Adds an item to the cart. Takes a price id as an attribute.

---

Let's see it!

---

Launch Elements: `<stripe-cart>` all growed up

---

# Future possible things
* Very soon:
  * ~~jsonpatch for efficient state management~~
  * authorization hook and example
* Other clients
  * Swift/iOS
  * Kotlin/Android
  * React
* Connecting to FAAS

---

# It's early times!
* APIs may still change
* It's great time to join us if you want to help them be better :)
* If you are building an embedded or micro front end app, let's talk
  * chris@launchscout.com

---

# Links:
* live_state elixir library: https://github.com/launchscout/live_state
* phx-live-state client npm: https://github.com/launchscout/live-state
* discord-element front end: https://github.com/launchscout/discord-element
* discord-element back end: https://github.com/launchscout/discord_element
* [Live comments demo](https://launchscout.github.io/test-livestate-comments/)

---
 
![h:400px](https://cdn.discordapp.com/attachments/564951236311253042/1012446048599416903/qr-chris-elixirconf-22.png)
### github.com/launchscout/elixirconf_2022_livestate

---
