## Custom templates

In the latest versions of `create-react-app`, you can select a template to use for your new application, and you can create your own custom templates.

## How are custom templates used?

A custom template can be used to:

- install particular dependencies
- provide the application directory structure
- add or change any default application files
- specify what is in the `.gitignore`
- add custom scripts or eslint configurations
- change the default README.md
- and more

You specify a custom template when you call create-react-app:

npx create-react-app my-app --template [template-name] 

## Finding custom templates

There are many custom templates already created that you can use. You can find templates created and published by others [by searching for "cra-template-*" on npm](https://www.npmjs.com/search?q=cra-template-*).

**Create a project using a custom template**

Try creating a React project with a template you find on npm. If you have trouble finding one, try this one:

`npx create-react-app basic-sass-app --template cra-template-basic-sass`

## Creating templates

Learn more about creating your own custom templates in [the Create React App documentation here](https://create-react-app.dev/docs/custom-templates/). You can create your own templates with react-scripts 3.3.0 and higher.

If you are keen, try creating your own template following the instructions in the Create React App documentation. After you [test it locally](https://create-react-app.dev/docs/custom-templates/#testing-a-template), you will have to [have an npm account](https://www.npmjs.com/signup), to make it available publicly. Once you do, from your template directory, you can run the following to publish your template:

```
npm login 
npm publish
```