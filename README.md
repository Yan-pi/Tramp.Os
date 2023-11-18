# Documentação do Projeto Tramp.Os

## Introdução

Bem-vindo à documentação oficial do projeto Tramp.Os, uma aplicação mobile desenvolvida em React Native com Expo. Este projeto foi realizado como parte dos estudos em uma disciplina da faculdade e utiliza a API Jsearch da RapidAPI para buscar oportunidades de trabalho e exibi-las no aplicativo.

### Estrutura do Projeto
___

O projeto está estruturado da seguinte forma:
(major folder structure)

```
Tramp.Os/
|-- app/
|   |-- jobdetails/
|   |-- search/
|   |-- _layout.js
|   |-- home.js
|   |-- index.js
|-- assets/
|   |-- fonts/
|   |-- icons/
|   |-- images/
|-- components/
|   |-- common/
|	|   |-- cards/
|	|   |-- header/
|   |-- home/
|	|   |-- nearby/
|	|   |-- popular/
|	|   |-- welcome/
|   |-- jobdetails/
|	|   |-- about/
|	|   |-- company/
|	|   |-- footer/
|	|   |-- specifics/
|	|   |-- tabs/
|   |-- index.js
|-- constants/
|   |-- icons.js
|   |-- images.js
|   |-- index.js
|   |-- theme.js
|   hook/
|   |-- useFetch.js
|-- styles/
|   |-- search.js
|-- utils/
|   |-- index.js
|-- package.json
|-- ...
```

- A pasta /components/` contém componentes reutilizáveis.

- A pasta `hooks/` contém o arquivo `useFetch`, responsável por realizar as chamadas à API Jsearch usando o Axios.

## Configuração do Ambiente
___

Certifique-se de ter o Node.js, o Expo CLI e o Yarn (ou npm) instalados no seu ambiente de desenvolvimento. Se não tiver, siga as instruções na documentação oficial do [Expo](https://docs.expo.dev/get-started/installation/).

```bash
# Instale o Expo CLI globalmente
npm install -g expo-cli

# Instale as dependências do projeto
npm install
```

## Dependências do Projeto
_____

O Tramp.Os utiliza diversas dependências essenciais para o desenvolvimento e funcionamento adequado da aplicação. Abaixo estão as principais dependências, junto com uma breve explicação do papel de cada uma:

### [Expo](https://docs.expo.dev/)

O Expo é uma plataforma que facilita o desenvolvimento de aplicativos React Native, fornecendo ferramentas e serviços adicionais. Ele simplifica tarefas como o acesso a recursos nativos do dispositivo, facilitando o desenvolvimento multiplataforma.

```bash
# Instalação do Expo CLI
npm install -g expo-cli
```

### [React Native](https://reactnative.dev/)

O React Native é um framework para criar aplicativos móveis usando React e JavaScript. Ele permite o desenvolvimento de aplicativos nativos para iOS e Android com uma base de código comum.

```bash
# Instalação do React Native
npm install react-native
```

### [Axios](https://axios-http.com/)

O Axios é um cliente HTTP baseado em Promises utilizado para fazer requisições HTTP. Ele simplifica o processo de comunicação com APIs, fornecendo uma interface fácil de usar para realizar solicitações e lidar com respostas.

```bash
# Instalação do Axios
npm install axios
```

### [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

O JavaScript é a linguagem de programação utilizada para desenvolver a lógica e a interação dinâmica no Tramp.Os. Ele é a principal linguagem de programação para o desenvolvimento web e móvel, proporcionando a capacidade de criar aplicações interativas e responsivas.

Não é necessário instalar o JavaScript separadamente, pois é interpretado pelos navegadores ou pelo ambiente Node.js.

## Configuração da API Jsearch
_____

O projeto utiliza a API Jsearch da RapidAPI para buscar oportunidades de trabalho. Para configurar a API, siga estes passos:

1. Acesse [RapidAPI](https://rapidapi.com/).
2. Crie uma conta ou faça login, se já tiver uma.
3. Assine o plano gratuito da Jsearch API.
4. Obtenha a chave da API Jsearch na página de configurações da RapidAPI.
5. Substitua a chave da API no arquivo `hook/useFetch.js`.

```javascript
// src/services/api.js

import { useState, useEffect } from "react";
import axios from "axios";

const useFetch = (endpoint, query) => {
  const [data, setData] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);
  
  const options = {
    method: "GET",
    url: `https://jsearch.p.rapidapi.com/${endpoint}`,
    headers: {
      "X-RapidAPI-Key": 'YOUR_API_KEY',
      "X-RapidAPI-Host": "jsearch.p.rapidapi.com",
    },
    params: { ...query },
  };

  
  const fetchData = async () => {
    setIsLoading(true);
    try {
      const response = await axios.request(options);
  
      setData(response.data.data);
      setIsLoading(false);
    } catch (error) {
      setError(error);
      console.log(error)
    } finally {
      setIsLoading(false);
    }
  };

  
  useEffect(() => {
    fetchData();
  }, []);

  const refetch = () => {
    setIsLoading(true);
    fetchData();
  };

  return { data, isLoading, error, refetch };
};
  

export default useFetch;
```

## Executando o Projeto
____

Com as dependências instaladas e a chave da API configurada, você pode iniciar o projeto com o seguinte comando:

```bash
npx expo start
```

Isso abrirá o Expo Developer Tools no seu navegador. Você pode então executar o aplicativo em um emulador ou em um dispositivo físico usando o aplicativo Expo Go.

## Observações

Este projeto foi desenvolvido com base em um tutorial e como parte de um projeto acadêmico. Se você encontrar dificuldades ou quiser contribuir, sinta-se à vontade para abrir um problema ou enviar uma solicitação de pull no repositório do GitHub.

GitHub do Projeto: [Tramp.Os]([https://github.com/seu-username/tramp-os](https://github.com/Yan-pi/Tramp.Os))

---

Esperamos que esta documentação seja útil para entender a estrutura e configurar o ambiente para o projeto Tramp.Os. Se tiver dúvidas adicionais, consulte a documentação oficial do [Expo](https://docs.expo.dev/) e do [React Native](https://reactnative.dev/docs/getting-started).
