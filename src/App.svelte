<script>
  import CustomInput from './CustomInput.svelte';
  import Toggle from './Toggle.svelte';
  import { isValidEmail } from './validation.js';

  let val = "";
  let selectedOption = 1;
  let price = 0;
  let agreed;
  let favColor = 'green';
  let favColorCheck = ['green']
  let singleFavColor = 'blue';
  let usernameInput;
  let someDiv;
  let customInput;
  let enteredEmail = "";
  let formIsValid = false;

  $: if (isValidEmail(enteredEmail)) {
    formIsValid = true;
  } else {
    formIsValid = false;
  }

  $: console.log(val)
  $: console.log(selectedOption)
  $: console.log(price)
  $: console.log(agreed)
  $: console.log(favColor)
  $: console.log(favColorCheck)
  $: console.log(singleFavColor)
  $: console.log(customInput)

  function setValue(e) {
    val = e.target.value
  }

  function saveData() {
    // vanilla js way to do it
    /*console.log(document.querySelector('#username').value)*/
    console.log(usernameInput.value)
    console.dir(usernameInput)
    console.dir(someDiv)
    customInput.empty()
  }
</script>

<style>
  .invalid {
    border: 1px solid red;
  }
</style>

<input type="text" value={val}>
<input type="text" value={val} on:input={setValue}>
<input type="text" bind:value={val}>
<CustomInput bind:this={customInput} />
<Toggle bind:chosenOption={selectedOption} />

<input type="number" value={price} on:input={e => console.log('1' +
       e.target.value)} />

<input type="number" bind:value={price} />

<label>
  <input type="checkbox" bind:checked={agreed} />
  Agree to Terms?
</label>

<h1>Favorite Color?</h1>
<label>
  <input type="radio" name="color" value="red" bind:group={favColor}>
  red
</label>
<label>
  <input type="radio" name="color" value="green" bind:group={favColor}>
  green
</label>
<label>
  <input type="radio" name="color" value="blue" bind:group={favColor}>
  blue
</label>

<label>
  <input type="checkbox" name="color" value="red" bind:group={favColorCheck}>
  red
</label>
<label>
  <input type="checkbox" name="color" value="green"
  bind:group={favColorCheck}>
  green
</label>
<label>
  <input type="checkbox" name="color" value="blue"
  bind:group={favColorCheck}>
  blue
</label>

<select bind:value={singleFavColor}>
  <option value="green">Green</option>
  <option value="red">Red</option>
  <option value="blue">Blue</option>
</select>

<hr>
<input type="text" bind:this={usernameInput} />
<button on:click={saveData}>Save</button>

<div bind:this={someDiv}></div>

<form on:submit|preventDefault>
  <input type="email" bind:value={enteredEmail}
  class={isValidEmail(enteredEmail) ? "" : 'invalid'}>
  <button type="submit" disabled={!formIsValid}>Submit</button>
</form>
