# object-oriented-tests-jest

**This package is a fork of the [@testdeck/jest](https://www.npmjs.com/package/@testdeck/jest)**

In this fork methods `beforeAll` and `afterAll` are instance of test class unlike the original package where they 
were static. This is made for easier and more convenient work with NestJS

The package provides a suite of decorators to integrate your favorite test framework into an object-oriented workflow.

## Object-Oriented API Usage
With object-oriented-tests-jest, writing object-oriented test suites is just a blaze.

```ts
import { suite, test } from "object-oriented-tests-jest";

class TestBase {
  @test
  basic() {
    // expected fail :/
    expect(true).toBe(false);
  }
}

@suite
class Hello extends TestBase {
  @test
  world() {
    // expected fail :/
    expect(false).toBe(true);
  }
}
```

## Benefits of the Object Oriented Style to work with NestJS

This fork was be created for next benefits:

We can once write a `BaseTestClass` like this:
```ts
class BaseTestClass {
  app: INestApplication;

  async beforeAll(): Promise<void> {
    const testModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    this.app = testModule.createNestApplication();
    await this.app.init();
  }

  async afterAll(): Promise<void> {
    await this.app.close();
  }
}
```

and then when we want create new test suite whe just write:
```ts
class Test extends BaseTestClass {
  async test(): Promise<void> {
    const result = await this.app.get(SomeService).someMethod();
    
    expect(result).toBeTruthy();
  }
}
```

## Standard Functional API Usage
With object-oriented-tests-jest, you can always use the standard functional test framework API:

```TypeScript
function basic() {
  it('basic', () => {
    // expected fail :/
    expect(true).toBe(false);
  });
}

describe('Hello', () => {
  basic();
  it('world', () => {
    // expected fail :/
    expect(false).toBe(true);
  });
})
```

And you can migrate your existing functional test suites to object-oriented over time.

## License

```
Copyright 2016-2022 Testdeck Team and Contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
