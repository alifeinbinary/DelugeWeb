 <script setup>
  import {getDebug, stopDebug, onChangeIn, onChangeOut, informRef} from "./mididriver.js";
  import {onMounted, ref} from 'vue';
	import DirView from "./DirView.vue";
	import MemDump from "./MemDump.vue";

	let showLogWindow = ref(false);
  let midiLog = ref("");
  
   onMounted(() => {
			// startup();
			informRef(midiLog);
	});

 function turnOnDebug() {
  showLogWindow.value = true;
 	getDebug();
 }

 function turnOffDebug() {
  stopDebug();
  showLogWindow.value = false;
 }
 
</script>
 
<template>
<div class='ingroup' id='ingroup' width='512px'>
<br/>Midi:
     in: <select id="chooseIn"  @change="onChangeIn"><option label="(none)" value="" id="noneInput"/></select>
     out: <select id="chooseOut" @change="onChangeOut"><option label="(none)" value="" id="noneOutput"/></select>
     &nbsp;
     <button type="button" id="getDebugButton" @click="turnOnDebug">Start SysEx</button>
     &nbsp;
     <button type="button" id="stopDebugButton" @click="turnOffDebug">Stop SysEx</button>

<p/>
</div>

<p/>

<MemDump/>
<DirView/>
<template v-if="showLogWindow">
<hr/>
<p/>
<div class='status' id="midiStatus">inactive</div>
<p/>
<div id="debugOutput" class="outbox"  v-html="midiLog">
 </div>
</template>
</template>

<style>


canvas {
  border:1px solid #000000;
}

.outbox {
  border:1px solid #000000;
  overflow-y: scroll;

  display: flex;
  flex-direction: column-reverse;

  height: 160px;
  margin-bottom: 10px;
  margin-right: 30px;
}

</style>