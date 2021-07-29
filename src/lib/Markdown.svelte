<script context="module">
  export const ssr = false;
</script>
<script lang="ts">
	import EasyMDE from "easymde";
  import { createEventDispatcher } from 'svelte';
  
  var easyMDE = new EasyMDE({
    autoDownloadFontAwesome: true,
    autoRefresh: true,
    element: document.getElementById('markdown'),
    initialValue: '# EasyMDE is working today...',
    autosave: {
        enabled: true,
        delay: 1000,
        uniqueId: 'mde-autosave-consomacteur'
    },
    previewClass: 'custom-preview',
    styleSelectedText: false,
    lineWrapping: false
  });

  const dispatch = createEventDispatcher();
  easyMDE.codemirror.on("change", function() {
    dispatch('easyChange', easyMDE.value());
  })
</script>
