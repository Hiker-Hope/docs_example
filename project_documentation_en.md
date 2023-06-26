# My greatest game project


## Responsible

The project is run and supported by the R&D team.

## Contents
1. [🎬Work with the project](#work-with-the-project)
2. [📝Work with the repository](#work-with-the-repository)
3. [🎨StyleGuide](#styleguide)
4. [📒Storybook](#storybook)

### 🎬Work with the project 

1. Install the dependencies:

```bash
yarn
```

#### 💻Start

1. Start the local mockup backend:
```bash
yarn dev 
```

2. Then **in a new tab** start the WDS:

```bash
yarn start 
```
The backend will be running on `http://localhost:3000/`

WDS  will be running on `http://localhost:3333/`

#### 🧱Build
```bash
yarn build
```


#### ✅Unit testing
The project uses [Jest](https://jestjs.io/) for unit testing.

To launch the tests run:
```bash
yarn test
```

All the utils should be covered by unit tests.

The test file (`*.test.ts`) should be kept next to the file of the function which it covers.

Example:
```
├── utils/
│   ├── countSomething.ts/
│   ├── countSomething.test.ts/
```


### 📝Work with the repository

1. Get a task in Jira 
2. Start a new branch from `main` named in the format `<github-username>_<task-number>`.

   E.g., for a username `rnd-coder` and the task `RND-1432` the branch will be named `rnd-coder_RND-1432`. 
3. After finishing the code, create a new PR into `main` titled in the format  `<task-number>: Краткое описание задачи`.

   E.g., for a task `RND-1432` with a loader fix PR should be titled `RND-1432: Fix loader`. 
4. In order to merge with the `main` branch we should squash the commits into one (button `Squash and merge`) and write a single-line commit message, equal to the PR title.


### 🎨StyleGuide

The styleguide with the main codestyle agreements can be found [here](https://github.com/Hiker-Hope/docs_example/blob/master/styleguide.md).

## 📒Storybook

We use [Storybook](https://storybook.js.org/) for faster and more convenient common components decelopment.

It accumulates all the files with the extension `.stories.ts|tsx`.

To launch Storybook run:

```
yarn storybook
```

By default, Storybook will be running on port 6006.

