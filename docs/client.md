# SlackSocket Client

To instantiate a `SlackSocket` class that will setup an RTM websocket:

```python
from slacksocket import SlackSocket
s = SlackSocket('<slack-token>')
```

**Params**:

* slacktoken (str): token to authenticate with slack
* translate (bool): yield events with human-readable user/channel names rather than id. default true

**Methods**

## get_event

Return a single event object in the order received or block until an event is received and return it.

**Params**:

* event_filter (list): Slack event type(s) to filter by. Excluding a filter returns all slack events. See https://api.slack.com/events for a listing of valid event types.

**Returns** (obj): SlackEvent object

## send_msg

Send a message via Slack RTM socket and wait for confirmation it was received. One of either channel_name or channel_id params is required.

**Params**:

* text (str): Message body to send
* channel_name(str): Name of the channel to post message
* channel_id(str): Slack ID of the channel to post message
* confirm(bool): Boolean to toggle blocking until a reply back is received from slack. default True 

**Returns** (obj): SlackMsg object

## events

Return a generator yielding SlackEvent objects

**Params**:

* event_filter (list): Slack event type(s) to filter by. Excluding a filter returns all slack events. See https://api.slack.com/events for a listing of valid event types.

**Returns** (generator): A generator of SlackEvent objects

# SlackEvent

Event object received from SlackSocket

Note: If slacksocket was instantiated with translate=True(default), user and channel IDs in the event will be replaced with their human-readable versions rather than ID. 

**Attributes**:

* type (str): The Slack API event type
* time (int): UTC epoch time that the event was received by the client
* event (dict): Dictionary of the event received from slack
* json (str): Event in JSON format

# SlackMsg

Msg created and sent via Slack RTM websocket

**Attributes**:

* time (int): UTC epoch time that the message was acknowledged as sent
* sent (bool): Boolean for message being sent successfully
* json (str): Message in JSON format
