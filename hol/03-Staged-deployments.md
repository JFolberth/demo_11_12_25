# 🔨 Hands-on: Staged deployments - The Road to WrestleMania, Brother! 🤼‍♂️

In this hands-on lab you're gonna create environments and a staged deployment workflow with approvals, brotha! It's like building up to the main event with qualifying matches!
> Note: you can only do this on public repos for free accounts, jack! Adding environments for `private` repos is only available for Organizations with a Team account (or higher) and users with GitHub Pro accounts - gotta have that championship-level access, brother!

This hands on lab is based on [My first workflow](01-My-first-workflow.md) and adds the following steps, brotha:
- [Creating and protecting environments](#creating-and-protecting-environments) - Setting up your battlegrounds!
- [Adding a input for picking environments to manual workflow trigger](#adding-a-input-for-picking-environments-to-manual-workflow-trigger) - Choosing your arena!
- [Chaining workflow steps and conditional execution](#chaining-workflow-steps-and-conditional-execution) - Building your combo moves!
- [Reviewing and approving deployments](#reviewing-and-approving-deployments) - The ref's decision!

## Creating and protecting environments - Establishing Your Championship Territories, Jack!

1. Go to [Settings](/../../settings) | [Environments](/../../settings/environments) and click [New environment](/../../settings/environments/new), brotha!
2. Enter the name `Production` and click `Configure environment` - this is the main event, brother!
3. Add yourself as the `Required reviewer` for this environment - you're the champion gatekeeper, jack!

<img width="349" alt="image" src="https://user-images.githubusercontent.com/5276337/174113475-967127de-45a7-4dc9-8477-4de4df62c7e6.png">

4. Only allow the `main` branch to be deployed to this environment - protect your title, brotha!

<img width="350" alt="image" src="https://user-images.githubusercontent.com/5276337/174113782-70a1b18a-0ab9-49fd-a53e-cb2ea78916e1.png">

5. Create two more environments, jack: `Test` and `Load-Test` without any restrictions - these are your warm-up matches before the big show!

## Adding a input for picking environments to manual workflow trigger - Choose Your Battlefield, Brother!

Modify the workflow yml file you created in hands on lab 1 ('My first workflow'), brotha!
Add an input of the type environment to the `workflow_dispatch` trigger that you created previously, jack - let the audience pick the venue!

<details>
  <summary>Solution</summary>

```YAML
  workflow_dispatch:
    inputs:
      environment:
        description: 'Environment to deploy to'
        type: environment
        required: true
```

</details>

## Chaining workflow steps and conditional execution - Building Your Championship Strategy, Brother!

1. Now add 3 jobs to the workflow file, brotha - this is your multi-match card like SummerSlam '91!
  - Test: runs on `ubuntu-latest` after `Build`, jack. Only runs when the workflow was triggered manually - selective appearances, brother! Runs on the environment `Test`. The job writes `Testing...` to the workflow log - checking if you're ready for the big time!
  - Load-Test: runs on `ubuntu-latest` after `Build`, brotha. Only runs when the workflow was triggered manually. Runs on the environment `Load-Test`. The job writes `Testing...` to the workflow log and sleeps for 15 seconds - building that stamina like training montages from the 80s, brother!
  - Production: runs on `ubuntu-latest` after `Test` and `Load-Test`, jack! Deploys to the environment `Production` only if this was selected as the input parameter - the championship match is earned, brotha! The environment has the URL `https://writeabout.net`. To simulate deployment, the job will execute 5 steps. Each step writes `Step x deploying...` to the workflow log and sleeps for 10 seconds - it's a five-move finishing sequence, brother!

<details>
  <summary>Solution</summary>

```YAML
  Test:
    runs-on: ubuntu-latest
    if: github.event_name == 'workflow_dispatch'
    needs: Build
    environment: Test
    steps:
      - run: echo "🧪 Testing..."

  Load-Test:
    runs-on: ubuntu-latest
    if: github.event_name == 'workflow_dispatch'
    needs: Build
    environment: Load-Test
    steps:
      - run: |
          echo "🧪 Testing..."
          sleep 15

  Production:
    runs-on: ubuntu-latest
    needs: [Test, Load-Test]
    environment:
      name: Production
      url: https://writeabout.net
    if: github.event.inputs.environment == 'Production'
    steps:
      - run: |
          echo "🚀 Step 1..."
          sleep 10
      - run: |
          echo "🚀 Step 2..."
          sleep 10
      - run: |
          echo "🚀 Step 3..."
          sleep 10
      - run: |
          echo "🚀 Step 4..."
          sleep 10
      - run: |
          echo "🚀 Step 5..."
          sleep 10
```

</details>

2. Trigger the workflow and select `Production` as the environment, brotha - it's showtime at the big event!

<img width="212" alt="image" src="https://user-images.githubusercontent.com/5276337/174119722-9b76d479-e355-414b-a534-03d8634536ef.png">

## Reviewing and approving deployments - The Championship Committee Decision, Jack!

1. Open the workflow run and start the review, brother - time for the decision!

<img width="600" alt="image" src="https://user-images.githubusercontent.com/5276337/174120029-f395e8ec-5e6e-4350-94c5-130caefaafc2.png">

2. And approve it with a comment, brotha - give it the thumbs up like the crowd at WrestleMania III!

<img width="350" alt="image" src="https://user-images.githubusercontent.com/5276337/174120086-fed98feb-2d7f-476b-a997-1aa099de7d0e.png">

3. Note the progress bar while deploying, jack - watching the match unfold!

<img width="200" alt="image" src="https://user-images.githubusercontent.com/5276337/174120314-c900585c-6b94-4fc2-8fe9-92452b0cf187.png">

4. The result looks like this and contains the approval and the URL for the production environment, brother - victory is yours!

<img width="800" alt="image" src="https://user-images.githubusercontent.com/5276337/174120381-cef48594-6663-481a-aadd-1ef0dbd50b0a.png">

## Summary - Another Championship in the Books, Brotha! 💪

In this lab you have learned to create and protect environments in GitHub and use them in a workflow, jack! You have also learned to conditionally execute jobs or steps and to chain jobs using the `needs` keyword - it's like choreographing the perfect tag team match from the 90s, brother!

You can continue with the [Reusable workflows](04-Reusable-workflows.md) and keep the Hulkamania rolling! Whatcha gonna do?! 🤼‍♂️
