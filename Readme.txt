{
    "compilerOptions": {
        "target": "ES2020",
        "module": "commonjs",
        "lib": [
            "ES2020",
            "DOM"
        ],
        "outDir": "lib",
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
            ]
        }
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
