[https://stackoverflow.com/questions/56916532/difference-b-w-only-exclude-and-omit-pick-exclude-typescript](https://stackoverflow.com/questions/56916532/difference-b-w-only-exclude-and-omit-pick-exclude-typescript)

type test = number | string;

type test2 = string extends test ? true : false;

type test99 = keyof test;

type test100 = Exclude<string, {length: Function}>

type test3 = { a?: string; b?: string; c: string };

type test4 = test3 extends { c?: string } ? true : false;
