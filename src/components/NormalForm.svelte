<script>
import { basketballTeams, checkboxOptions } from '../config.js'
  import { errors } from '../store.js'
  //Initializing variables
  let firstName = '';
  let lastName = '';
  let dob = '';

  let sex = '';
  let selectSex = ['Male', 'Female']

  let selectbb = '';

  //Recommend Codesmith
  let recommendation = 0;
  let scale = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  
  let fruits = [];

  let submitted = false

  function handleSubmit(){
    limitFruits()
    if (!firstName) {
      $errors.firstName = 'First name must be provided'
    } else {
      $errors.firstName = ''
    }
    if (!lastName) {
      $errors.lastName = 'Last name must be provided'
    } else {
      $errors.lastName = ''
    }
    const vals = Object.values($errors)
    let disableFlag = true
    for (let i = 0; i < vals.length; i++) {
      if (vals[i]) {
        disableFlag = false
        break
      }
    }
    submitted = disableFlag
  }

  //limit number of fruit choices validators
  function limitFruits(){
    if (fruits.length>3){
        // disableSubmit = true;
        $errors.fruits = 'You can only select a max of 3 fruits'
    }
    else if (fruits[0] =='' || !fruits[0]){
      $errors.fruits = 'You have to select at least 1 fruit'
    }
    else {
      if ($errors.fruits) {
        $errors.fruits = ''
        }
    }
    console.log($errors)
  }
</script>

<h1>Personal Survey</h1>
<form on:submit|preventDefault={handleSubmit}>
  <!-- First Name Input Field -->
  <div>
    <label for="firstName">First Name</label>
    <input type="text" name='firstName' bind:value={firstName} autocomplete='off'/>
  </div>

  <!-- Last Name Input Field -->
  <div>
    <label for="lastName">Last Name</label>
    <input type="text" name='lastName' bind:value={lastName} autocomplete='off'/>
  </div>  

  <!-- Date of Birth -->
  <div>
    <label for="dob">Date of Birth</label>
    <input type="date" name='dob' bind:value={dob} min=1850-01-01 max=2022-01-01>
  </div>  

  <!-- Sex -->
  <div>
    <label for="sex">Sex</label>
    {#each selectSex as s}
    <label>
    <input type='radio' name='sex' value = {s} bind:group={sex}> 
    {s}</label>
    {/each}
  </div>

  <!-- Favorite Basketball Team -->
  <div>
    <label for="basketball">Favorite Basketball Team</label>
    <select bind:value = {selectbb}>
        {#each basketballTeams as bbTeam}
        <option value={bbTeam}>{bbTeam}</option>
        {/each}
    </select>
  </div>

  <!-- on a scale of 1-10, how likely are you recommending codesmith to other people? -->
  <div>
    <label>
        On a Scale of 1-10, how likely are you recommending Codesmith to other people? 
        <select bind:value={recommendation}>
            {#each scale as rating}
            <option value={rating}>{rating}</option>
            {/each}
        </select>
    </label>
 </div>

<!-- Please check your favoriate fruits! (up to 3) -->
<div>
  <!-- svelte-ignore a11y-label-has-associated-control -->
  <label>Please check your favorite fruits! (up to 3)</label>
  {#each checkboxOptions as option}
    <label><input type="checkbox" value={option} bind:group={fruits}>{option} </label>
  {/each}
</div>

  <!-- Submit Button -->
  <div>
    <button type='submit'>Submit Survey</button>
  </div>
</form>
<p>{JSON.stringify($errors, undefined, 2)}</p>
{#if submitted}
<p>{JSON.stringify({
  firstName,
  lastName,
  dob,
  sex,
  selectbb,
  recommendation,
  fruits
})}</p>
{:else}
<p>Not submitted</p>
{/if}
