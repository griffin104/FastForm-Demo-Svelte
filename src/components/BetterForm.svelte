<script>
  import { basketballTeams, checkboxOptions } from '../config';
  import { FastForm, Field } from '@fastform/form'

  let myValues
  let myErrors

  const initalValues = {
    firstName: '',
    lastName: '',
    email: '',
    confirmEmail: '',
    recommendation: 0,
    fruits: [],
    members: []
  }

  function handleEverything({values, errors}){
    myValues = values
    myErrors = errors
  }


</script>

<h1>Personal Survey</h1>
<FastForm 
  initValues={initalValues}
  handleSubmit={handleEverything}
  validate={({required, minNumOptions, maxNumOptions, mustMatch}) => {
    required('lastName')
    mustMatch('email', 'confirmEmail')
    minNumOptions('fruits', 1)
    maxNumOptions('fruits', 3)
  }}>
<div>
  <label for='firstName'>First Name</label>
  <Field type='text' name='firstName' autocomplete='off' validate={({required, customValidator}) => {
    required('firstName')
    customValidator(({values, errors}) => {
      if (values.firstName !== 'Angel') {
        errors.custom ??= {}
        errors.custom.firstName = 'Angel must be first name >:('
      }
      return {
        values,
        errors
      }
    })
  }} handleBlur={handleEverything} validateOnChange handleChange={handleEverything}/>
</div>
<div>
  <label for='lastName'>Last Name</label>
  <Field type='text' name='lastName' autocomplete='off'/>
</div>
<div>
  <label for='color'>Last Name</label>
  <Field type='range' name='color' min={1} max={2}/>
</div>
<div>
  <label for='email'>Email</label>
  <Field type='text' name='email' autocomplete='off'/>
</div>
<div>
  <label for='confirmEmail'>Confirm Email</label>
  <Field type='text' name='confirmEmail' autocomplete='off'/>
</div>
<div>
  <p>multi</p>
  <Field type='multiselect' name='members' values={['Angel', 'Steven', 'Ilija', 'Griffin']} />
</div>
<div>
  <label for='recommendation'>On a Scale of 1-10, how likely are you recommending Codesmith to other people?</label>
  <Field type='select' name='recommendation' values={[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]} />
  </div>
<div>
  <label for='fruits'>Please check your favorite fruits! (up to 3)</label>
  <Field type='checkbox' name='fruits' values={checkboxOptions} />
</div>
  <button type='submit'>Submit</button>
</FastForm>
<p>{JSON.stringify(myValues)}</p>
<p>{JSON.stringify(myErrors)}</p>