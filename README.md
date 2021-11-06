# nj-request-scope
Performant request scope dependency injection for NestJS framework using express server

## Description
nj-request-scope library solves NestJs request-scope dependency injection problems:
* bubbling up the injection chain - [NestJS documentation](https://docs.nestjs.com/fundamentals/injection-scopes#scope-hierarchy)
* request-scope performance issues - [NestJS documentation](https://docs.nestjs.com/fundamentals/injection-scopes#performance)

This solution is based on the build-in javascript Proxy design pattern. For every request, only the proxy's target object is changed to the new request-scope instance instead of creating all injection chain objects.

## Installation
```console
npm install nj-request-scope
```

## Usage
To use nj-request-scope in NestJS module you have to add import of ```RequestScopeModule``` in the module class decorator:
```typescript
@Module({
    imports: [RequestScopeModule],
})
```

Next, there are two ways of using nj-request-scope.

1. Inject express request object into class constructor with ```REQUEST_PROVIDER``` token:
```typescript
constructor(@Inject(REQUEST_PROVIDER) private readonly request: Request) {}
```

2. Change class inject scope to request-scope with ```@RequestScope()``` decorator:
```typescript
@Injectable()
@RequestScope()
export class RequestScopeService {
```

## Limitations
Proxy handler implements only most common methods: ```get```, ```has```, ```set```. If you need other methods implemented please feel free to contribute. 
[ProxyHandler implementation](https://github.com/kugacz/nj-request-scope/blob/main/src/util/dynamic.object.handler.factory.ts)

## Example project
[https://github.com/kugacz/nj-request-scope-example](https://github.com/kugacz/nj-request-scope-example)

## License
nj-request-scope is [MIT licensed](LICENSE).
