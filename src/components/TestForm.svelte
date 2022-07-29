<script>
  import { FastForm, Field } from "@fastform/form"
  // import Field from '../lib/Field/Field.svelte'
  let initValues = {
    name: 'Griffin',
    name2: 'Angel',
    icecream: []
  }
  
  function handleSubmit(values) {
    console.log(values)
  }
  let v
  let e
</script>


<FastForm 
initValues={initValues} 
handleSubmit={handleSubmit}
validate = {({values, errors, required, mustMatch, minNumOptions, maxNumOptions}) => {
  required('name')
  mustMatch('name', 'name2')
  maxNumOptions('icecream', 2)
  minNumOptions('icecream', 1)

  v = values
  e = errors
  }}>
  <Field name='name' type='text' autocomplete='off'/>
  <Field name='name2' type='text' autocomplete='off'/>
  <Field name='icecream' type='checkbox' values={['Chocolate', 'Vanilla', 'Cookies N Cream']}/>
  <button type='submit'>Submit!</button>
</FastForm>

<p>{JSON.stringify(v)}</p>
<p>{JSON.stringify(e)}</p>
