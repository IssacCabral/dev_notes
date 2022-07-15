Podemos mexer com o corpo da requisição como no exemplo abaixo,
está bem intuitivo então essa parte não explicarei muita coisa

```ts
export default class UsersController {
  public async store({request, response, logger, route}: HttpContextContract) {
    const {email} = request.only(['email'])
    const body = request.body()
    const all = request.all()

    // E agora quando fizermos a requisição teremos informação da máquina de quem fez
    // essa requisição
    logger.info('create of the user')

    // informações da rota
    console.log(route)
    
    response.json({email: email, body, all})
  }
}
```