# MetaHub

![image](https://github.com/VictorBravim/MetaHub/assets/122113588/872b9eeb-e6df-4da2-944c-5c1704bbbab9)

## <code>Introdução</code>

MetaHub é um projeto de mídia social desenvolvido com React e Firebase. A plataforma permite aos usuários criar perfis personalizados, publicar conteúdo, seguir outros usuários e interagir com postagens por meio de curtidas. O aplicativo foi projetado para praticar integração com backend e banco de dados.

## <code>Pré-requisitos</code>

- Node.js
- Firestore
- React Router
- React Icons

## <code>Configuração</code>

1. Clone o repositório:

``` 
git clone https://github.com/VictorBravim/MetaHub.git
```

2. Navegue até o diretório do projeto:

```
cd MetaHub
```

3. Instale as dependências:

```
npm install
```

## <code>Estrutura</code>

- FireStore

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }

    match /users/{userId}/followers/{followerId} {
      allow write: if request.auth != null && request.auth.uid != null && request.auth.uid == followerId;
    }

    match /posts/{postId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
      allow delete: if request.auth != null && request.auth.uid == resource.data.userId;
    }
  }
}
```

- Storage

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /postImages/{userId}/{allPaths=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    match /profileImages/{userId}/{allPaths=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## <code>Licença</code>

- Este projeto está licenciado sob a [Licença MIT](LICENSE).
