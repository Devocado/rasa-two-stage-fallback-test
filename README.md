# Rasa 2.0.0 two-stage fallback test

This repo is a small example to reproduce a bug in Rasa 2.0.0 two-stage fallback.

### The assistant asks for your
- name
- age
- favourite colour
and fills a slot with each.

The two-stage fallback clears all of the slots when it rewinds

## Steps to reproduce:

- Start the assistant
- Enter 'Hi' or 'hello' to start a conversation
- Provide the information requested, a name, a number for age, and a colour
- When the assistant asks 'what can I do for you?' enter
```
/nlu_fallback
```
to trigger an nlu fallback (just for the sake of simplicity; with so few intents it is tricky to trigger it with an ordinary message)
- The assistant will ask "did you mean 'nlu_fallback'?". Select 'No'
- The assistant will ask you to rephrase your message. This time enter something along the lines of "tell me a joke" to trigger the `tell_joke` intent

The assistant will answer, using the `name` slot. However the slot will be empty, and will output 'None' where the name should be.

Running in debug mode will reveal that all of the slots are empty at this point
