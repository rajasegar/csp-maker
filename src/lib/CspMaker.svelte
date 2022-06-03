<script>
  import { getCSP, nonce, EVAL, INLINE, SELF } from 'csp-header';

    import TabsPill from './VerticalTabs.svelte';
    import CheckBox from './CheckBox.svelte';

    import directiveList from './directiveList.js';
    import directiveValues from './directiveValues.js';

    let enableDirectives = {
        'default-src': false,
        'script-src': false,
        'style-src': false,
        'img-src': false,
        'connect-src': false,
        'style-src': false,
      }

    let directives = { };
    let cspObj = { directives };

    let inputs = [{title: ''}];

  function addInput() {
      directives['default-src'] = [...getDirectiveValues('default-src'), ...inputs.map(i => i.title)];
        text = getCSP(cspObj);

    inputs = [...inputs, { title: "" }];
  }

  function callFocus(input){
    input.focus();
  }





    let text = getCSP(directives);

    function handleDirectiveSelection(directive, checked) {
        enableDirectives[directive] = checked;
        if(checked) {
            directives[directive] = [];
          } else {
              delete directives[directive];
            }
        text = getCSP(cspObj);
      }

    function updateScriptSrc(dirName, checked) {
        scriptDirective[dirName] = checked;

        let _scriptDirs = [];
        for(const dir in scriptDirective) {
            if(scriptDirective[dir]) {
                _scriptDirs.push(dir);
              }
          }

        directives['script-src'] = _scriptDirs;

        text = getCSP(cspObj);
      }


    function updateDefaultSrc(dirName, checked) {
        defaultDirective[dirName] = checked;

        let _dirs = [];
        for(const dir in defaultDirective) {
            if(defaultDirective[dir]) {
                _dirs.push(dir);
              }
          }

        directives['default-src'] = _dirs;

        text = getCSP(cspObj);
      }

    function updateDirectiveValue(directive, key, value) {
        const _dirValue = directiveValues[directive];
        _dirValue[key] = value;

        let _dirs = [];
        for(const key in _dirValue) {
            if(_dirValue[key]) {
                _dirs.push(`'${key}'`);
              }
          }

        directives[directive] = _dirs;

        console.log(directives);

        text = getCSP(cspObj);
      }

    function getDirectiveValues(directive) {
      let values = directiveValues[directive];
        return Object.keys(values)
          .filter(k => values[k])
      }

    function updateDefaultSrcNonce(ev) {
        if(ev.target.value) {
        directives['default-src'] = [...getDirectiveValues('default-src'), `nonce('${ev.target.value}')`];
          } else {

        directives['default-src'] = [...getDirectiveValues('default-src')];
            }
        text = getCSP(cspObj);
      }

    function addDefaultSrcUrl(ev) {

        directives['default-src'] = [...getDirectiveValues('default-src'), ev.target.value];
        text = getCSP(cspObj);
      }

</script>

<div class="text-left">
<div class="max-w-7xl mx-auto flex flex-wrap">
  <div class="w-full flex flex-column">
    <textarea class="mb-4 p-2 border w-full" bind:value={text}></textarea>
  </div>
</div>

  <TabsPill labels={directiveList}>
    <div  slot="tab1" >
      <p class="mb-2">The default-src directive defines the default policy for fetching resources such as JavaScript, Images, CSS, Fonts, AJAX requests, Frames, HTML5 Media.</p>
      <section>
        <CheckBox handleFn={(ev) => handleDirectiveSelection('default-src', ev.target.checked)} label='default-src' />
        <div class="flex">
          <CheckBox handleFn={(ev) => updateDirectiveValue('default-src', '*', ev.target.checked)} label='*' enable={enableDirectives['default-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('default-src', 'self', ev.target.checked)} label='self' enable={enableDirectives['default-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('default-src', 'unsafe-inline', ev.target.checked)} label='unsafe-inline' enable={enableDirectives['default-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('default-src', 'unsafe-eval', ev.target.checked)} label='unsafe-eval' enable={enableDirectives['default-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('default-src', 'https:' , ev.target.checked)} label='https:' enable={enableDirectives['default-src']}/>
        </div>

          <div>
            <label class="block mb-1 text-indigo-600">nonce:</label>
            <input class="block border rounded p-1 w-full" disabled={!enableDirectives['default-src']} on:input={updateDefaultSrcNonce} type="text"/>
          </div>

          <div class="mt-2">
            <h3>Custom domain urls:</h3>
            {#each inputs as i}
              <input disabled={!enableDirectives['default-src']} class="my-1 block border rounded p-1 w-full" type="text" bind:value={i.title} use:callFocus /> 
            {/each}

            <button class="bg-gray-700 text-white px-2 py-1 rounded disabled:bg-red-500 disabled:cursor-not-allowed" disabled={!enableDirectives['default-src']} on:click={addInput}>+</button>
          </div>
      </section>
    </div>
    <div  slot="tab2" >

      <p class="mb-2">Defines valid sources of JavaScript.</p>
      <section>
        <CheckBox handleFn={(ev) => handleDirectiveSelection('script-src', ev.target.checked)} label='script-src' />
        <div class="flex">
          <CheckBox handleFn={(ev) => updateDirectiveValue('script-src', SELF, ev.target.checked)} label='SELF' enable={enableDirectives['script-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('script-src', INLINE, ev.target.checked)} label='INLINE' enable={enableDirectives['script-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('script-src', EVAL, ev.target.checked)} label='EVAL' enable={enableDirectives['script-src']}/>
        </div>
      </section>
    </div>
    <div slot="tab3">
      <p class="mb-2">Defines valid sources of Stylesheets or CSS.</p>
      <section>
        <CheckBox handleFn={(ev) => handleDirectiveSelection('style-src', ev.target.checked)} label='style-src' />
        <div class="flex">
          <CheckBox handleFn={(ev) => updateDirectiveValue('style-src', SELF, ev.target.checked)} label='SELF' enable={enableDirectives['style-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('style-src', INLINE, ev.target.checked)} label='INLINE' enable={enableDirectives['style-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('style-src', EVAL, ev.target.checked)} label='EVAL' enable={enableDirectives['style-src']}/>
        </div>
      </section>
    </div>
    <div slot="tab4">
      <p class="mb-2">Defines valid sources of images.</p>
      <section>
        <CheckBox handleFn={(ev) => handleDirectiveSelection('img-src', ev.target.checked)} label='img-src' />
        <div class="flex">
          <CheckBox handleFn={(ev) => updateDirectiveValue('img-src', SELF, ev.target.checked)} label='SELF' enable={enableDirectives['img-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('img-src', INLINE, ev.target.checked)} label='INLINE' enable={enableDirectives['img-src']}/>
          <CheckBox handleFn={(ev) => updateDirectiveValue('img-src', EVAL, ev.target.checked)} label='EVAL' enable={enableDirectives['img-src']}/>
        </div>
      </section>
    </div>
  </TabsPill>


</div>

<style>
</style>

