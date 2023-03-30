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

# Agenda
- What are custom elements (aka Web Components)
- Why are they the best option for LiveView integration
- How to do it
- When to do it
- Fun demo codez :)

---

# Common scenarios
- Using existing elements
- Rolling our own
- Wrapping a library

---

# What are the "out of the box" options?
- LiveView hooks
- JS commands
- both are IMO, kinda clunky

---

## Have you heard the good news about Custom Elements?
- Supported in all the browsers
- They are really are just HTML
- Stylable via CSS (to the precise extent you decide)
- No framework committment required!
- There may already be one to do what you want

---

# Custom element guidance
- Pass information in as attributes/props
- Send information out using events
- Custom events are your friend!
- Libraries like Lit can help

---

# Ok cool let's use em! Not (quite) so fast
- Your custom element probably dispatches custom events
- You might have want to give your elements some complex data

---

# NBD
- We can serialize stuff as JSON
- We can use `phoenix-custom-event-hook` to listen to custom events

---

## But wouldn't it be nice if our custom elements magically became functional components?

---

# Meet LiveElements

---

# Scenario the second
I want to take my custom element on the road!

---
# Specifically...
- What if my app isn't hosted by phoenix
- A statically generate site mebbe (eg launchscout.com)
- I'd like to interactive functionality
- How to?

---

# Meet LiveState

---
