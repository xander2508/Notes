### Module Manifest

A module manifest is a simple `.psd1` file that contains a hash table. The keys and values in the hash table perform the following functions:

- Describe the `contents` and `attributes` of the module.
- Define the `prerequisites`. ( specific modules from outside the module itself, variables, functions, etc.)
- Determine how the `components` are `processed`.

If you add a manifest file to the module folder, you can reference multiple files as a single unit by referencing the manifest. The `manifest` describes the following information:

- `Metadata` about the module, such as the module version number, the author, and the description.
- `Prerequisites` needed to import the module, such as the Windows PowerShell version, the common language runtime (CLR) version, and the required modules.
- `Processing` directives, such as the scripts, formats, and types to process.
- `Restrictions` on the module members to export, such as the aliases, functions, variables, and cmdlets to export.

We can quickly create a manifest file by utilizing `New-ModuleManifest` and specifying where we want it placed.

```powershell-session
New-ModuleManifest -Path C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon\quick-recon.psd1 -PassThru
```

The `-PassThru` modifier lets us see what is being printed in the file and on the console.