# AVM Worker common types

[![npm](https://img.shields.io/npm/v/@fluencelabs/avm-worker-common)](https://www.npmjs.com/package/@fluencelabs/avm-worker-common)

AVM Worker is the abstraction over Aqua virtual machine (AVM) interpreter designed to allow run it in different contexts such as web workers in browsers or worker threads on nodejs. 

The package provides common interface for AVM worker implementation as well as necessary TypeScript definitions.

## Getting started

The main exports of the package is the AVM worker type :

```typescript
export type AvmWorker = {
    init: (logLevel: LogLevel) => Promise<void>;
    terminate: () => Promise<void>;
    run: (
        air: string,
        prevData: Uint8Array,
        data: Uint8Array,
        params: {
            initPeerId: string;
            currentPeerId: string;
        },
        callResults: CallResultsArray,
    ) => Promise<InterpreterResult>;
};
```

To make a custom AVM worker three functions has to be implemented:

* init - should allocate any resources needed for AVM worker (such as AVM interpreter memory or background worker state)
* terminate - should deallocate all the resources used by the AVM worker
* run - should pass the particle execution to actual AVM interpreter running in the context of implementation

## Available implementations:

-   Single-threaded, ui-blocking: [@fluencelabs/avm-worker](https://github.com/fluencelabs/avm-worker)
-   Web workers based for browsers: [@fluencelabs/avm-worker-web](https://github.com/fluencelabs/avm-worker-background/tree/main/avm-worker-node)
-   Worker threads based for nodejs: [@fluencelabs/avm-worker-node](https://github.com/fluencelabs/avm-worker-background/tree/main/avm-worker-node)

## Contributing

While the project is still in the early stages of development, you are welcome to track progress and contribute. As the project is undergoing rapid changes, interested contributors should contact the team before embarking on larger pieces of work. All contributors should consult with and agree to our [basic contributing rules](CONTRIBUTING.md).

## License

[Apache 2.0](LICENSE)
