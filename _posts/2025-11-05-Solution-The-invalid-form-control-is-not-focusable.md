---
title:  "Solution | The invalid form control ... is not focusable"
date:   2025-11-05
tags: [form-validation, frontend, stimulus]
---
<!-- link para blog com problmea -->
When an input has the hidden and required properties set
to `true`, the browser doesn't show the validation messages
and instead warns on the console that:

> [!WARNING]
> The invalid form control with name=‘’ is not focusable.

Solution:
Remove required true from input.
And manually validate and create error message using js when submitting the form
without the _required_ values.

```html
  <form action="" id="form">
    <label for="image" id="label">
      <span>Files</span>
      <input type="file" name="image" id="">
    </label>
    <input type="submit" value="upload">
  </form>
  <script>
    const form = document.getElementById('form');
    form.addEventListener('submit', (event) => {
      event.preventDefault();
      // verify if the input has a file
      const label = document.getElementById('label');
      const file = event.target.image.files[0];
      if (!file){
        // create error message
        const error = document.createElement('p');
        error.textContent = "Please add a file";
        error.style.color = 'red';
        label.insertAdjacentElement('beforeend', error);
      }
    })
  </script>
```
