# Bug repro
Right now, given this repo, you should just need to run `yarn` then `yarn cap run android` to recreate the issue. Details below on how this repo was created.

I've given you the repro for android, know that this does the same thing for iOS builds and Yarn 4.

I can, however open the project in android studio and run it from there.

## The stacktrace that is generated
```
[error] SyntaxError: Unexpected token 'E', "Error: spawn ENOTDIR" is not valid JSON
        at JSON.parse (<anonymous>)
        at getPlatformTargets
        (/Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/util/native-run.js:39:26)
        at async runAndroid
        (/Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/android/run.js:14:64)
        at async run
        (/Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/tasks/run.js:107:9)
        at async runCommand
        (/Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/tasks/run.js:81:13)
        at async
        /Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/index.js:129:9
        at async
        /Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/telemetry.js:26:13
        at async Command.<anonymous>
        (/Users/WHOAMI/.yarn/berry/cache/@capacitor-cli-npm-5.7.0-5a0dc1edf0-10c0.zip/node_modules/@capacitor/cli/dist/util/cli.js:12:13)
```

## Steps to reproduce (From scratch)
1. Before starting, have these dependendencies globally available
    - node v21.6.1
    - yarn 1.22.21
2. Then run `yarn init` to create the `package.json`
3. Manually add the `packageManager: "yarn@4.1.0"` field to your `package.json`
4. Run `yarn` to install `yarn@4.1.0`.
5. Confirm the yarn version `yarn --version`

### Commands
1. `yarn add @capacitor/core @capacitor/cli @ionic/utils-process`
2. `yarn cap init` (accept defaults)
3. `yarn add @capacitor/android`
3. `yarn cap add android`
4. `yarn cap sync`
5. `yarn cap run android`

### Expected
The android simulator runs

### Actual
A syntax error is thrown: `SyntaxError: Unexpected token 'E', "Error: spawn ENOTDIR" is not valid JSON`.