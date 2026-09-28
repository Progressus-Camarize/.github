# Política de Segurança

O Camarize é um projeto acadêmico da equipe Progressus (FATEC Registro, DSM). Levamos a segurança a sério, principalmente por lidar com autenticação de usuários e credenciais de serviços em nuvem.

## Versões com suporte

Apenas a branch `main` de cada repositório recebe correções.

## Como reportar uma vulnerabilidade

**Não abra uma issue pública.** Use o relato privado do GitHub:

1. Abra o repositório afetado.
2. Vá na aba **Security**.
3. Clique em **Report a vulnerability**.

Inclua, se possível: o repositório e o arquivo afetados, os passos para reproduzir e o impacto que você percebeu.

Vamos confirmar o recebimento assim que possível e manter você informado sobre a correção. Por ser um projeto mantido por estudantes, não há prazo formal de resposta.

## Credenciais expostas

Se você encontrar uma senha, token ou chave em qualquer repositório da organização (no código ou no histórico), reporte pelo mesmo canal. Não teste a credencial.

## Para quem contribui

- Nunca faça commit de arquivos `.env`, senhas, tokens ou chaves. Use variáveis de ambiente.
- Arquivos `*.example` devem conter apenas valores fictícios, como `SENHA_AQUI`.
- Scripts não devem ter connection strings embutidas. Leia de `process.env`.
- Se uma credencial vazar, **rotacione-a primeiro** e só depois limpe o histórico. Apagar o commit não invalida a senha.
