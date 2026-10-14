# Festa de Fim de Ano – 5ª Cia PM

Controle de participantes (adultos, crianças de 6 a 12 e até 5 anos) e de pagamentos (1ª, 2ª e 3ª parcela).
Site estático (`index.html`) + Firebase (Authentication e Firestore). Publicação: GitHub → Vercel.

## 1. Firebase

1. Acesse https://console.firebase.google.com e crie um projeto (ex.: `festa-5cia`).
2. **Build → Authentication → Sign-in method**: ative **E-mail/senha**.
3. **Authentication → Users → Add user**: crie o(s) usuário(s) administrador(es) (e-mail e senha).
4. **Build → Firestore Database → Create database** (modo produção, região `southamerica-east1`).
5. **Firestore → Rules**: cole e publique:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /festa_fim_de_ano_participantes/{doc} {
      allow read, write: if request.auth != null;
    }
  }
}
```

6. **Configurações do projeto (engrenagem) → Seus apps → Web (`</>`)**: registre o app e copie o objeto `firebaseConfig`.
7. Cole os valores no `index.html`, no trecho marcado `COLE AQUI A CONFIGURAÇÃO DO SEU PROJETO FIREBASE`.
8. **Authentication → Settings → Authorized domains**: depois do deploy, adicione o domínio da Vercel (ex.: `festa-5cia.vercel.app`).

## 2. GitHub e Vercel

1. Crie um repositório (ex.: `festa-fim-de-ano-5cia`) e envie `index.html` e `README.md`.
2. Em https://vercel.com → **Add New → Project** → importe o repositório → **Deploy** (sem build, sem configurações extras).
3. Qualquer alteração enviada ao GitHub é publicada automaticamente.

## 3. Uso

- No primeiro acesso, o sistema cadastra sozinho os 64 policiais da lista no Firestore.
- **Participantes**: preencha adultos, crianças de 6 a 12 e crianças até 5 anos. Salva automaticamente.
- **Pagamentos**: toque em "Pendente" para marcar a parcela como "Pago" (toque de novo para desfazer).
- O campo de busca filtra as duas abas; os cartões do topo mostram os totais.
