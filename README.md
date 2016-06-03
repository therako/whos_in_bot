# WhosInBot

[![Build Status](https://travis-ci.org/col/whos_in_bot.svg?branch=master)](https://travis-ci.org/col/whos_in_bot)

WhosInBot is a Telegram bot that helps you keep track of who is attending an event within a group chat.

## Deployment

    Note: Make sure your AWS keys are set!
    
    mix edeliver build release --branch=bot_hub
    mix edeliver deploy release to production --version=0.0.x
    mix edeliver start|restart production

## Upgrade

    mix edeliver build upgrade --from=0.0.x --to=0.0.z
    mix edeliver deploy upgrade to production --version=0.0.z


## Testing (IEX)

    message = %Telegram.Message{text: "/start_roll_call", chat: %Telegram.Chat{id: 1}}
    message = Telegram.Message.set_entity(message, Telegram.Entity.new("bot_command", 0, 16))  
    message = Telegram.Message.process_entities(message)
    WhosInBot.ChatGroup.handle_message(message)

## Commands

### Basic Commands

- /start_roll_call - Start a new roll call (with optional title)
- /end_roll_call - End the current roll call
- /in - Let everyone know you'll be attending (with optional comment)
- /out - Let everyone know you won't be attending (with optional comment)
- /maybe - Let everyone know that you don't know (with optional comment)
- /whos_in - List attendees

### Other Commands

- /set_title <title> - Add a title to the current roll call
- /set_in_for <name> - Allows you to respond for another user
- /set_out_for <name> - Allows you to respond for another user
- /set_maybe_for <name> - Allows you to respond for another user
- /shh - Tells WhosInBot not to list all attendees after every response
- /louder - Tells WhosInBot to list all attendees after every response

## Usage

Simply add [@WhosInBot](https://telegram.me/whosinbot) to your group chat and send a '/start_roll_call' to start
recording who will be attending an event.

Members of the group chat can respond with '/in', '/out' or '/maybe'. They can
even provide a reason after the command. ie) '/out injured'.

Each time someone responds [@WhosInBot](https://telegram.me/whosinbot) will print the attendee list.

```
Dinner on Friday
1. Sam
2. John
2. Chris

Out
- James (on holiday)
```

You can clear all the responses and start a new roll call by sending '/start_roll_call' again.
