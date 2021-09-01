<script lang="ts">
  import classNames from 'classnames';
  // static defaultProps = {
  //   prefixCls: 'sc-checkbox',
  //   className: '',
  //   style: {},
  //   type: 'checkbox',
  //   defaultChecked: false,
  //   onFocus() {},
  //   onBlur() {},
  //   onChange() {},
  //   onKeyDown() {},
  //   onKeyPress() {},
  //   onKeyUp() {},
  // };
  let inputNode
  let checked = 'checked' in $$props ? $$props.checked : $$props.defaultChecked;

  function focus() {
    inputNode.focus();
  }

  function blur() {
    inputNode.blur();
  }

  const handleChange = e => {
    console.log('handleChange', e, $$props)
    const { disabled, onChange } = $$props;
    if (disabled) {
      return;
    }
    if (!('checked' in $$props)) {
      checked = e.target.checked
    }
    if (onChange) {
      onChange({
        target: {
          ...$$props,
          checked: e.target.checked,
        },
        stopPropagation() {
          e.stopPropagation();
        },
        preventDefault() {
          e.preventDefault();
        },
        nativeEvent: e.nativeEvent,
      });
    }
  };

  export let prefixCls = 'sc-checkbox';
  export let className = '';
  export let style = '';
  export let name;
  export let id;
  export let type = 'checkbox';
  export let defaultChecked = false;
  export let disabled = false;
  export let readOnly = false;
  export let tabIndex;
  export let onClick = () => {};
  export let onFocus = () => {};
  export let onBlur = () => {};
  export let onKeyDown = () => {};
  export let onKeyPress = () => {};
  export let onKeyUp = () => {};
  export let autoFocus = false;
  export let value;
  export let required = false;

  let others = {}
  $: {
		/* eslint-disable no-unused-vars */
		const {
			prefixCls,
      className,
      style,
      name,
      id,
      type,
      disabled,
      readOnly,
      tabIndex,
      onClick,
      onFocus,
      onBlur,
      onKeyDown,
      onKeyPress,
      onKeyUp,
      autoFocus,
      value,
      required,
      ...extraProps
		} = $$props;
    others = extraProps
	}

  const globalProps = Object.keys(others).reduce((prev, key) => {
    if (key.substr(0, 5) === 'aria-' || key.substr(0, 5) === 'data-' || key === 'role') {
      // eslint-disable-next-line no-param-reassign
      prev[key] = others[key];
    }
    return prev;
  }, {});

  $: classString = classNames(prefixCls, className, {
    [`${prefixCls}-checked`]: checked,
    [`${prefixCls}-disabled`]: disabled,
  });
</script>

<main>
  <span class={classString} style={style}>
    <input
      name={name}
      id={id}
      type={type}
      required={required}
      readonly={readOnly}
      disabled={disabled}
      tabindex={tabIndex}
      class={`${prefixCls}-input`}
      checked={!!checked}
      on:click={onClick}
      on:focus={onFocus}
      on:blur={onBlur}
      on:keyup={onKeyUp}
      on:keydown={onKeyDown}
      on:keypress={onKeyPress}
      on:change={handleChange}
      autofocus={autoFocus}
      bind:this={inputNode}
      value={value}
      {...globalProps}
    />
    <span class={`${prefixCls}-inner`} />
  </span>
</main>

<style>

</style>
