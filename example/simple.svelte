<script lang="ts">
  import Checkbox from '../src/index.svelte';
  import '../assets/index.less';

  let disabled = false

  function onChange(e) {
    console.log('Checkbox checked:', e.target.checked);
  }

  function onKeyDown(e) {
    console.log('Checkbox key down:', e.key);
  }

  function onKeyPress(e) {
    console.log('Checkbox key press:', e.key);
  }

  function onKeyUp(e) {
    console.log('Checkbox key up:', e.key);
  }

  const handleDisabled = () => {
    disabled = !disabled
  }
</script>

<main>
  <h1>Svelte Checkbox</h1>

  <div style="margin: 20px">
    <div>
      <p>
        <label>
          <Checkbox checked on:change={onChange} disabled={disabled} />
          &nbsp; controlled checked sc-checkbox
        </label>
        &nbsp;&nbsp;
      </p>
      <p>
        <label>
          <input checked type="checkbox" on:change={onChange} disabled={disabled} />
          &nbsp; controlled checked native
        </label>
        &nbsp;&nbsp;
      </p>
    </div>

    <div>
      <p>
        <label>
          <Checkbox defaultChecked on:change={onChange} disabled={disabled} />
          &nbsp; defaultChecked sc-checkbox
        </label>
        &nbsp;&nbsp;
      </p>
      <p>
        <label>
          <input
            type="checkbox"
            checked
            onChange={onChange}
            disabled={disabled}
          />
          &nbsp; defaultChecked native
        </label>
        &nbsp;&nbsp;
      </p>
    </div>

    <div>
      <p>
        <label>
          <Checkbox
            name="my-checkbox"
            defaultChecked
            on:change={onChange}
            disabled={disabled}
          />
          &nbsp; defaultChecked sc-checkbox with name
        </label>
        &nbsp;&nbsp;
      </p>
      <p>
        <label>
          <input
            name="my-checkbox"
            type="checkbox"
            defaultChecked
            on:change={onChange}
            disabled={disabled}
          />
          &nbsp; defaultChecked native with name
        </label>
        &nbsp;&nbsp;
      </p>
    </div>

    <div>
      <p>
        <label>
          <Checkbox
            on:change={onChange}
            on:keydown={onKeyDown}
            on:keypress={onKeyPress}
            on:keyup={onKeyUp}
            disabled={disabled}
          />
          &nbsp; sc-checkbox with key events
        </label>
        &nbsp;&nbsp;
      </p>
      <p>
        <label>
          <input
            type="checkbox"
            on:change={onChange}
            on:keydown={onKeyDown}
            on:keypress={onKeyPress}
            on:keyup={onKeyUp}
            disabled={disabled}
          />
          &nbsp; native checkbox with key events
        </label>
        &nbsp;&nbsp;
      </p>
    </div>

    <button type="button" on:click={handleDisabled}>
      toggle disabled
    </button>
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
  p {
    height: 20px;
  }
  p label{
    display: flex;
  }
</style>
