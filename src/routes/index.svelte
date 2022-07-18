<script>
  //Initializing variables
  let firstName = '';
  let lastName = '';
  let dob = '';

  let sex = '';
  let selectSex = ['Male', 'Female']

  let selectbb = '';
  let basketballTeams = [
    {id:1, team: 'Raptors'},
    {id:2, team: 'Warriors'},
    {id:3, team: 'Heat'},
    {id:4, team: 'Suprs'},
    {id:5, team: 'Rockets'},
    {id:6, team: 'Suns'},
    {id:7, team: 'Celtics'},
    {id:8, team: 'Bulls'},
    {id:9, team: 'Knicks'},
    {id:10, team: 'Bucks'},
    {id:11, team: 'Nets'},
    {id:12, team: 'Lakers'},
    {id:13, team: 'Clippers'}
  ];
  //Income and income display format
  let income = 0;
  let formatMoney = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
  });

  //Recommend Codesmith
  let recommendation = 0;
  let scale = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

  let whyTho = '';
  let yesOrNo = '';

  //checkboxes
  let checkboxOptions = [
    {key:1, fruit:'Apple'},
    {key:2, fruit:'Banana'},
    {key:3, fruit:'Papaya'},
    {key:4, fruit:'Peach'},
    {key:5, fruit:'Pineapple'},
    {key:6, fruit:'Lychee'},
    {key:7, fruit:'Orange'},
    {key:8, fruit:'Cherry'},
    {key:9, fruit:'Mango'}
  ];
  let fruits = [''];

  //Handle submit function


  function sendAlert(){
      alert(`
          Name: ${firstName} ${lastName}
          Date of Birth: ${dob}
          Sex: ${sex}
          Favorite basketball team: ${selectbb}
          Income: ${income}
          Likelyhood of recommending Codesmith: ${recommendation}
      `)
      disableSubmit = false;
    }

    //first name and last name validators
  // @ts-ignore
  function checkLetters(input){
    return /^[A-Za-z]+$/.test(input);
  }

  let disableSubmit = true;

  function handleSubmit(){
    disableSubmit = true;
    
    setTimeout(sendAlert, 2000)
  }

  function validateInputs (){
    if (checkLetters(firstName) && checkLetters(lastName)){
    // disableSubmit = false;
    return false;
    }
    else {
    disableSubmit = true;
    return true; 
    }
  }
  //limit number of fruit choices validators
  function limitFruits(){
    if (fruits.length>3){
        // disableSubmit = true;
        alert('Please select 3 fruits or less')
        return true;
    }
    else if (fruits[0] =='' || !fruits[0]){
        return true;
    }
    else {
        // disableSubmit = false;
        return false;
    }
  }

  //on change, check the following validators
  $: console.log(fruits)


  $: if (firstName || lastName || fruits){
        if(!limitFruits() && !validateInputs()){
            console.log('if two validators are true')
            disableSubmit = false;
            console.log('disableSubmit', disableSubmit)
        }
        else {
            console.log('else')
            disableSubmit = true;
            console.log('disablesubmit', disableSubmit);
        }
  }


</script>

<h1>Personal Survey</h1>
<form>
  <!-- First Name Input Field -->
  <div>
    <label for="firstName">First Name</label>
    <input type="text" bind:value={firstName} required>
  </div>

  <!-- Last Name Input Field -->
  <div>
    <label for="lastName">Last Name</label>
    <input type="text" bind:value={lastName} required>
  </div>  

  <!-- Date of Birth -->
  <div>
    <label for="dob">Date of Birth</label>
    <input type="date" bind:value={dob} min=1850-01-01 max=2022-01-01>
  </div>  

  <!-- Sex -->
  <div>
    <label for="sex">Sex</label>
    {#each selectSex as s}
    <label>
    <input type='radio' value = {s} bind:group={sex}> 
    {s}</label>
    {/each}
  </div>

  <!-- Favorite Basketball Team -->
  <div>
    <label for="basketball">Favoriate Basketball Team</label>
    <select bind:value = {selectbb}>
        {#each basketballTeams as bbTeam}
        <option value={bbTeam.team}>{bbTeam.team}</option>
        {/each}
    </select>
  </div>

  <!-- Income -->
  <div>
    <label>
        Income
        <input type=range bind:value={income} min=0 max=500000>
        {formatMoney.format(income)}
    </label>
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
    {#if recommendation < 5 && recommendation > 0}
    <div>
        <label>
            WHY THOUGH?
            <br/>
            <textarea bind:value={whyTho} cols="40" rows="10"></textarea>
        </label>
    </div>
    {:else}
        {#if recommendation<=10 && recommendation>5}
          <div>
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label>
                ARE YOU SURE IT'S THAT GOOD?
                <br/>
                <label><input type=radio bind:group={yesOrNo} value='yes'>Yes</label>
                <label><input type=radio bind:group={yesOrNo} value='no'>No</label>
            </label>
          </div>
        {/if}
    {/if}
 </div>

<!-- Please check your favoriate fruits! (up to 3) -->
<div>
  <!-- svelte-ignore a11y-label-has-associated-control -->
  <label>Please check your favoriate fruits! (up to 3)</label>
  {#each checkboxOptions as option}
    <label><input type="checkbox" value={option.fruit} bind:group={fruits}>{option.fruit} </label>
  {/each}
</div>

  <!-- Submit Button -->
  <div>
    <button type='submit' disabled={disableSubmit} on:click|preventDefault={handleSubmit}>Submit Survey</button>
  </div>
</form>