# Animalise

Animalise is a simple reimplementation of the sound system used for dialogues in Animal Crossing.
This repository is based on the explanations from [this video](https://www.youtube.com/watch?v=t_jFVcA-ZsQ).

See it live at: https://wally869.github.io/Animalise/

## Dependencies

CSS: Tailwind  
JS: Howler

Sounds are handled as URI with Howler. Both dependencies are downloaded from a CDN.

## How does it work

We used the mp3 files provided by [the author of the video](https://www.reddit.com/r/Unity3D/comments/gvkwg8/how_to_make_animalese_animal_crossings_language/fsr3rup?utm_source=share&utm_medium=web2x), encoded them as data URI. These sounds were then mapped to their respective character tokens.

On the website the user inputs a target sentence, from which we prune whitespaces and unused characters, in order to only keep characters of interest in an array.

Finally, from this array of characters, we create an array of Howl objects, with the onEnd callback calling the next Howl object once the sound has finished playing.

The onEnd callback also registers the currently playing Howler in the higher scope. This allows us to check whether an Howl is currently playing and stop it before processing the new sentence.

## Improvements

We wanted to create a quick and dirty implementation, with no need for a server. There are obvious improvements one could make one this small project

- Current implementation uses multiple Howl objects, which has a non-trivial cost in memory. A better approach would be to get access to the data of the sound file, concatenate the data from the different sounds, create a new URI and play it.

- Base sounds are not the best quality. One could spend more time and effort on recording and editing.
