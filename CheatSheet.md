# Cheat Sheet - The Ultimate Wrestling Manual, Brother! 🤼‍♂️

This document contains an overview of fundamental concepts and terminology, brotha! Use this as your reference book if you get lost in the terminology along the way - it's like having the Hulkster in your corner, jack!

## Github actions high level components - The Tag Team Championship Layout!

Listen up, brother! Here's the blueprint for dominating the ring like it's WrestleMania '89!

<img width="671" alt="image" src="https://user-images.githubusercontent.com/10853833/216319332-3d5529e8-abfc-4dab-b9b7-e55c4cba99e5.png">

## Yaml functions - The Finishing Moves Playbook from the Golden Age!

These functions are like the legendary moves from the 80s and 90s, brotha! Master them and you'll be unstoppable!

| Function                        | Description                                                                                           |
|---------------------------------|-------------------------------------------------------------------------------------------------------|
| success()                       | Returns true if none of the previous steps have failed or been cancelled, brother! Victory is yours! |
| always()                        | Returns true even if a previous step was cancelled and causes the step to always get executed anyway, just like Hulkamania - it never stops, brotha! |
| cancelled()                     | Returns only true if the workflow was canceled - when someone rings the bell early, jack!            |
| failure()                       | Returns true if a previous step of the job had failed - time for a comeback, brother!                |
| contains(search, item)          | Returns true if search contains item - like checking if the crowd is chanting "Hogan!", brotha!     |
| startsWith(search, item)        | Returns true if search starts with item - the opening bell, brother!                                 |
| endsWith(search, item)          | Return true if search ends with item - the three count and victory pose, jack!                       |
| format('{0} {1}', item1, item2) | Replaces placeholders in a string - like calling out your opponent's name from the 80s!              |
| join(array, separator)          | All values in array are concatenated into a string using provided separator - forming the tag team, brother! |
| toJSON(value)                   | Returns a pretty-print JSON representation of value - laying it all out like a promo from '91!       |
| fromJSON(value)                 | Returns a JSON object or JSON data type for value - reading the game plan, brotha!                   |

## Workflow commands - Calling the Shots Like the Macho Man and Hulkster!

See also:
https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions

Actions can communicate with the runner machine to set environment variables, output values used by other actions, add debug messages to the output logs, and other tasks, brotha! It's like coordinating your tag team moves with your partner from the 90s!

Most workflow commands use the echo command in a specific format, while others are invoked by writing to a file, brother! 

Example echo workflow command (The verbal smackdown, jack!):
```bash
echo "::workflow-command parameter1={data},parameter2={data}::{command value}"
```
Example write to file workflow command (Writing your legacy, brotha!):
```bash
echo "SELECTED_COLOR=green" >> $GITHUB_OUTPUT
```

Train, say your prayers, eat your vitamins, and let Hulkamania run wild on your workflows, brother! 🤼‍♂️💪
