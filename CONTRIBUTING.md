# Contribution Guide For REST API Playground
- [Getting started](#getting-started)
- [:beetle: Issues](#beetle-issues)
- [:hammer_and_wrench: Pull requests](#hammer_and_wrench-pull-requests)
  - [Ready to make a change? Fork the collection](#ready-to-make-a-change-fork-the-collection)
  - [Done making your changes? Make a pull request](#done-making-your-changes-make-a-pull-request)
  - [Review after submitting the pull request](#review-after-submitting-the-pull-request)
  - [Your pull request is merged!](#your-pull-request-is-merged)
- [Contribution Guide](#contribution-guide)
  - [Variables](#variables)
    - [Environment Variables](#environment-variables)
    - [Local Variables](#local-variables)
  - [Folders](#folders)
  - [APIs](#apis)
  - [Workflows](#workflows)
- [Reviewing](#reviewing)
  - [Self review](#self-review)
  - [Comments](#comments)
## Getting Started

Before you begin:
- Be sure to create an account in [postman](https://www.postman.com/) if you don't already have one.
  If you are unfamilar with the postman interface be sure to checkout the [learning center in postman](https://learning.postman.com/docs/getting-started/introduction/).
- Read the [code of conduct](CODE_OF_CONDUCT.md)?
- Check out the [existing issues](https://github.com/MicroStrategy/rest-api-playground/issues).
- Check out this [video](https://www.youtube.com/watch?v=cIDhJpA_5Qk) to get started with our REST API Playground.

## :beetle: Issues

If you've found something in the content or the collection that should be updated, search open issues to see if someone else has reported the same thing. If it's something new, open an issue [here](https://github.com/MicroStrategy/rest-api-playground/issues). We'll use the issue to have a conversation about the problem you want to fix.

## :hammer_and_wrench: Pull requests

We handle pull requests in [postman](https://www.postman.com/microstrategysdk).

A [pull request](https://learning.postman.com/docs/collaborating-in-postman/version-control/#creating-pull-requests) is a way to suggest changes in our REST API Playground.

When we merge those changes, they will be available for everyone to see and use.

### Ready to make a change? Fork the collection

[Fork](https://learning.postman.com/docs/collaborating-in-postman/version-control/#creating-a-fork) the collection you want to make changes to.

We recommend forking to a private [workspace](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/creating-workspaces/) while you work on your changes. You can move it to a public workspace when you are done making your changes.

The naming convention of the fork is not enforced, however we recommend naming the fork after the folder you are modifying/adding. If you are modifying/adding more than folder name it after the type of change you are making.

If you have your changes in a non forked collection, make the changes in the forked collection. You can do this manually or by dragging and adding/replacing the apis or folders you made changes to/for. 

See [Contribution Guide](#contribution-guide) for details on the specifics on the conventions and changes you should make.

### Done making your changes? Make a pull request

To [make a pull request](https://learning.postman.com/docs/collaborating-in-postman/version-control/#creating-pull-requests), your forked collection must be in a public workspace. If your forked collection is not in a public workspace, you need to [move the collection to the public workspace](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/managing-workspaces/#moving-elements-to-workspaces). 

Next follow these conventions for filling out the pull request:
- Title the pull request apprioriately based on the change being made and follow [code of conduct](CODE_OF_CONDUCT.md).
- Have a description of the changes you make so we understand what the pull request is doing.
- Put MicroStrategy Developer as the reviewer.

### Review after submitting the pull request

- Once you submit your PR, we will review it. But, the first thing you're going to want to do is a [self review](#self-review).
- After that, we may have questions, check back on your PR to keep up with the conversation.

### Your pull request is merged!

Congratulations! The whole MicroStrategy community thanks you. :sparkles:

## Contribution Guide

As you make changes keep the following in mind: 
1. If the api is not available publicly, we will not add the api workflow in playground.
2. All the workflow in playground should be ready to use in demo or brand new cloud environment without server side setup.
3. Exception to (2), if the workflow requires some configuration, we should clearly document the requirement in documentation.

### Variables

There are many different types of [variables](https://learning.postman.com/docs/sending-requests/variables/) available in postman. In our playground, we use environment variables and local variables.

#### Environment Variables

Environment variables are scoped to the [environment](https://learning.postman.com/docs/sending-requests/managing-environments/) you selected. We provide two environments in our playground. One is the [demo environment](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/environment/16131298-aac3a1ea-b878-488a-bf80-f4dc5f50a831) and the other is a [template](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/environment/16131298-531df55b-93e4-4911-a93d-6d853455e9c5) for a new cloud environment.

In these environments, we provide some long-lived environment variables such as:
- baseUrl
- projectId
- username
- password
- loginMode
Please use these long-lived environment variables over creating your own, whenever possible.
Note: In the template environment, please change these values to suit your environment.

Environment variables are used to store values that may be used across more than one apis or workflows. For PRs that add/modify content from our collections, you can create/edit these variables through [pre-request scripts and tests](https://learning.postman.com/docs/sending-requests/managing-environments/#setting-environment-variables-from-scripts).

For environment variable naming convention and usage:
1. We adopt camelCase for variable names.
  An example can be "`dossierId`" instead of "`DossierID`".
2. We enforce a "rd_" prefix to runtime generated environment variables(set inside test scripts or pre-request scripts).
  An example can be "rd_instanceId". This variable is set in the test script of an instance creation api.
3. We do not have a "rd_" prefix to long-lived environment variables nor using non-runtime environment variables.
  An example can be "`dossierId`" instead of "`rd_dossierId`" because we plan to use the provided "`dossierId`" in the environment rather than the runtime generated one.
4. There are special rules that apply to each collection
  - In the [workflow](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/collection/16131298-9ba9a108-18ee-438e-8f4f-df058f265f1b) collection:
    - Use runtime environment variables and long-lived environment variables for the path/params/headers/body of api when possible.
      An example can be we will want to use "`rd_dossierId`" rather than "`dossierId`", because we can not assure the "`dossierId`" will work for every workflow. Hence, we want to generate it at runtime rather than using the existing one in environment.
  - In the [api](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/collection/16131298-15ac2bcb-1b3c-4be4-81b2-c3defec602ad) collection:
    - Use non-runtime environment variables and long-lived environment variables for GET apis' path/params/headers/body when possible.
      An example can be using "`dossierId`" instead of "`rd_dossierId`" and "`rd_instanceId`" instead of "`instanceId`". In our pre-request script, we will change the "`dossierId`" to "`rd_dossierId`" at runtime automatically if "`dossierId`" is empty, so you can still set in pre-request or test-scripts the "`rd_dossierId`" if the "`dossierId`" was not provided in the environment. Meanwhile for "`rd_instanceId`", the "`instanceId`" can not be provided in non-runtime(it's different every time) hence the "rd_" prefix.
    - Use runtime environment variables and long-lived environment variable for apis that will edit(POST, PUT, DELETE, PATCH) in path/params/headers/body when possible
      An example can be using "`rd_dossierId`" instead of "`dossierId`" for a deletion api, we don't want users accidentally deleting one of the default provided dossiers in environment. Hence, we make them have to manually change it to "`dossierId`" or delete a runtime created one.

#### Local Variables

[Local variables](https://learning.postman.com/docs/sending-requests/variables/#variable-scopes) are scoped to the api or request script. They are no longer avaiable once the run is complete. In our playground, we use it in the test scripts to simplify and parse response jsons.

For local variable naming convention and usage: 
1. Use it when it is only going to be used in that single request/api and if it makes it easier to get the information you want
2. Have a name that makes sense(no particular requirement)

### Folders

- The title of the folder should be in "Title Case". "This is an Example".
- Each folder under the collection should have a description describing the contents under it.
- Folders can have folders nested within it.
- If the folder is based on an existing page in API docs try to structure it similar to the docs. Though you can simplify workflows if they feel redundant.
- You can set variables in the pre-request script if it applies to everything in folder.

### APIs

- The title of the API in postman should be in sentence case. "Get this example".
- In the test script, you can set variables like the id of a response object. And try to have a test script for each api even if not storing variables just to show what is the proper response like "pm.response.to.have.status(201);"
- Try to label what params or headers are required or not.
- Have description for each field.
- Exceptions/special cases:
  - In the [workflow](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/collection/16131298-9ba9a108-18ee-438e-8f4f-df058f265f1b) collection:
    - The title of api does not need to be the same as in the swagger docs.
    - Use "Login" instead of "Returns Authorization Token"
    - Use "Logout" instead of "Close all existing sessions for the authenticated user"
    - APIs do not need all optional params or headers. This is optional.
  - In the [api](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/collection/16131298-15ac2bcb-1b3c-4be4-81b2-c3defec602ad) collection:
    - The title of the api should match the swagger docs.
    - APIs should contain all optional params or headers.

### Workflows

- Workflows, based on existing documentation, should try to match/structure based on the documentation.
  Workflows, not based on existing documentation, should have a more thorough description. If the workflow cuts across multiple different api families, put the workflow in a folder that pertains most closely to the workflow or create a new folder, if no folder matches it close enough.
- Workflows should work either in a demo environment or newly created cloud environment. If setup is needed include it in documentation.
- Don't cause permanent unrevocable changes in a workflow without user explicitly editing the workflow.
  This means: 
  - Most of time you want to create a new object to showcase editing/modification workflow.
  - Delete any created objects at the end of workflow to clean up space.
  - Revert any changes by apis to existing objects at end of workflow.
- Try to use a folder existing in demo or newly created environment to store newly created objects. Such as `publicReportsFolderId` in environments or `publicObjectsFolderId`.
- All workflows with "Login" api should have "Logout" api, "Logout" should unset all used variables.

## Reviewing

We will review every single PR. The purpose of reviews is to create the best content we can for people who use MicroStrategy.

:yellow_heart: Reviews are always respectful, acknowledging that everyone did the best possible job with the knowledge they had at the time.
:yellow_heart: Reviews discuss content, not the person who created it.
:yellow_heart: Reviews are constructive and start conversation around feedback.

### Self review

You should always review your own PR first.

For changes, make sure that you:

- [ ] Pull the latest changes from the source to confirm the changes will have the expected behavior(folder order, etc...). This helps spot issues like typos and content that doesn't follow the [contribution guide](#contribution-guide).
- [ ] Review the content for technical accuracy.
- [ ] Run the API or Workflow in Postman in a demo or new cloud environment.
- [ ] Check if the API or Workflow is available publicly or on demo server yet. If it isn't the PR will not be approved.

### Comments 

We may ask for clarification or changes in the comments on the PR in postman.

As you update your PR and apply changes, mark each comment as resolved.
