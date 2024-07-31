# looper-jam
Real-time music collaboration

## Problem
Musicians love to collaborate and jam. Jams in-person work great, but every video/audio/whatever chat has latency issues. Music is extremely sensitive to timing, and even a small difference in the played offset of a note compared to what everyone else hears can be impactful. I avoid this problem by emailing my recorded parts asynchronously to my producer. However, music benefits immensely from real-time collaboration, where artists can bounce ideas off each other and hear the music they create together. We need to solve this latency issue for remote music collaboration to happen in real-time.

## Proposed Solution
We can solve the latency issue by utilizing loops. Recording musicians, myself included, use loops to iterate over multiple ideas. Most (if not all) digital audio workstations have some looping feature where the artist can select a section to repeat indefinitely. We can utilize a client-server star model that I'll call a producer-player model. The producer will connect to all players through a web socket.
![Producer-musician](https://github.com/user-attachments/assets/ad1f9042-7d8e-4257-9e29-8ea6463a798e)

The producer will create a track with a certain length and beats per minute. Then, the players can contribute one at a time round-robin style. Each cycle the producer will broadcast the current total track to all players. The current contributing player will play along and stream their playing (as a sampled audio waveform) to the producer alongside a total track alignment timestamp (aligning the musician's contribution to the start of the total track). Then, the producer will align the player's contribution with the total track and broadcast again with the next player in the cycle getting the chance to play.
![producer-player](https://github.com/user-attachments/assets/3d022e8f-f396-43d7-a49d-f828f314143f)
