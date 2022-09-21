
# How can I write a property editor for Umbraco using [_my framework_]?

  

Although this example is written using Lit, this approach will allow you to write a property editor using any framework of your choice. Or no framework at all!

  

**What's Important**

  

1. `webComponentPropertyEditorWrapper.js` is our base AngularJS controller (the "Wrapper") that creates a unique key, listens for a unique event, and reports the value back to Umbraco.

2. `package.manifest` includes a reference to the Wrapper.

3. You are free to write your component your way. Just remember to:

- Wrap your component's HTML with the Wrapper.

- Your component is responsible for communicating changes to the Wrapper through a custom event, referencing the unique key.

  
  

**What Does This Example Use?**

  

- I'm using `Lit` to create a simple property editor.

- The value type of my property editor is `Object.`

- To keep this example as brief as possible, I've forgone any `build systems` or build steps.

  

**But performance!**

  

- If you're considering loading an additional JS framework in the Umbraco Backoffice ... I think we can agree that _blazing performance_ has been cast aside in favor of other improvements such as (1) modern workflows, (2) existing component reuse, and (3) to use fun new frameworks!

- I import my new property editor script in the markup instead of referencing this from the `package.manifest`. I do this so I can mark it as a `module.` Don't worry if you have multiple instances of the very same property editor; a browser will only ever load and execute a module one time.

- I left out the `build system` entirely, so I don't expect this example to run in everyone's browser. You'll need support for `modules,` `imports,` and the `Lit` framework I request from a CDN.

  

**Can you show me how to write this in [x] framework?**

  

- Probably not!

- I'm not kidding, but I plan to revisit this idea once Umbraco HQ has completed their modernization of the backoffice. They aim to rewrite the backoffice using modern web components and remove the AngularJS dependency!

  

**Is there a better way to do this?**

  

- Probably!

- A peculiar issue plagues both `LocalStorage` and `SessionStorage`. The `storage` event, which one could generally subscribe to and be notified of any changes, only works _between other windows and tabs_. The event will not trigger when your listener is in the same document as the setter.
