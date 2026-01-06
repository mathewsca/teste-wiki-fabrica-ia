# Governança de Commits e Branching

Em nossos projetos, utilizaremos padrões e convenções para o processo de desenvolvimento de software, tais como GitFlow, Conventional Commits e Semantic Versioning. É de suma importância que você que faz parte do Fábrica de IA, compreenda os conceitos desses padrões e convenções para melhor integração com o time de desenvolvimento e seu desenvolvimento no geral realizando sua demandas. Parra isso, recomendamos os seguintes artigos para um melhor entendimento.

[GitFlow](https://www.alura.com.br/artigos/git-flow-o-que-e-como-quando-utilizar?utm_term=&utm_campaign=%5BAO%5D+%5BPerformance+Max%5D+%5BVenda%5D&utm_source=google&utm_medium=cpc&campaign_id=22048829191__&utm_id=22048829191__&hsa_acc=7964138385&hsa_cam=%5BAO%5D+%5BPerformance+Max%5D+%5BVenda%5D&hsa_grp=&hsa_ad=&hsa_src=x&hsa_tgt=&hsa_kw=&hsa_mt=&hsa_net=google&hsa_ver=3&gad_source=1&gad_campaignid=22038890376&gbraid=0AAAAADpqZICRpGUxhEUIBkY2UCfG-Dw5I&gclid=CjwKCAjwmNLHBhA4EiwA3ts3mQHUos8Ws2D2o__J2Dvks1HIxBeRGdU49YMkfumrEM9oGxpFT_rXbRoCOCgQAvD_BwE)<br>
[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)<br>
[Semantic Versioning](https://semver.org/)

Em nossos projetos, teremos as seguintes branchs, master, develop, hotfix, release, feature e support. Quando falarmos em mergeamento, estaremos nos referindo no sentido de baixo pra cima do fluxo GitFlow.


![GitFlow](https://cdn-wcsm.alura.com.br/2025/04/imagem3-50.png)

**master**: A branch master (ou main) armazena o código-fonte oficial em produção. Ela é o destino final onde todas as novas funcionalidades, após concluídas e validadas, são integradas. Sempre após alguma interação, o número da minor version sobre (xYz, x1z -> x2z). <br>
_Criado de: início do projeto._<br>
_Mergeamento para: Produção._<br>
_Base para criação de: hotfix e develop_

**develop**: Esta branch serve como a principal linha de integração, consolidando todas as funcionalidades recém-desenvolvidas. Ela representa o estado 'pré-produção' do código, agrupando mudanças que estão prontas para o próximo deploy e que, futuramente, serão incorporadas à master.<br>
_Criado de: develop e hotfix._<br>
_Mergeamento para: release._<br>
_Base para criação de: feature e support._

**hotfix**: É uma branch de curto prazo criada para resolver algum bug, problema ou modificação na master, após sua implementação na master, necessário também mergeamento com develop.<br>
_Criado de: master._<br>
_Mergeamento para: master._<br>
_Base para criação de: develop._

**release**: A branch release é um intermediário de curta duração entre a develop e a master. O seu objetivo principal é servir ao ambiente de homologação. Correções de última hora são aplicadas nela e devem ser sincronizadas de volta para a develop. Após os testes serem concluídos e a versão ser oficialmente lançada (mergeada na master), esta branch é excluída.<br>
_Criado de: develop._<br>
_Mergeamento para: master._<br>
_Base para criação de: novas develop após algum tipo de implementação de última hora._

**feature**: Esta branch é responsável pela criação de novas funcionalidades em nosso sistema, cada demanda (nova funcionalidade) atribuida a algum desenvolvedor, é feita nesta branch específica e depois mergeada para a develop.<br>
_Criado de: develop._<br>
_Mergeamento para: develop._<br>
_Base para criação de: nenhuma._

**support**: Esta branch é exclusiva para solução de bug ou alterações necessárias/encontrados após a nova funcionalidade ser implementada em develop.<br>
_Criado de: develop._<br>
_Mergeamento para: develop._<br>
_Base para criação de: nenhuma._

Sobre o semantinc versioning, utilizaremos XYZ, onde X é a versão maior, Y é versão menor e Z é a versão de patch.<br>
X: É alterada quando o serviço sofre uma mudança consiverável (possívelmente um breackchange), esta mudança e decisão é feita pelos líderes técnicos.<br>
Y: É alterado quando é mergeado mudanças da release pra master.<br>
Z: É alterado sempre que temos uma nova release.

# Padrão de criação de branchs

[branch]/[sua demanda em 3 palavras separadas por hífen]-[número indentificador do seu card]

### Exemplos

_feature/implementa-novo-botao-123 <br>_
_support/corrige-bug-botao-456 <br>_
_hotfix/falha-botao-producao-546 <br>_
_release/pacote-novas-funcionalidades-147_

# Padrão de commits

Para commits, utlizaremos o Padrão de Modo Imperativo (Imperative Mood). A regra central é que a mensagem de commit deve ser escrita como um comando ou uma ordem. Os benefícios são principalmente clareza, consistência e profissionalismo no histórico do projeto.

Exemplos:

CORRETO<br>
_"Implementa/ajusta/modifica/adiciona [Sua demanda]."_

ERRADO<br>
_"implementando [Sua demanda]."_





