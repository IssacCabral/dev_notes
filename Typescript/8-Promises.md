```ts
type User = {

    name: string,

    points: number
}

function sleep(time: number): Promise<void>{
    return new Promise((res) => {
        setTimeout(res, time)
    })
}

async function Promessa(): Promise<number>{
    console.log('cai aqui')

    return 16
}

async function main(){

    const issac: User = {

        name: 'issac',

        points: 1

    }
  
    await sleep(5000)

    console.log('eae')

    // Promessa().then(result => {

    //     console.log(result)

    // }).catch(err => {

    //     console.log(err)

    // })

    let result = await Promessa()

    console.log(result)
    console.log('fim da main')

}

main()
```
[[9-Classes]]