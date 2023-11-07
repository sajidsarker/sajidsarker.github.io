---
layout: post
title: Stateless Dialogue Tree
date: 2023-11-06 04:51:00
tags: [Game Design, Python, Videogame]
---
## Stateless Dialogue Tree

I enjoy role-playing games greatly, and have been getting into the wonderful **Baldur's Gate 3**. It's a stellar example of technical and artistic craftsmanship, and deserving of all the good reviews garnered for its gameplay and writing.

What I enjoyed the most are the extensive dialogue trees in Baldur's Gate. Originally, a mainstay of old 90s CRPGs, the mechanic has popped up in modern games like Mass Effect, episodic TellTale Games, and Disco Elysium for deep narratives and NPC interaction.

I'll be detailing a simple implementation of a stateless dialogue tree running in the command line. Stateless implies that no conditional quest-related flags are used to trigger the entry point to a particular conversation or branch. This can be a feature worth extending the provided code on.

### Class: Conversation Manager

The *Conversation Manager* class processes a dictionary of conversations, which are each dictionaries holding all the dialogue constituting a conversation.

```python
#!/usr/bin/python3

from typing import Dict
from dialogue import *

class ConversationManager:
    conversations: Dict[str, Dict[int, Dialogue]]
    conversation_id: str

    def __init__(self, conversations: Dict[str, Dict[int, Dialogue]]) -> None:
        self.conversations = conversations
        for conversation in self.conversations:
            for dialogue in self.conversations[conversation]:
                self.conversations[conversation][dialogue].instancer = self

    def play(self, conversation: str) -> None:
        self.conversation_id = conversation
        self.conversations[self.conversation_id][0].play()
```

### Class: Dialogue

The *Dialogue* class held in the dictionary of conversations are dependent on the existence of the calling *Conversation Manager*. Each *Dialogue* instance has an assigned speaker, an action prompt, and the content of dialogue. 

```python
#!/usr/bin/python3

from typing import List

class Dialogue:
    speaker: str
    prompt: str
    content: str
    choices: List

    instancer = None

    def __init__(self, speaker: str, prompt: str, content: str, choices: List[int]) -> None:
        self.speaker = speaker
        self.prompt = prompt
        self.content = content
        self.choices = choices

    def play(self) -> None:
        print('{}: {}'.format(self.speaker, self.content))

        i: int = 0
        for choice in self.choices:
            print('[{}] {}'.format(str(i + 1), self.instancer.conversations[self.instancer.conversation_id][choice].prompt))
            i += 1

        if len(self.choices) > 1:
            choice: int = int(input('?'))
            choice = max(0, min(choice, len(self.choices)))
            choice -= 1
        else:
            choice: str = input('?')
            choice: int = 0

        if len(self.choices) > 0:
            self.instancer.conversations[self.instancer.conversation_id][self.choices[choice]].play()
        else:
            self.instancer.conversation_id = ''
```

### Entry Point

We simply pass the dialogue tree as a conversation to the *Conversation Manager*. We can pass multiple conversations in this manner, referencing which one to play after the fact.

```python
#!/usr/bin/python3

from conversation_manager import *

def main():
    conversation_manager = ConversationManager(
        {
            'conversation_0': {
                0: Dialogue('Narrator', 'START >>', 'Before you is a computer. What do you do?', [1, 2, 3]),
                1: Dialogue('Narrator', 'Turn on the computer.', 'It did not respond and stays inert.', [4]),
                2: Dialogue('Narrator', 'Check if the lid is warm.', 'It seems cold, like it has not been turned on in some time.', [4]),
                3: Dialogue('Narrator', 'Call tech support on your phone.', 'The line is busy and the call ends.', [4]),
                4: Dialogue('Narrator', 'CONTINUE >>', 'There is nothing to be done.', [])
            }
        }
    )

    conversation_manager.play('conversation_0')

if __name__ == '__main__':
    main()
```
