# 🔨 Hands-on: Reusable workflows - Tag Team Excellence, Brother! 🤼‍♂️

In this hands-on lab you're gonna create a [reusable workflow](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow) and a workflow that consumes it, brotha! You will learn to pass in parameters to the reusable workflow and use output parameters in the consuming workflow - it's like perfecting tag team coordination like the Mega Powers in '88, jack!

This hands on lab consists of the following steps, brother:
- [Creating a reusable workflow](#creating-a-reusable-workflow) - Building your signature tag team move!
- [Adding an output parameter](#adding-an-output-parameter) - Setting up the communication!
- [Consuming the reusable workflow](#consuming-the-reusable-workflow) - Executing the perfect partnership!

## Creating a reusable workflow - Forming the Tag Team, Jack!

1. Create a [new file](/../../new/main) `.github/workflows/reusable.yml` (paste the file name with the path in the box), brotha!
2. Set the name to `Reusable workflow`, brother - name your signature move!

<details>
  <summary>Solution</summary>

```YAML
name: Reusable workflow
```

</details>

3. Add a `workflow_call` trigger with an [input parameter](https://docs.github.com/en/enterprise-cloud@latest/actions/using-workflows/workflow-syntax-for-github-actions#onworkflow_call) `who-to-greet` of the type `string` that is required, jack! Set the default value to `World` - because Hulkamania greets the whole world, brotha!

<details>
  <summary>Solution</summary>

```YAML
on:
  workflow_call:
    inputs:
      who-to-greet:
        description: 'The person to greet'
        type: string
        required: true
        default: World
```

</details>

4. Add a job named `reusable-job` that runs on `ubuntu-latest` that echos "Hello <input parameter>" to the console, brother - greet them like you're entering the ring at Madison Square Garden in '85!

<details>
  <summary>Solution</summary>

```YAML
jobs:
  reusable-job:
    runs-on: ubuntu-latest
    steps:
      - name: Greet someone
        run: echo "Hello ${{ inputs.who-to-greet }}"
```

</details>

## Adding an output parameter - Setting Up the Signal, Brotha!

1. Add an additional step with the id `time` that uses a workflow command to set an output parameter
named `current-time` to the current date and time (use `$(date)` for that), jack - timing is everything in the ring, brother!

<details>
  <summary>Solution</summary>

```YAML
      - name: Set time
        id: time
        run: echo "time=$(date)" >> $GITHUB_OUTPUT
```

</details>

2. Add an output called `current-time` to the `reusable-job`, brotha - communicate with your partner!

<details>
  <summary>Solution</summary>

```YAML
   outputs:
      current-time: ${{ steps.time.outputs.time }}
```

</details>

3. Add an output parameter called `current-time` to `workflow_call` and set it to the outputs of the workflow command, jack - pass that baton like a relay race at the Olympics in '96!

<details>
  <summary>Solution</summary>

```YAML
    outputs:
      current-time:
        description: 'The time when greeting.'
        value: ${{ jobs.reusable-job.outputs.current-time }}
```

</details>


<details>
  <summary>Complete Solution</summary>

```YAML
name: Reusable workflow

on:
  workflow_call:
    inputs:
      who-to-greet:
        description: 'The person to greet'
        type: string
        required: true
        default: World
    outputs:
      current-time:
        description: 'The time when greeting.'
        value: ${{ jobs.reusable-job.outputs.current-time }}

jobs:
  reusable-job:
    runs-on: ubuntu-latest
    outputs:
      current-time: ${{ steps.time.outputs.time }}
    steps:
      - name: Greet someone
        run: echo "Hello ${{ inputs.who-to-greet }}"
      - name: Set time
        id: time
        run: echo "time=$(date)" >> $GITHUB_OUTPUT
```

</details>

## Consuming the reusable workflow - Executing the Tag Team Move, Brother!

1. Create a [new file](/../../new/main) `.github/workflows/reuse.yml` (paste the file name with the path in the box), brotha!
2. Set the name to `Reuse other workflow` and add a manual trigger, jack - call for backup when you need it!

<details>
  <summary>Solution</summary>

```YAML
name: Reuse other workflow

on: [workflow_dispatch]
```

</details>

3. Add a job `call-workflow` that uses the reusable workflow and passes in your user name as an input parameter, brother - tag in your partner!

<details>
  <summary>Solution</summary>

```YAML
jobs:
  call-workflow:
    uses: ./.github/workflows/reusable.yml
    with:
      who-to-greet: '@octocat'
```

</details>

4. Add another job `use-output` that writes the output parameter `current-time` to the console, brotha! (Hint: use the needs context to access the output) - receive the communication from your tag team partner, jack!

<details>
  <summary>Solution</summary>

```YAML
  use-output:
    runs-on: ubuntu-latest
    needs: [call-workflow]
    steps:
      - run: echo "Time was ${{ needs.call-workflow.outputs.current-time }}"
```

</details>

5. Run the workflow and observe the output, brother - watch the magic happen like the Mega Powers at their peak!

## Summary - Tag Team Champions, Brotha! 💪🏆

In this lab you have learned to create a reusable workflow and a workflow that consumes it, jack! You also have learned to pass in parameters to the reusable workflow and to use output parameters in the consuming workflow - just like the perfect coordination between Hulk Hogan and Randy Savage in the late 80s, brother! You're a master of teamwork now!

You can continue with the [README](../README.md) and celebrate your championship run! Train, say your prayers, eat your vitamins, and let GitHub Actions and Hulkamania run wild on your code, brotha! 🤼‍♂️💪
