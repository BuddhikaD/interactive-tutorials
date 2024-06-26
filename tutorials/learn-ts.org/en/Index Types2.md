### Index Types

Tutorial
-------
Using index types, you can get the compiler to check code that uses dynamic property names. It provides a way to set the type of an object's keys and values.

    function pluck<T, K extends keyof T>(obj: T, keys: K[]): T[K][] {
        return keys.map(key => obj[key]);
    }

Exercise
-------
Define a function that takes an object and an array of keys and returns an object with just those keys.

Tutorial Code
-------
    function pick<T, K extends keyof T>(obj: T, keys: K[]): /* Return type here */ {
        // Your code here
        return {};
    }
    pick({name: "John", age: 30, city: "NY"}, ["name", "age"]);

Expected Output
-------
    { name: "John", age: 30 }

Solution
-------
    function pick<T, K extends keyof T>(obj: T, keys: K[]): Pick<T, K> {
        let result: any = {};
        keys.forEach(key => {
            result[key] = obj[key];
        });
        return result;
    }
    pick({name: "John", age: 30, city: "NY"}, ["name", "age"]);