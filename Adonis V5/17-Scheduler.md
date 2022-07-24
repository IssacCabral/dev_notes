### Instalação
```bash
yarn add adonis5-scheduler
```

### Configurando todas as dependências para conseguir acessar através do node ace

```bash
node ace invoke adonis5-scheduler
```

### Criando uma scheduler

```bash
node ace make:task [Task_name]
node ace make:task VerifyTimeItemInCart
```

resolva o erro  do arquivo gerado importando o logger do Adonis:

```ts
import { BaseTask } from 'adonis5-scheduler/build'
import Logger from '@ioc:Adonis/Core/Logger'

export default class VerifyTimeItemInCart extends BaseTask {
    public static get schedule() {
        return '* * * * * *'
    }

    public static get useLock() {
        return false
    }
  
    public async handle() {
        Logger.info('Handled')
    }

}
```

### Executando a scheduler
```bash
node ace scheduler:run
```

#### O que é uma scheduler?
- é um agendador, ela funciona como um alarme

Os asteriscos, cada posição significa o seguinte:

The cron format consists of:

```bash
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    │
│    │    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, OPTIONAL)
```

```ts
/**
   * Qualquer valor
   , separador de lista de valores
   - faixa de valores
   / valores de passo
*/
```

### Precisamos instalar uma lib para ficar verificando o tempo que já passou

```bash
yarn add dayjs
```


```ts
import { BaseTask } from 'adonis5-scheduler/build'

import Logger from '@ioc:Adonis/Core/Logger'
import dayjs from 'dayjs'

// plugin para setar qual localidade de horas que vamos trabalhar

import isLeapYear from 'dayjs/plugin/isLeapYear'
import 'dayjs/locale/pt-br'

import Cart from 'App/Models/Cart'

export default class VerifyTimeItemInCart extends BaseTask {
    /**
     * Qualquer valor
     , separador de lista de valores
     - faixa de valores
     / valores de passo

     */
    public static get schedule() {
        return '1 39 12 * * *'
    }

    /**
     * Set enable use .lock file for block run retry task
     * Lock file save to `build/tmpTaskLock`
     */
    public static get useLock() {
        return false
    }

    public async handle() {
        dayjs.extend(isLeapYear)
        dayjs.locale('pt-br')

        try{
            const itensCart = await Cart.all()
            
            await Promise.all(
                itensCart.map(async (item) => {
                    const {created_at} = item.serialize()
                    const newDateMoreThan1hour = dayjs(created_at).add(1, 'h').format()
                    const currentDate = dayjs().format()
                    
                    if(newDateMoreThan1hour < currentDate){
                        try{
                            await item.delete()
                            return Logger.info('Item removed')
                        } catch(error){
                            return Logger.error('Error in deleting item')
                        }
                    }
                })
            )

        } catch(error){

        }
    }
}
```


## Documentações  
Scheduler adonis V5 => https://www.npmjs.com/package/adonis5-scheduler  
Crontab => https://github.com/node-schedule/node-schedule#cron-style-scheduling  
DayJS => https://day.js.org/en/