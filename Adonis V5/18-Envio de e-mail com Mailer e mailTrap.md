## Comandos 
- Instalação do mailer ⇒ 
```bash
yarn add @adonisjs/mail 
```

- Configuração do mailer ⇒ 
```bash
node ace configure @adonisjs/mail 
```

- Instalação de pacote para criação de templates html no adonisjs: 
```bash
yarn add @adonisjs/view
```

- Configuração do view ⇒ 
```bash
node ace configure @adonisjs/view
```
 
- Criação de uma nova view => 
```bash
node ace make:view {{nome da view}}
node ace make:view email/welcome
```

com isso, será gerado um arquivo welcome.edge que renderiza html, e lá colocamos o seguinte código html:

```html
<h1> Welcome {{user.name}} </h1>
<p>
    <a href="{{url}}">Click here </a> to verify your email address.
</p>
```

vamos criar um função dentro de Services para o envio de email:

```ts
import Mail from '@ioc:Adonis/Addons/Mail'
import User from "App/Models/User";

export async function sendEmail(user: User, template: string): Promise<void>{
    await Mail.send((message) => {
        message.from('merchandise-management@email.com')
            .to(user.email)
            .subject('Welcome to merchandise management!')
            .htmlView(template, {user})
    })

}
```

após isso, importamos e utilizamos essa função dentro do nosso controlador de usuários:

```ts
// send email service
try {
	await sendEmail(user, 'email/welcome')
} catch (error) {
	return response.badRequest({
	message: 'Error in send welcome email', 
	originalError: error.message})
}
```

e então, precisamos nos cadastrar no site de serviço para testar os envios de email [https://mailtrap.io/](https://mailtrap.io/)

após o cadastro, clicamos em SMTP settings e escolhemos Nodemailer como _Integrations_. copiamos o corpo que fica dentro do objeto de _transport_

```ts
var transport = nodemailer.createTransport({ 
	host: "smtp.mailtrap.io", 
	port: 2525, 
	auth: { 
		user: "dd392dc88335c5", 
		pass: "bdf17037e2ec01" 
	} 
});
```

e colocamos essas informações lá no arquivo _.env_

```bash
SMTP_HOST=smtp.mailtrap.io
SMTP_PORT=2525
SMTP_USERNAME=dd392dc88335c5
SMTP_PASSWORD=bdf17037e2ec01
```

