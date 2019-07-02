# Angular Folder Structure

Recommended angular folder structure to use in your projects, as gathered from different source all over the web, and from own try-and-error.

```
|-- app
    |-- home
        |-- [+] components
        |-- [+] services
        |-- home-routing.module.ts
        |-- home.module.ts
    |
    |-- feature-module-1
        |-- [+] components
        |-- [+] services
        |-- feature.module.ts
    |
    |-- core
        |-- [+] authentication
        |-- [+] guards
        |-- [+] http
        |-- interceptors
            |-- http-error.interceptor.ts
        |
        |-- [+] mocks
        |-- services
            |-- hashing.service.ts
        |
        |-- core.module.ts
        |-- ensureModuleLoadedOnceGuard.ts
        |-- logger.service.ts
    |
    |-- shared
        |-- components
            |-- spinner component
            |-- 
        |    
        |-- [+] directives
        |-- [+] pipes
        |-- [+] models
        |-- [+] validators
        |-- [+] resolvers
        |-- [+] parsers
        |-- consts.ts
        |-- shared.module.ts
    |
    |-- utilities
        |-- datetime.utilities.ts
        |-- http.utilities.ts
    |
    |-- [+] configs
|-- assets
     |-- scss
          |-- [+] partials
          |-- _base.scss
          |-- styles.scss

```
## CoreModule

The CoreModule takes on the role of the root AppModule , but is not the module which gets bootstrapped by Angular at run-time.
Contains singleton services, universal components and other features where there’s only once instance per application. 
To prevent re-importing the core module elsewhere, you should also add a guard for it in the core module’ constructor.


    export class CoreModule {
        constructor(@Optional() @SkipSelf() parentModule: CoreModule) {
            throwIfAlreadyLoaded(parentModule, 'CoreModule');
        }
    }

## SharedModule

It is where any shared components, pipes/filters and services should go. The SharedModule can be imported in any other module when those items will be re-used. The shared module shouldn’t have any dependency to the rest of the application and should therefore not rely on any other module.

Shared modules would normally be imported potentially multiple times. Core modules on the other hand, should only be imported once and that should only happen into the root.
