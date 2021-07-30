<script context="module">
  export const ssr = false;
</script>
<script lang="ts">
	import EasyMDE from "easymde";
  import { onMount } from "svelte";
  import { createEventDispatcher } from 'svelte';
  
  var easyMDE = new EasyMDE({
    autoDownloadFontAwesome: true,
    element: document.getElementById('markdown'),
    initialValue: '# EasyMDE is working today...',
    scrollbarStyle: 'null',
    autosave: {
        enabled: true,
        delay: 1000,
        uniqueId: 'mde-autosave-consomacteur'
    },
    previewClass: 'custom-preview',
    styleSelectedText: false,
    lineWrapping: true,
    toolbar: ["bold", "italic", "heading", "link", "unordered-list", "horizontal-rule",
      {
        name: "Paragraphe",
        action: function customFunction(editor){
          const doc = editor.codemirror.getDoc();
          const cursor = doc.getCursor();
          doc.replaceRange('<p>Insérer le texte ici</p>', cursor);
        },
        className: "fa fa-paragraph",
        title: "Paragraphe",
      },
      {
        name: "Saut de ligne",
        action: function customFunction(editor){
          const doc = editor.codemirror.getDoc();
          const cursor = doc.getCursor();
          doc.replaceRange('<br/>', cursor);
        },
        className: "fa fa-line",
        title: "Saut de ligne",
      },
    ]
  });

  const dispatch = createEventDispatcher();
  easyMDE.codemirror.on("change", function() {
    dispatch('easyChange', easyMDE.value());
  })

  onMount(async () => {
    dispatch('easyChange', easyMDE.value());
  });
</script>
