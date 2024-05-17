# React Hook Form Intricacies

[React Hook Form](https://react-hook-form.com/) is a powerful framework to handle probably the most hardest part in interface work, the forms. I've been using the framework for the past 4 years maybe and it still keeps on giving in the good and in the bad. Here are some pain points I've stumbled upon and some ideas how to tackle them.

## TL;DR;

- If something is wrong with the dirty state. Check default values.

## Pain points

### Form state is dirty after initial load

You have an editor which is used for editing an existing model. When you fetch a resource from the API and the form state gets loaded with the data, the formState.isDirty is immediately true.

**Questions**

- What fields are registered to the form state?
- What kind of data does the API return?
- What kind of "empty" values does the API return? What do you consider empty?
- Does all the registered fields have default values and what are those?
- If you use array fields, what are default values for those?

### Form state is stuck on isDirty

You change a field value and change it back to the original and the form state stays on _isDirty_.

**Questions**

- What fields are registered to the form state?
- Does all those fields have default values and what are those?
- If you use array fields, what are default values for those?

### Client sends empty strings to the API

You have text inputs and you clear values from them and hit save and the client sends empty string to the API which is not good.

**Questions**

- What does empty value mean in your context?

**Principles**

- [Undefined and null are not allowed for input's value.](https://react.dev/reference/react-dom/components/input#controlling-an-input-with-a-state-variable)
- Prefer null over empty string "" in **form state**

**Actions**

- Create a component which wraps the form state handling and your input component. This way we can centralize the input state handling and make the overall code more concise. In this wrapper you can map null values to empty strings and map empty strings back to null for the form state whenever value changes.

## Patterns

- Have two separate models. One for the API and one for the UI. Create mappers for mapping data both ways. E.g `toApiModel` and `toFormState`.
- Create intermediate components which wraps individual field form state handling and your custom inputs. This way you can centralize the state handling and make your code a bit more concise.
- Use nulls for empty values in the form state if possible. The actualy inputs need to still have empty string, null is not allowed.
- If you have numeric data consider having them as strings in your UI model. Add numeric validator for these fields. This way your life gets a lot easier than trying to handle numeric data.
