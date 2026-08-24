{
    "extends": "../configs/base.tsconfig",
    "include": [],
    "compilerOptions": {
      "composite": true
    },
    "references": [
      {
        "path": "../extensions/gsc-core-extension"
      },
      {
        "path": "../extensions/gsc-earth-extension"
      },
      {
        "path": "../extensions/gsc-files-extension"
      },
      {
        "path": "../extensions/gsc-mission-extension"
      },
      {
        "path": "../extensions/gsc-moon-extension"
      },
      {
        "path": "../extensions/gsc-pass-control-extension"
      },
      {
        "path": "../extensions/gsc-pass-prediction-extension"
      },
      {
        "path": "../extensions/gsc-settings-extension"
      }
    ]
}
