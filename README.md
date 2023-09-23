# TS Note

## Introduction

In this exercise you will build a basic notes app. Completion of this exercise demonstrates
that you can model data in TypeScript, communicate with the compiler using assertions,
work with built in [DOM Interfaces](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model#dom_interfaces)
and also use generics to convey to TypeScript the type of DOM nodes you are working with.

## Prerequisites

[Yarn](https://yarnpkg.com/getting-started/install)

## Running the project

This project was created from the [vite vanilla-ts template](https://vitejs.dev/guide/#scaffolding-your-first-vite-project)

To run the project run the following commands from the project root folder.

```sh
yarn # install project
yarn dev # run development server
```

## 1. Project Setup

Take a moment to review the project in its current state, taking inventory of already existing items.
Be sure to read through the requirements thoroughly to understand what is expected and how the application
should behave.

## 2. Project Requirements

- Create a custom type to model a note. A single note should have a (unique)`id`, `title` and `description`
- Using the `starterNotes`, when the application starts up add all starter notes to the `note list` container
- Create a function that takes in a note type, that then makes the following structure

```html
<div class="note">
  <h2>{note title}</h2>
  <p>{note description}</p>
</div>
```

- Using [Custom Data Attributes](https://www.w3schools.com/tags/att_data-.asp) add a `data-note-id` attribute
  to all note elements created.

- When a user clicks on the `Add Note` button create a new note and reset the form.

  - Listen for a `submit` event on the form. Using the `event` object, prevent the default behavior of the form, we want to drive the behavior ourself.
  - Grab the `form` element off the page and create a `FormData` object using the `form` element.
  - Using the `FormData` object get the `title` and `description` from the form and use the values
    to help create a new note object.
  - Once a new note has been created and added to the page, use the form element [reset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/reset) method to clear out the form inputs
  - Use the [get](https://developer.mozilla.org/en-US/docs/Web/API/FormData/get) method on the `FormData` object to grab the values of interest. The string provided to the `get` corresponds to the `name` attribute on form fields.

- When selecting DOM nodes TS has no way of knowing if the node exists or not, there for the return type is `Element | undefined` (either a HTML Element or Undefined). As developers we know more than TS does, use [Non Null Assertion Operator](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#non-null-assertion-operator) to tell TypeScript that your DOM nodes exist when you are querying elements off the page.

  NOTE: When querying elements off the page you will need to use `generics` to tell TypeScript what type of element you are querying for. Examples of what this looks like is the following...

  ```ts
  const someDiv = document.querySelector<HTMLDivElement>(".some-selector");
  ```

  The `<HTMLDivElement>` is our `generic` here that tells TypeScript specifically what element we are pulling off the page. this is needed in order to have access to methods and properties that are unique to specific elements. If not you will get errors saying that a `property` or `method` does not exist on type `Element` which is the default base type of all HTML Elements.

  A reference of elements can be found [here](https://developer.mozilla.org/en-US/docs/Web/API) in the `H` section. Using `Ctrl + f` you can search the page for `HTMLDivElement`, `HTMLFormElement` etc and be taken to the section showing all the element interfaces available to you. You can also see the list of possible elements in your editors intellisense suggestions by typing `HTML` within the `<>`'s

## Stretch

The following items are completely optional

- implement a way for users to edit a selected note using the existing form on the page.

  TIP: add a custom data attribute called `data-editing-state` to the form and set it to be false by default. Set the editing state to true when a note is selected for editing. Also earlier we added a `data-note-id` to all notes, use this ID along with custom data attributes to help you figure out which note should have changes applied to it.

- implement a way for users to delete a note
