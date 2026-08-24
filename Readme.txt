{
    "compilerOptions": {
        "module": "commonjs",
        "moduleResolution": "node",
        "baseUrl": ".",
        "target": "es2017",
        "lib": [
            "es6",
            "dom"
        ],
        "sourceMap": true,
        "rootDir": "src",
        "outDir": "lib",
        "strict": true,
        "esModuleInterop": true,
        "jsx": "react",
        "experimentalDecorators": true,
        "emitDecoratorMetadata": true,
        "noImplicitAny": false,
        "skipLibCheck": true,
        "paths": {
            "@uzay/gsc-core-extension": [
                "../gsc-core-extension/src/browser/common-index.ts",
                "../gsc-core-extension/lib/browser/common-index.d.ts",
                "../gsc-core-extension",
                "../../node_modules/@uzay/gsc-core-extension"
            ],
            "@uzay/*": [
                "../gsc-core-extension/src/browser/common-index.ts",
                "../*",
                "../../node_modules/@uzay/*"
            ]
        },
        "references": [
            {
                "path": "../gsc-core-extension"
            }
        ]
    },
    "include": [
        "src/**/*"
    ]
}
