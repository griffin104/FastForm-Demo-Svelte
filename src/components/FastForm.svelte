<script>
  import { basketballTeams, checkboxOptions } from 'src/config';
  import { FastForm, Field } from '@fastform/form'

  const initalValues = {
    firstName: '',
    lastName: '',
    dob: '',
    sex: '',
    selectbb: '',
    income: 0,
    recommendation: 0,
    fruits: []
  }
  function handleSubmit(){
    isSubmitting = true;
    setTimeout(() => {
      isSubmitting = false
    }, 2000);
  }
</script>

<h1>Personal Survey</h1>
<FastForm 
  initValues={initalValues}
  handleSubmit={handleSubmit}>

  <label for='firstName'>First Name</label>
  <Field type='text' name='firstName' />

  <label for='lastName'>Last Name</label>
  <Field type='text' name='lastName' />

  <label for='dob'>Date of Birth</label>
  <Field type='date' name='dob' min=1850-01-01 max=2022-01-01 />

  <label for='sex'>Sex</label>
  <Field type='radio' name='sex' values={['male', 'female']} />

  <label for='basketball'>Favorite Basketball Team</label>
  <Field type='select' name='selectbb' values={basketballTeams} />

  <label for='recommendation'>On a Scale of 1-10, how likely are you recommending Codesmith to other people?</label>
  <Field type='select' name='recommendation' values={[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]} />

  <label for='fruits'>Please check your favorite fruits! (up to 3)</label>
  <Field type='checkbox' name='fruits' values={checkboxOptions} />

  <button type='submit' on:click|preventDefault={handleSubmit}>Submit</button>
</FastForm>