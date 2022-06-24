Vim-Notes
===

_Yet another note plugin for VIM_

[Basic Tests](https://github.com/fmount/vim-notes/actions/workflows/basic_test.yml)

Commands
---
| Command | Description |
|---|---|
|**:Note**&nbsp;_filename_      | This command creates a new Note buffer. This is saved in a new file inside the folder g:notes_folder (set to ~/.notes by default). If no extension is specified the new file will be created with '.note' and it will be processed in the editor using the _markdown_ syntax highlighting. |
|**:NoteList**             | Shows all the notes available inside the folder g:notes_folder |
|**:NoteDelete**&nbsp;_filename_|  Delete a note |
|**:NoteAutoSaveToggle** | Activate/Deactivate automatic save for the current _.note_ buffer |

______


Parameters
---
| Parameter | Default Value | Description |
|-----------|:-------------:|-------------|
|g:notes_folder| $HOME/.notes   | Folder containing the notes |
|g:notes_autosave| 0        | Enable/Disable the autosave of the notes |
|g:notes_autosave_time| 30  | Defines the minimum interval between 2 successive automatic saves |
|g:notes_compiler| markdown   | Defines the compiler for note files |
|g:notes_export_folder| $HOME/.notes/md2html   | Folder containing the exported notes |
|g:default_keymap| 1   | Load the default plugin keymap |
|g:notes_template_path | $HOME/.notes/templates/template.M  | The template used for notes |
|g:notes_template_autogen | 0 | Autogenerate template folder and template.M sample file  |


______


Editing key mapping
---
|Combination | Modes   | Name function | Description |
|------------| :-----: | :-----------: | ----------- |
|&lt;_leader_&gt;&nbsp;+&nbsp;[i| I / N   | note-new-cbox-inline | Create a new checkbox inline |
|&lt;_leader_&gt;&nbsp;+&nbsp;[o| I / N   | note-new-cbox-below  | Create a new checkbox in the line below the current one|
|&lt;_leader_&gt;&nbsp;+&nbsp;[O| I / N   | note-new-cbox-above | Create a new checkbox in the line above the current one|
|&lt;_leader_&gt;&nbsp;+&nbsp;[x|  N      | notes#toggle_checkbox | Toggle the state of the checkbox between done and undone ([x]/[ ])|


______


Fast Export key mapping
---
|Combination | Modes   | Name function | Description |
|------------| :-----: | :-----------: | ----------- |
|&lt;_leader_&gt;&nbsp;+&nbsp;[e| N   | notes#export | Export the current note buffer in a specified folder|


______


Key mapping override
---
The plugin sets by default all the described key mappings, but this can be easily disabled.
For instance, if you want your set of customized keybindings, you can just edit the vimrc as follows:

    "Disable the default key mapping
    let g:default_keymap = 0

    "Apply your own key mapping
    nmap <Leader>ni (note-new-cbox-inline)
    nmap <Leader>ni (note-new-cbox-inline)
    imap <Leader>ni (note-new-cbox-inline)
    nmap <Leader>no (note-new-cbox-below)
    imap <Leader>no (note-new-cbox-below)
    nmap <Leader>nO (note-new-cbox-above)
    imap <Leader>nO (note-new-cbox-above)
    nmap <Leader>nx :call notes#toggle_checkbox(line('.'))<cr>
    " Fast Export function
    nmap <leader>ne :call notes#export() <cr>


______


Customizing templates
---
The plugin supports writing notes based on user-defined templates.
You can either define a particular path where a note template is stored (and set it in your vimrc):

    g:notes_template_path = <template_dir>/<template_file>

or let the plugin configure a default path and generate a sample template for you.
In this case, you just need to set in your vimrc the following variable:

    g:notes_template_autogen = 1

and both the template directory and the sample file are generated according to the defaults
specified in the table above.

`g:notes_template_autogen` is set to 0 by default, which means that even though the feature
is enabled, you don't take advantage of it until one of the described variables is set.
By keeping `g:notes_template_autogen = 0`, you can either choose to manually set a template
path that can be used, or do not use this feature at all.

## Note

The autogenerated template path depends on the value of the `g:notes_folder`, hence the `templates/`
directory is nested to the main `g:notes_folder`, which represents the main working area where the
notes are stored.

e.g. assuming `g:notes_folder = "$HOME/.notes"`, the resulting templates/ directory will be something
like:

    > tree ~/.notes/templates
    ~/.notes/templates
    └── template.M
