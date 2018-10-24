# Usage

```
yarn add forms-binding-react

npm install forms-binding-react
```

```js
// For HOC usage
import { withForm } from 'forms-binding-react'

// For Function As a Children Component
import { FormFACC } from 'forms-binding-react'
```

**withForm** example :

```js
import React, { Component } from 'react'
import { withForm } from 'forms-binding-react'

const validators = {
    username: addNamePredicate = value => value && /(?:\w){6,}/.test(value);
}

class FormPageComponent extends Component {
    render () {
        const {
              handleChange,
              handleSubmit,
              addPredicate,
              fields: { username },
              errors,
              formValid
            } = this.props;

        return (
            <form onSubmit={handleSubmit}>
                <InputForm
                    type="text"
                    name="username"
                    value={username}
                    labelTitle="Username"
                    error={errors.username}
                    handleChange={handleChange}
                    setPredicate={addPredicate("username", validators.username)}
                />
                <button
                    type="submit"
                    disabled={!formValid}
                >
                    Submit
                </button>
            </form>
        )
    }
}

export const FormPage = withForm(FormPageComponent)
```

**formFACC** example :

```js
import React, { Component } from 'react'
import { FormFACC } from 'forms-binding-react'

const validators = {
    username: addNamePredicate = value => value && /(?:\w){6,}/.test(value);
}

class FormPageComponent extends Component {
    render () {
        return (
            <FormFACC>
            {({
                handleChange,
                handleSubmit,
                addPredicate,
                fields: { username },
                errors,
                formValid
            }) => (
                 <form onSubmit={handleSubmit}>
                    <InputForm
                        type="text"
                        name="username"
                        value={username}
                        labelTitle="Username"
                        error={errors.username}
                        handleChange={handleChange}
                        setPredicate={addPredicate("username", validators.username)}
                    />
                    <button
                        type="submit"
                        disabled={!formValid}
                    >
                        Submit
                    </button>
                 </form>
            )}
            </FormFACC>
        )
    }
}

export const FormPage = FormPageComponent
```