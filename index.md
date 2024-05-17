# React Hook Form Intricacies

[React Hook Form](https://react-hook-form.com/)  is a powerful framework to handle probably the most hardest part in interface work, the forms. I've been using the framework for the past 4 years maybe and it still keeps on giving in the good and in the bad. Here are some pain points I've stumbled upon the past years and some notes how to tackle them other considerations.

## Issues

### Form state is stuck on isDirty

#### Problem

- You change a field value and change it back to the original and the form state stays on _isDirty_.

#### Questions

- What fields are registered to the form state?
- Does all those fields have default values and what are those?
- If you use array fields, what are default values for those?

# Tips

- Have two separate models, one for API and one for UI and create a mapper that handles mapping to the form state
  and mapping to the api state.
- Create separate components for handling wrapping your form inputs and form state handling. This way the code gets a bit
  more concise.
- Use nulls for empty values in the form state if possible. The actualy inputs need to still have empty string, null is not allowed.
  Map the values accordingly in the form input intermediate component.

# Fields

## Numeric

- In UI model have it as a string and add a validator
