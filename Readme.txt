{
    "compilerOptions": {
        "target": "ES2020",
        "module": "commonjs",
        "lib": [
            "ES2020",
            "DOM"
        ],
        "outDir": "lib",
        "rootDir": "src",
        "declaration": true,
        "declarationMap": true,
        "sourceMap": true,
        "strict": false,
        "strictPropertyInitialization": false,
        "experimentalDecorators": true,
        "emitDecoratorMetadata": true,
        "esModuleInterop": true,
        "skipLibCheck": true,
        "jsx": "react-jsx",
        "moduleResolution": "node",
        "baseUrl": ".",
        "paths": {
            "@theia/*": [
                "../../node_modules/@theia/*"
            ],
            "@lumino/*": [
                "../../node_modules/@lumino/*"
            ],
            "react": [
                "../../node_modules/@types/react"
            ],
            "inversify": [
                "../../node_modules/inversify"
            ],
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
        "src/**/*.ts",
        "src/**/*.tsx"
    ],
    "exclude": [
        "node_modules",
        "lib"
    ]
}
