<script context="module">
  export const ssr = false;
</script>
<script>
	import EasyMDE from "easymde";
  import { createEventDispatcher } from 'svelte';

  var easyMDE = new EasyMDE({
    autoDownloadFontAwesome: true,
    element: document.getElementById('markdown'),
    initialValue: '# EasyMDE is working today...',
    autosave: {
        enabled: true,
        delay: 1000,
        uniqueId: 'mde-autosave-consomacteur'
    }
  });

  const dispatch = createEventDispatcher();
  easyMDE.codemirror.on("change", function() {
    console.log(easyMDE.value());
    dispatch('easyChange', easyMDE.value());
  })
</script>
