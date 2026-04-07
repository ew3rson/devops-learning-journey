# 📓 CI/CD pipeline | anotações

este documento contém anotações sobre pipeline CI/CD com o objetivo de consolidar a compreensão de seus fundamentos e processos.

---

> [!NOTE]
> chamamos de **pipeline** o processo de automatizar, em etapas, o fluxo de trabalho dos processos descritos abaixo.

## CI — Integração Contínua

sem CI, é comum que desenvolvedores implementem funções ou melhorias no código do software e as mantenham para si até acharem que devem gerar o *commit* para a sua *branch*, deixando o código isolado por longos períodos e realizando *merges* com pouca frequência.

a **Integração Contínua** é a prática de realizar *commits* **regulares** de pequenas mudanças — ao invés de esperar essas pequenas mudanças se acumularem — dessa forma, as **alterações** passam por testes assim que são enviadas para a *branch* da pessoa desenvolvedora e o **feedback** e **correções** de bugs ou erros são realizados de forma *rápida* e *eficaz*.

testar e **validar** as alterações **antes** mesmo de **chegarem** à *branch main* é uma prática eficaz pois garante o controle de qualidade, mantém a integridade do código principal e facilita a **implantação** das alterações quando for a hora de mesclá-las à *branch main*.

>[!TIP]
*"commit small. frequently. test fast. fix early."* — Nana Janashia

## CD — Entrega Contínua

Entrega Contínua é o conjunto de práticas que tem como objetivo **manter** a aplicação sempre em um **estado implantável**. 

para isso, estima-se quanto tempo leva para a aplicação chegar ao usuário final desde o momento em que o time inicia seu desenvolvimento — esse tempo é chamado de ***cycle time*** — busca-se reduzir o ***cycle time*** o máximo possível, pois ele reflete a eficiência e **otimização dos processos**. 

aliada à Integração Contínua, a Entrega Contínua fornece uma abordagem estruturada ao desenvolvimento de software, permitindo a experimentação segura do código e a tomada de riscos sem grandes consequências.

por meio da automação de processos, ambientes de teste e monitoramento, a Entrega Contínua permite que cada *commit* seja um ***release candidate***.

## Continuous Deployment

Continuous Deployment trata-se da **automação** do processo de ***deploy***, ou seja, a implantação do software para que o usuário final tenha acesso é feita de forma automatizada.

Há também as chamadas 'estratégias de *deployment*' que controlam os riscos após o *deploy* da aplicação e permitem seu acompanhamento aliado a ferramentas de observabilidade.

 - **canary deployment**: o *deploy* é feito de maneira **gradual**, dessa forma é possível **observar** como a versão nova se comporta com um **número** de usuários **menor**.
 - **blue-green deployment**: são criados **dois ambientes idênticos**, mas separados; um deles roda a **versão atual** do software e o outro roda a **versão nova**, dessa forma, se algo sair diferente do planejado, é possível **reverter** a versão nova à **anterior**.

## fluxo da pipeline

***time dev***
1. **plan** — planejamento do código. 
2. **code** — desenvolvimento do código e gerenciamento das suas versões.
3. **build** — o código do software é transformado em um artefato executável.  
4. **test** — o software passa por testes em busca de bugs ou erros.
5. **release** — caso o software passe nos testes ele é enviado para a próxima fase.

***time ops***
1. **deploy** — o código é implantado em um ambiente de trabalho.
2. **operate** — é realizada a operação e manutenção do software.
3. **monitor** — após implantação, o software passa por testes e é monitorado continuamente para a coleta de feedback.
4. **feedback loop** — o feedback coletado volta à fase de planejamento, fechando o ciclo de feedback contínuo.