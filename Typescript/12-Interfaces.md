# Interfaces
```ts
interface IAddress{

    address: string

    city: string
}

interface IUser{

    firstName: string

    lastName: string

    fullName: () => string

    address?: IAddress
}

const obj: IUser = {

    firstName: "",

    lastName: "",

    fullName: function (): string {

        return this.firstName + ' ' + this.lastName
    }
}

interface Person{

    name: string

    age: number

    calculate(input: number): number // dessa forma estamos tratando como método

    getName: () => string // dessa forma estamos tratando como propriedade

}

class Test implements Person{

    name: string

    age: number

    getName: () => string

    constructor(name: string, age: number, ){

        this.name = name

        this.age = age

        this.getName = () => {

            return this.name

        }

    }

    calculate(input: number): number {

        return input * 10
    }
}
```