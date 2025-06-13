# Cross Origin Resource Sharing (CORS)
![cors](assets/cors.avif)

- [O que é cors](#o-que-é-cors)


## O que é CORS?
CORS - Cross-Origin Resource Sharing (Compartilhamento de recursos com origens diferentes) é um mecanismo de segurança que permite que recursos de uma página da web sejam solicitados de outro domínio diferente do que o recurso está hospedado. Isso é importante porque, por padrão, navegadores bloqueiam essas solicitações para proteger os usuários de ataques maliciosos, como o Cross-Site Scripting (XSS).

## Por que CORS é necessário?
Imagine que você tem um frontend (HTML, CSS, JavaScript) hospedado em https://meusite.com e uma API backend em https://api.meusite.com. Quando o frontend tenta fazer uma requisição para a API, o navegador bloqueia essa requisição por ser de origem diferente (domínio diferente). O CORS permite que você controle quais origens podem acessar os recursos do seu servidor.

## Cabeçalhos CORS Comuns
- **Access-Control-Allow-Origin**: Especifica quais domínios podem acessar o recurso. Pode ser um domínio específico (https://siteA.com) ou um curinga (*) para permitir qualquer origem.

- **Access-Control-Allow-Methods**: Indica quais métodos HTTP (GET, POST, etc.) são permitidos.

- **Access-Control-Allow-Headers**: Especifica quais cabeçalhos podem ser usados na solicitação.
Conclusão

Como habilitar CORS no Node.js?
Para habilitar CORS em um servidor Node.js, a maneira mais comum é usar o middleware cors da biblioteca express. Vamos ver um exemplo passo a passo.

Permitindo requisições de qualquer dominio
```javascript
app.use(cors());
  // Permite de qualquer dominio
```
Configurando dominio de origim da requisição
```javascript
app.use(cors({
  origin: 'https://meusite.com'
  // Permite apenas requisições de https://meusite.com
}));
```

Configurando Options
```javascript
const corsOptions = {
  origin: 'https://meusite.com',                // Permite apenas requisições de https://meusite.com
  methods: 'GET,HEAD,PUT,PATCH,POST,DELETE',    // Métodos HTTP permitidos
  allowedHeaders: 'Content-Type,Authorization', // Cabeçalhos permitidos
  credentials: true                             // Permite o envio de cookies
};

app.use(cors(corsOptions));
```