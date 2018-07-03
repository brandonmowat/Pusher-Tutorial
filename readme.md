This tutorial assumes that you already know how the chatkit server works.
Form more information on setting up your environment, check out [this tutorial](https://github.com/bookercodes/pusher-chatkit-tut).

Intro:
Building a chat application is not trivial and time consuming, even with ChatKit. That's why I wrote `react-chat-ui`. `react-chat-ui` handles all the chat interface logic for you. In this tutorial, I'll go through the setup of `react-chat-ui` with your ChatKit app.

For simplicity sake, I'm not going to go over setting up your Pusher Account and instance.
They already have great documentation on that over [here]()

## ...Some Setup and Configuration Goes Here...

install react-chat-ui

I'm going to assume you have a `source` or `src` folder that contains your `app.js` or `main.js` file. This is where you're going to write your chat application.

Let's add a nifty little method to our `App` component:

```JavaScript
  connectToChatManager(userId) {
    this.chatManager = new ChatManager({
      instanceLocator: [YOUR_INSTANCE_LOCATOR],
      userId,
      tokenProvider: new TokenProvider({
        url:
          'https://us1.pusherplatform.io/services/chatkit_token_provider/v1/[YOUR_CHAT_TOKEN]/token',
      }),
    })

    this.chatManager
      .connect()
      .then(currentUser => {
        this.setState({ currentUser })
        this.joinRoom(currentUser)
      })
      .then(currentRoom => {
        this.setState({ currentRoom })
      })
      .catch(err => {
        console.log('Error on connection', err)
      })
  }
```	