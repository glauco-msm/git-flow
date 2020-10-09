# git-flow
Processo de fluxo do Git

# Branches de base

- Branch de produção: ***main***
- Branch de teste e versionamento: ***release***
- Branch do próximo release: ***develop***

# Como nomear branches

- Branch de feature: ***feat/[feature-name]***
- Branch de bug fix em desenvolvimento: ***fix/[fix-description]***
- Branch de bug fix em produção: ***hotfix/[hotfix-description]***
- Branch de release: ***release/v.1.00-b10***
- Branch de refactor: ***ref/[ref-description]***
- Branch de configuração/update de bibliotecas: ***chore/[chore-description]***

# Regras de nomenclatura

- Sempre escrito em inglês;
- Sempre escrito em minúsculo;
- Usar apenas letras e números, quando precisar utilizar espaço, usar o
caracter ***-***. Exemplo: ***feat/new-login***. Para tags de release, usar
pontos. Exemplo: ***release-v1.0.0-b51***;
- Para branches compartilhadas entre devs, utilizar as iniciais do
primeiro e último nome do dev na descrição da branch. Exemplo: ***feat/gm-new-login***.

# Features

Crie a branch a partir da branch ***develop***, use o prefixo ***feat/*** e o nome da
feature.

Flow:
- Start: ***develop*** – create branch >> ***feat/login*** 
- Done: ***feat/login*** – merge >> ***develop***

### Múltiplos devs:

Quando houver mais de um desenvolvedor trabalhando na mesma branch, crie branches secundárias a partir da branch da feature ***feat/[feature-name]***, usando as iniciais do desenvolvedor como prefixo da descrição da branch:

Flow:
- Feature start: ***develop*** – create branch >> ***feat/login***
- Dev-1 start: ***feat/login*** – create branch >> ***feat/ey-login*** 
- Dev-2 start: ***feat/login*** – create branch >> ***feat/gm-login*** 
- Dev-1 done: ***feat/ey-login*** – merge >> ***feat/login*** 
- Feature done: ***feat/login*** –merge >> ***develop***

### Note:
Nesse caso, a branch com as iniciais do desenvolvedor, só pode fazer merge com a branch base da feature, nunca com a ***develop*** ou qualquer outra. A branch que faz merge com ***develop*** é apenas a branch base.

# Refactor

Crie a branch a partir da branch ***develop*** para refazer alguma feature ou
código, use o prefixo ***ref/*** e a descrição do refactor. 

Flow:

- Start: ***develop*** – create branch >> ***ref/add-swiftlint*** 
- Done: ***ref/add-swiftlint*** – merge >> ***develop***

# Hotfix

Crie a branch a partir da branch ***main*** quando encotrar erros em produção e junte ela a branch ***develop***, para que as correções sejam inclusas nos próximos deploys também. Quando houver necessidade de fazer algum hotfix, use o prefixo ***hotfix/*** e a descrição do ***hotfix***.
  
Flow:

- Start: ***main*** – create branch >> ***hotfix/login*** 
- Update develop: ***hotfix/login*** – merge >> ***develop*** 
- Done: ***develop*** – merge >> ***main***

# Fix

Crie a branch a partir da branch ***develop*** para consertar erros que aparecem durante o desenvolvimento, use o prefixo ***fix/*** e a descrição do reactor. 

Flow:

- Start: ***develop*** – create branch >> ***fix/login*** 
- Done: ***fix/login*** – merge >> ***develop***

# Chore

Crie a branch a partir da branch ***develop*** para estruturar mudanças de bibliotecas, configurações e pequenos ajustes, use o prefixo ***chore/*** e a descrição do reactor. 

Flow:

- Start: ***develop*** – create branch >> ***chore/update-reactnative*** 
- Done: ***chore/update-reactnative*** – merge >> ***develop***

# Release

A branch ***release*** recebe merge da branch ***develop***. Aqui é feito o versionamento e criado a tag para submeter para as lojas (Apple Store e Google Play):

***Exemplo:***

```
$ git checkout -b release
$ git merge develop
$ git add .
$ git commit -m “Bumps version to v1.0.1-b10”
$ git tag -a release- v1.0.1-b10 -m  ́tagging release- v1.0.1-b10 ́ 
$ git push origin release
$ git push –tags
```
Flow:
- Start: ***develop*** – merge >> ***release***
- Done: ***release*** – create tag >> ***release- v1.0.1-b10***

# Main
Após a aprovação nas lojas, deve ser criado uma branch a partir da tag de release ***release- v1.0.1-b10*** e após isso fazer o merge com a ***main***, para que a ***main*** sempre mantenha a versão que está em produção na loja. Após o merge com ***main***, a branch de ***release*** deve ser removida.

***Exemplo:***

```
$ git checkout -b release- v1.0.1-b10 
$ git checkout master
$ git merge release- v1.0.1-b10
$ git push origin
$ git branch -d release- v1.0.1-b10
```

Flow:
- Store: ***release- v1.0.1-b10*** – create branch >> ***release- v1.0.1-b10*** 
- Update master: ***release- v1.0.1-b10*** – merge >> ***release- v1.0.1-b10*** 
- Done: ***release- v1.0.1-b10*** – >> remove branch
