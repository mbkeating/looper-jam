# looper-jam
Real-time music collaboration

## Problem
Musicians love to collaborate and jam. Jams in-person work great, but every video/audio/whatever chat has latency issues. Music is extremely sensitive to timing, and even a small difference in the played offset of a note compared to what everyone else hears can be impactful. I avoid this problem by emailing my recorded parts asynchronously to my producer. However, music benefits immensely from real-time collaboration, where artists can bounce ideas off each other and hear the music they create together. We need to solve this latency issue for remote music collaboration to happen in real-time.

## Proposed Solution
We can solve the latency issue by utilizing loops. Recording musicians, myself included, use loops to iterate over multiple ideas. Most (if not all) digital audio workstations have some looping feature where the artist can select a section to repeat indefinitely. We can utilize a client-server star model that I'll call a musician-producer model (I don't mean to imply that producers are not musicians, I just liked the name). The producer will connect to all musicians through a web socket.
![Producer-musician](https://github.com/user-attachments/assets/ad1f9042-7d8e-4257-9e29-8ea6463a798e)

The producer will create a track with a certain length and beats per minute. Then, the musicians can contribute one at a time round-robin style. Each cycle the producer will broadcast the current total track to all musicians. The current contributing musician will play along and stream their playing (as a sampled audio waveform) to the producer alongside a total track alignment timestamp (aligning the musician's contribution to the start of the total track). Then, the producer will align the musician's contribution with the total track and broadcast again with the next musician in the cycle getting the chance to play.
![producer-musician-2](https://github.com/user-attachments/assets/70b6e7c1-d8a9-4e17-9a90-a5d781a6082b)
![producer-musician-3](https://github.com/user-attachments/assets/43068b13-83cd-4078-84f3-7057aceea98a)
![producer-musician-4](https://github.com/user-attachments/assets/4540302c-42c7-48a5-b082-8d986c6d9bf7)
