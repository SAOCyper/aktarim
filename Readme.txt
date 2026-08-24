"compile": "lerna run --scope=\"@uzay/gsc-core-extension\" build && lerna run --scope=\"@uzay/*\" build --concurrency=1 && lerna run compile",
        "build:extensions": "lerna run --scope=\"@uzay/gsc-core-extension\" build && lerna run --scope=\"@uzay/*\" build --concurrency=1",
