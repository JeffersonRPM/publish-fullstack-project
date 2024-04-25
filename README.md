# Guia para publicar um projeto Full Stack de graça

## Primeiro passo

- Carregue o `front-end` e o `back-end` separadamente no Github

## Acesse a vercel: 
```
https://vercel.com/
```
- Faça o login com o Github

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/4bd7ddb9-9b80-4152-9f05-b701ec84d6fc)

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/9f6d97e0-ba67-4d9b-bb7d-5981b2891bd5)

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/6f524988-fa95-4fa4-9ec6-4c8497ff7fbf)

- Pemita o acesso da Vercel no projeto e depois salve

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/7b4bb88e-ffca-454e-8057-183efd2b7d9e)

- Clique em import

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/d4d380cb-cc70-492a-8a74-195458a21188)

- Renomeie o projeto
- Caso o Framework Preset seja o Node.js deixe em Other

## Acesse o Neon Tech

```
https://console.neon.tech/
```

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/5890b6cf-d4b2-46f7-a05f-54095466da10)

- Copie a Connection string

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/ba598217-f711-4739-a202-d23ad77bb533)

- Cole em Value (Will Be Encrypted), depois clique em `Add` e `Deploy`

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/c9c8e8d4-73bd-4443-ba94-ea5de4aa189f)

## No back-end utilizando Node.js vá no arquivo package.json e crie o `vercel-build`, no meu caso estou usando o prisma

```
"main": "mesmo caminho do start",

"scripts": {
    "start": "node (o caminho aqui deve ser o mesmo do main),
    "vercel-build": "npx prisma migrate deploy && npx prisma generate"
},
 ```

- Crie o arquivo `vercel.json` - aqui ja vamos configurar o acesso ao node

```
{
  "version": 2,
  "builds": [
    {
      "src": "caminho da main",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "(.*)",
      "dest": "caminho das rotas ou main"
    }
  ]
}
```

- Previnindo erro de Cors
```
const app = express();

app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', "aqui voce adiciona a URL do seu front-end");
  res.header('Access-Control-Allow-Headers', "*");
  res.header('Access-Control-Allow-Methods', "GET, POST, PUT, DELETE");
  app.use(cors());
  next();
});

```

- No back-end no arquivo principal JavaScript adicione:

```
const port = process.env.PORT || 8000;

app.listen(port, () => {
  console.log(`The server is running on port ${port}`);
});
```

## Acesse a Netlify
```
https://app.netlify.com/
```

- Mesmo procedimento do back-end será feito para o front-end, permita a Netlify acessar seu projeto do Github do front-end

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/45430aea-1292-42c7-b609-0e0f9b84e72c)

- Chegando nessa parte

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/75c42b34-0a81-46e1-bc07-01f8ba96f2fd)

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/85339098-b523-4033-bb2e-3e8c161006eb)

- No front-end caso tenha problemas com as rotas crie em `public` um arquivo chamado `_redirects` com essa linha de código
```
/*    /index.html   200
```

- No front-end acesse seu arquivo de conexão
```
import axios from "axios";

export const urlApi = 'linkdoseubackendaqui';

const Api = axios.create({
    baseURL: 'linkdoseubackendaqui',
});
 
export default Api;
```

`Agora é só acessar o link do front-end que a Netlify forneceu e testar, caso a site tenha adição de imagens infelizmente a Vercel não possui suporte para isso após o build (no back-end),caso tenha interesse seria necessario usar algum serviço cloud como a Aws, todas as imagens usadas até o build (do frond-end) serão carregadas normalmente de forma Statica`

## Bônus - Cron Job

- Acesse o cron-job.org
```
https://console.cron-job.org/
```
![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/b856769d-6db7-4be1-b2cc-3316a21233da)


- No arquivo principal JavaScript do back-end crie uma requisição do tipo GET com a rota /clear
```
app.get('/clear', async (req, res) => {
  console.log('Executando a tarefa de limpeza do banco de dados');
  try {
      await prisma.(tabela do bd).deleteMany();
      res.send('Limpeza do banco de dados concluída com sucesso');
  } catch (error) {
      console.error('Erro ao limpar o banco de dados', error);
      res.status(500).send(`Erro ao limpar o banco de dados: ${error.message}`);
  }
});
```

![image](https://github.com/JeffersonRPM/publish-fullstack-project/assets/48998618/c0cb9e0d-9727-4aa7-b86c-334ea357c486)






