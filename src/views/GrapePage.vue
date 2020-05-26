<template>
  <div>
    <div id="gjs"></div>
  </div>
</template>

<script>
import grapesjs from 'grapesjs/dist/grapes.js';
import grapejsPreset from 'grapesjs-preset-newsletter';

export default {
  name: 'grape-test',
  data () {
    return {
      editor: null,
    };
  },
  mounted () {
    const myNewComponentTypes = editor => {
      editor.DomComponents.addType('rsvp-button', {
        extend: 'link',
        model: {
          defaults: {
            editable: true,
            droppable: false,
            style: {
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'width': '200px',
              padding: '5px',
              'min-height': '50px',
              'min-width': '50px',
              color: 'black',
              'text-decoration': 'none',
            },
            attributes: {
              href: 'http://google.com'
            },
            components: [{
              tagName: 'span',
              type: 'text',
              attributes: { title: 'foo' },
              components: [{
                type: 'textnode',
                content: 'Hello world!!!'
              }]
            }]
          }
        }
      });

      editor.DomComponents.addType('custom-image', {
        extend: 'image',
      });
    };

    var editor = grapesjs.init({
      container: '#gjs',
      plugins: [grapejsPreset, myNewComponentTypes],
      pluginsOpts: {
        'gjs-preset-newsletter': {
          modalTitleImport: 'Import template',
        }
      },
      styleManager : {
        sectors: [{
          name: 'Dimension',
          buildProps: ['width', 'min-height']
        },{
          name: 'Extra',
          buildProps: ['background-color', 'box-shadow']
        }]
      }
    });

    this.editor = editor;

    const bm = this.editor.BlockManager;
    this.editor.on('load', () => {
      this.editor.BlockManager.render([
        bm.get('sect100').set('category', ''),
        bm.get('text').set('category', ''),
        bm.get('image').set('category', '')
      ])
    });

    console.log(this.editor)

    // this.editor.BlockManager.add('rsvp-button', {
    //   label: 'Rsvp button',
    //   category: 'Contents',
    //   attributes: { class: 'fa fa-graduation-cap' },
    //   content: {
    //     type: 'rsvp-button'
    //   },
    // });

    // this.editor.BlockManager.add('custom-image', {
    //   label: 'Custom image',
    //   category: 'Contents',
    //   attributes: { class: 'fa fa-image' },
    //   content: {
    //     type: 'custom-image'
    //   }
    // });
  },
}
</script>

<style lang="scss">
// .gjs-pn-panel {
//   position: relative;
// }

// .row {
//   display: flex;
//   justify-content: flex-start;
//   align-items: stretch;
//   flex-wrap: nowrap;
// }

// .column {
//   min-height: 75px;
//   flex-grow: 1;
//   flex-basis: 100%;
//   overflow: auto;
// }

// .editor-clm {
//   display: flex;
//   flex-direction: column;
// }

// .gjs-blocks-c {
//   justify-content: center;
//   height: 50px;
// }

// .gjs-block {
//   width: auto;
//   font-size: 5px;
//   justify-content: center;
//   height: auto;
//   min-height: auto;
// }

// .gjs-block-label {
//   display: none;
// }

// .gjs-cv-canvas {
//   width: 100%;
//   height: 100%;
//   top: 0;
// }

// .gjs-blocks-cs {
//   border: 1px solid rgba(0, 0, 0, 0.3);
//   border-top: none;
// }

// /* Theming */
// .gjs-one-bg {
//   background-color: #242a3b;
// }

// .gjs-two-color {
//   color: #9ca8bb;
// }

// .gjs-three-bg {
//   background-color: #1e8fe1;
//   color: white;
// }

// .gjs-four-color,
// .gjs-four-color-h:hover {
//   color: #1e8fe1;
// }
</style>