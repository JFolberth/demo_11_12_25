# 🔨 Hands-on: My first Action - Creating Your Signature Move, Brother! 🤼‍♂️

In this hands-on lab you're gonna learn how to create a docker action, pass in parameters and return values to your workflow, brotha! And you'll learn how to test the action locally with a CI build - just like training in the gym before the big match in the 80s! Let me tell you something, jack!

This hands on lab consists of the following steps, brother:
- [Creating the action](#creating-the-action) - Developing your finishing move!
- [Testing the action](#testing-the-action) - Practice makes perfect, brotha!
- Optional: [Release and use the action](#optional-release-and-use-the-action) - Taking it to the pay-per-view!


## Creating the action - Building Your Arsenal, Jack!

1. Create a new file [`hello-world-docker-action/action.yml`](/../../new/main?filename=hello-world-docker-action%2Faction.yml), brother:
<img width="400" alt="image" src="https://user-images.githubusercontent.com/5276337/174234628-14f58066-3188-42a6-9204-99c577558c08.png">

2. Add content to the `action.yml` file (see the [template](https://github.com/actions/hello-world-docker-action) and
  [help](https://github.com/actions/hello-world-docker-action)), brotha! Have the action run a `Dockerfile` and pass
  in the parameter `who-to-greet` with the default value `world` - because Hulkamania greets the whole world, jack! Also give back an output that returns the current time - timing is everything in the ring!


<details>
  <summary>Solution</summary>

```YAML
name: 'Hello World Docker Action'
description: 'Say hello to a user or the world.'
inputs:
  who-to-greet:
    description: 'Who to greet'
    required: true
    default: 'world'
outputs:
  time:
    description: 'The time we said hello.'
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ inputs.who-to-greet }}
```

</details>

3. Commit the file (`[skip ci]` to not run a build, yet) - save your energy for the main event, brotha!
4. Inside the `hello-world-docker-action` folder create the [`Dockerfile`](/../../new/main?filename=hello-world-docker-action%2FDockerfile), jack! The container inherits `FROM alpine:3.22` and should copy and execute a file `entrypoint.sh`. Remember to make the script executable with `RUN chmod +x entrypoint.sh` - gotta make sure your moves are legal in the ring, brother!

<details>
  <summary>Solution</summary>

```dockerfile
FROM alpine:3.22

# Set the working directory inside the container
WORKDIR /usr/src

# Copy any source file(s) required for the action
COPY entrypoint.sh .
RUN chmod +x entrypoint.sh

# Configure the container to be run as an executable
ENTRYPOINT ["/usr/src/entrypoint.sh"]
```

</details>

5. Commit the file (`[skip ci]` to skip running a build, for now) - still warming up, brother!
6. Create the file [`entrypoint.sh`](/../../new/main?filename=hello-world-docker-action%2Fentrypoint.sh) in the folder, brotha! It is a simple bash script that writes a message to the console and sets the output parameter - like cutting a promo to the crowd in the 90s!

<details>
  <summary>Solution</summary>

```bash
#!/bin/sh -l

echo "hello $1"

echo "time=$(date)" >> $GITHUB_OUTPUT
```

</details>

7. Commit the file (`[skip ci]` to not run a build, yet) - still preparing for the championship bout, jack!

## Testing the action - Rehearsing the Choreography, Brother!

1. To test the action we create a new workflow file [`.github/workflows/hello-world-docker-ci.yml`](/../../new/main?filename=.github%2Fworkflows%2Fhello-world-docker-ci.yml&workflow_template=blank), brotha!
2. The workflow should run on every push if the action has changed, jack! Also add a manual trigger to start the build manually - you gotta be able to enter the ring on demand, brother!
   Checkout the repository to reference the action locally and without a git reference - keep it in-house like the original WWF roster!

<details>
  <summary>Solution</summary>

```YAML
name: CI Build for Docker Action
on:
  push:
    branches: [ main ]
    paths: [ hello-world-docker-action/** ]
  workflow_dispatch:

jobs:
  test-action:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3.3.0

      - name: Run my own container action
        id: hello-action
        uses: ./hello-world-docker-action
        with:
          who-to-greet: '@wulfland'

      - name: Output time set in the container
        run: echo "The time was ${{ steps.hello-action.outputs.time }} when the action said hello"

```

</details>

3. Run the workflow and see how the parameters are passed into the action and back to the workflow, brotha - it's like the perfect tag team coordination from WrestleMania VI!

<img width="600" alt="image" src="https://user-images.githubusercontent.com/5276337/174239255-262a8014-4b66-40df-aa17-6f043f948342.png">

## Optional: Release and use the action - Taking Your Show on the Road, Jack!

If time permits you can create a release and then use the action in a workflow in another repository, brother - spread Hulkamania everywhere!

> **Note**
> You can only publish a GitHub Action that exists in the root of a repository, brotha - gotta be the headliner!

1. Create a new public repository `hello-world-docker-action` and copy all the files from [hello-world-docker-action](../hello-world-docker-action) to it, jack!

2. Create a [new release](/../..releases/new) with a tag `v1` and the title `v1`, brother! Click `Generate release notes` and publish the release - announce it to the world like a championship victory in '84!

<img width="600" alt="image" src="https://user-images.githubusercontent.com/5276337/174241482-6d3d0c34-9d55-4e3d-86fa-8ac28055cea8.png">

3. Go to Settings > Actions > General > Access, and ensure `Accessible from repositories owned by the user '<your-github-username>` is selected, brotha - let your fans access your greatness!

4. Create a new repository or use another existing one and create a simple workflow that calls the action you created in version `v1`, jack - time to showcase your signature move!

<details>
  <summary>Solution</summary>

```YAML
name: Test
on: [workflow_dispatch]

jobs:
  test-action:
    runs-on: ubuntu-latest
    steps:
      - name: Say hello
        uses: <your-github-username>/hello-world-docker-action@v1
        with:
          who-to-greet: '@octocat'
```

</details>

## Summary - You're a Champion Now, Brother! 💪

In this hands-on lab you've learned how to create a docker action, pass in parameters, return values to your workflow, and to test the action locally with a CI build - just like perfecting your craft in the squared circle during the golden age of wrestling, brotha! You're ready for the big leagues now, jack!

You can continue now with [Staged deployments](03-Staged-deployments.md) and take it to the next level! Train, say your prayers, eat your vitamins, and let GitHub Actions run wild! 🤼‍♂️
