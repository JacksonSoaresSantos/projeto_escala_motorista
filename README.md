# Contexto do Caso: Gerenciamento de Escala de Motoristas

## Situação Atual:

* **Processos de controle e planejamento manuais:** A empresa usa métodos manuais para planejar as escalas de motoristas, veículos e rotas, o que pode levar a erros e ineficiências.  
* **Dificuldade em gerenciar e otimizar rotas:** O planejamento manual das rotas diárias e semanais pode não ser o mais eficiente, considerando a necessidade de evitar que motoristas e veículos repitam as mesmas rotas em dias consecutivos.  
* **Falta de controle sobre a alocação de motoristas e veículos:** A gestão da escala de 20 motoristas e 20 veículos é complexa, e a falta de um sistema pode dificultar a distribuição justa e estratégica da carga de trabalho.  
* **Demora na geração de relatórios:** A criação manual de relatórios de rotas diárias e semanais (em formatos .pdf, .xlsx ou .docx) é um processo que consome tempo e pode atrasar a comunicação de informações importantes.  
* **Vulnerabilidade na segurança da informação:** As informações sensíveis dos motoristas, como CNH, classe e validade, são armazenadas de forma descentralizada ou em arquivos locais, sem um controle de acesso formalizado.

## Objetivo da Informatização:
* Aumentar a eficiência e a agilidade no **planejamento de escalas** e rotas.  
* Otimizar a **gestão da frota**, garantindo que motoristas e veículos sejam alocados de forma inteligente para evitar repetição de rotas.  
* Reduzir erros operacionais e retrabalho na **geração de relatórios**.  
* Centralizar e organizar as informações de motoristas (como dados da CNH) e veículos de forma segura.  
* Proporcionar uma experiência de usuário moderna e segura com um sistema centralizado, incluindo login de acesso e interfaces para cadastro, edição e atualização de dados.

## Papéis e Atores do Sistema

* **Motorista:** Realiza a consulta da sua escala.   
* **Líder:** Cadastrar, editar e, em alguns casos, deletar o registro de motoristas, rotas, projetos e carros. A exclusão de algum cadastro (motorista, rota, projeto e carros) será permitida apenas se nunca esteve incluído em uma escala (esteja ela finalizada ou não).  
* **Administrador do Sistema:** Gerenciar acessos e permissões, realizar backups, manter o sistema operacional.

## Requisito Funcional: Cadastro de Motoristas  
> **RF-001: Cadastro de Motoristas** O sistema deve permitir o cadastro de motoristas com foto, identificação funcional (chapa),dados pessoais, informações da CNH (número, classe e validade),se pode dirigir carro manual, automático ou ambos, períodos de férias/ausências e calcular automaticamente o status de disponibilidade do dia. 

#### Critérios de Aceitação
1. O cadastro deve conter os dados pessoais e só pode ser salvo se os campos obrigatórios (nome,identificação funcional (chapa), e-mail,CNH,categoria da CNH, validade da CNH, se pode dirigir carro manual / automático /ambos) estiverem preenchidos.  
2. A foto do motorista deve ser carregada a partir de um arquivo local, sendo exibida no perfil do motorista após o cadastro.  
3. Se a validade da CNH estiver a menos de 30 dias do vencimento, o sistema deve exibir um alerta visual.  
4. O status de disponibilidade do dia do motorista deve ser atualizado automaticamente com base em sua agenda de escalas e períodos de férias/ausências.

#### Critérios de Qualidade
* **Usabilidade:** A interface de cadastro deve ser intuitiva, com campos claros para cada informação.  
* **Segurança:** As informações da CNH devem ser armazenadas de forma segura, com acesso restrito a usuários autorizados.  
* **Performance:** O carregamento da página de cadastro e o salvamento das informações devem ser concluídos em no máximo 2 segundos.  
* **Rastreabilidade:** A origem deste requisito está na necessidade do cliente de gerenciar as informações dos motoristas e evitar problemas com CNHs vencidas.

#### Priorização
* **Must Have:** Essencial para o funcionamento inicial do sistema, pois é a base para a alocação de motoristas nas escalas.

#### Testabilidade
* O cadastro deve ser testado com dados válidos, dados incompletos e com uma data de CNH próxima ao vencimento para verificar a exibição do alerta. A funcionalidade de upload da foto deve ser testada com arquivos de diferentes formatos e tamanhos.  
    
##  Requisito Funcional: Cadastro de Veículos
> **RF-002: Cadastro de Veículos** O sistema deve permitir o cadastro de veículos com informações essenciais como placa, VIN (número do chassi), projeto, marca, modelo e o tipo de rota exigido pelo projeto.

#### Critérios de Aceitação
1. O cadastro só pode ser salvo se todos os campos obrigatórios (placa, VIN chassi, marca e modelo) estiverem preenchidos.
2. O sistema deve validar o VIN (composto por 17 caracteres (dígitos e letras maiúsculas) que funcionam como um identificador único para o veículo).
3. O sistema deve validar o formato da placa para garantir que siga o padrão Mercosul.
4. Após o cadastro, o veículo deve aparecer imediatamente na listagem geral de veículos.
5. O sistema deve permitir a seleção do **tipo de rota** para o veículo (City, Dritell, Highway), garantindo que ele seja alocado apenas em rotas compatíveis.
6. O sistema deve permitir a seleção do **projeto** para o veículo, garantindo que ele seja alocado apenas em projetos ativos.

#### Critérios de Qualidade
* **Usabilidade:** A interface de cadastro deve ser clara e direta, facilitando a inclusão de novos veículos.
* **Segurança:** As informações do veículo devem ser armazenadas de forma segura, com acesso controlado para evitar alterações não autorizadas.
* **Performance:** O tempo de salvamento do cadastro não deve exceder 2 segundos.
* **Rastreabilidade:** A origem deste requisito está na necessidade do cliente de gerenciar e categorizar sua frota, garantindo que os veículos sejam utilizados nas rotas corretas.

#### Priorização
* **Must Have:** Essencial para o funcionamento inicial, pois a frota de veículos é um dos principais ativos do sistema.

#### Testabilidade

* O cadastro deve ser testado com dados válidos e incompletos. A validação da placa deve ser verificada com formatos corretos e incorretos.A validação do VIN (composto por 17 caracteres (dígitos e letras maiúsculas). A funcionalidade deve ser validada para garantir que o veículo recém-cadastrado seja exibido na listagem, e que o tipo de rota selecionado seja corretamente associado.

## Requisito Funcional: Cadastro de Rotas

> **RF-003: Cadastro de Rotas** O sistema deve permitir o cadastro de rotas, incluindo nome, tipo (City, Dritell, Highway), distância (em quilômetros) e status (ativa/inativa).

#### Critérios de Aceitação
1. O cadastro só pode ser salvo se os campos **nome** e **distância** estiverem preenchidos.
2. O sistema deve permitir a seleção de um dos tipos de rota predefinidos (City, Dritell, Highway).
3. A distância deve ser um valor numérico e não pode ser negativa.
4. A medida deverá ser dada em quilômetros (Km).
5. Após o cadastro, a rota deve aparecer na lista de rotas disponíveis com o status padrão de **ativa**.
6. O sistema deve permitir que o status da rota seja alterado manualmente para **inativa** (e vice-versa), impedindo que ela seja alocada em novas escalas.

#### Critérios de Qualidade
* **Usabilidade:** A interface de cadastro deve ser simples e direta, facilitando o gerenciamento das rotas.
* **Consistência:** A lista de tipos de rota deve ser consistente com os tipos exigidos pelo cliente.
* **Performance:** O salvamento de uma nova rota não deve demorar mais de 2 segundos.
* **Rastreabilidade:** A origem deste requisito é a necessidade do cliente de categorizar e gerenciar as rotas de rodagem da frota.

#### Priorização
* **Must Have:** Essencial para o funcionamento inicial do sistema, pois o planejamento das escalas depende diretamente das rotas disponíveis.

#### Testabilidade
* O cadastro deve ser testado com dados válidos e com campos obrigatórios em branco. Deve-se verificar se a distância aceita apenas valores numéricos positivos. A funcionalidade de alteração de status deve ser testada para garantir que rotas inativas não possam ser usadas em escalas.

## Requisito Funcional: Geração de Escalas Inteligente
>**RF-004: Cadastro de Rotas** O sistema deve permitir a geração de escalas de motoristas, veículos e rotas em duas modalidades: **Manual** e **Automática** (Diária e Semanal). A funcionalidade automática deve seguir regras de negócio complexas.

#### Critérios de Aceitação

1. O sistema deve permitir a seleção manual de motorista, veículo e rota que estejam disponíveis no dia.  
2. Na geração automática, o sistema deve **priorizar** motoristas e veículos que não foram alocados nas mesmas rotas no dia anterior.  
3. A geração automática deve considerar somente motoristas e veículos com status "Disponível".  
4. O sistema deve validar a CNH do motorista e o status da rota antes de gerar a escala.  
5. Férias, ausências e o banco de férias devem ser respeitados, impedindo a alocação de motoristas nesses períodos.  

#### Critérios de Qualidade
* **Performance:** A geração de escala automática semanal deve ser concluída em um tempo aceitável para o usuário, idealmente em no máximo 10 segundos.  
* **Confiabilidade:** A lógica de alocação deve ser robusta, garantindo que todas as regras de negócio sejam aplicadas corretamente, evitando conflitos de escala.  
* **Usabilidade:** As interfaces para a geração manual e automática devem ser fáceis de usar e fornecer feedback claro sobre o processo e quaisquer erros encontrados.  
* **Rastreabilidade:** A origem deste requisito é a principal demanda do cliente, visando otimizar a operação, reduzir o trabalho manual e evitar erros no planejamento das escalas.

#### Priorização
* **Should Have:** Esta é a funcionalidade mais avançada do sistema e o maior diferencial. Embora seja de alto valor, o sistema ainda pode funcionar com a geração manual em uma primeira versão.

#### Testabilidade
* A funcionalidade manual deve ser testada para garantir que apenas motoristas e veículos disponíveis possam ser selecionados.  
* A lógica de geração automática deve ser testada com múltiplos cenários de dados:  
  * Cenário 1: Motorista com CNH vencida.  
  * Cenário 2: Motorista em férias.  
  * Cenário 3: Tentar alocar o mesmo motorista na mesma rota em dias consecutivos para verificar se a regra de evitação é aplicada.  
* Os filtros por turno e por período (diário/semanal) devem ser testados para garantir que funcionem conforme o esperado.

#### Requisito Funcional: Relatórios e Logs
>**RF-005: Relatórios e Logs** O sistema deve permitir a geração de relatórios de escala em formato PDF e Excel (XLSX) e manter um registro detalhado de logs de auditoria para todas as ações importantes.
 
#### Critérios de Aceitação
1. O sistema deve gerar relatórios de escala que podem ser filtrados por período (diário ou semanal) e por turno.  
2. Os relatórios gerados devem incluir todos os detalhes relevantes da escala, como dados do motorista, veículo, rota e turno.  
3. Os relatórios devem ser exportáveis para os formatos **PDF** e **XLSX**.  
4. O sistema deve registrar automaticamente e de forma permanente as seguintes ações: login, logout, cadastro, edição e exclusão de motoristas, veículos, rotas e escalas.  
5. Os logs de auditoria devem incluir o usuário responsável pela ação, o tipo de ação, a data e a hora da ocorrência.

#### Critérios de Qualidade
* **Performance:** A geração de um relatório semanal completo não deve demorar mais de 10 segundos.  
* **Segurança:** O acesso aos logs de auditoria deve ser restrito apenas a usuários com privilégios de administrador.  
* **Confiabilidade:** A informação nos relatórios deve ser precisa e consistente com os dados do sistema. Os logs devem ser inalteráveis para garantir a integridade da auditoria.  
* **Usabilidade:** A interface para geração de relatórios deve ser intuitiva, com opções de filtro claras para o usuário.  
* **Rastreabilidade:** A origem deste requisito é a necessidade do cliente por controle e auditoria, permitindo a análise de produtividade e a rastreabilidade das ações no sistema.

#### Priorização
* **Should Have:** Esta funcionalidade é fundamental para o controle e a análise da operação. Embora seja de alto valor para o cliente, o sistema pode ser utilizado sem ela na fase inicial, mas é essencial para o sucesso a longo prazo.

#### Testabilidade
* A geração de relatórios deve ser testada com diferentes filtros (período diário, semanal, por turno) para garantir que a saída corresponda aos dados esperados.  
* A exportação para PDF e XLSX deve ser validada para assegurar que os arquivos sejam gerados corretamente.  
* O sistema de logs deve ser testado simulando todas as ações importantes (login, logout, cadastro, etc.) para confirmar se os registros estão sendo criados de forma correta e completa.

## Requisito Não Funcional: Segurança de Acesso
>**RNF-001: Segurança de Acesso** O sistema deve implementar um **controle de acesso baseado em papéis**, exigindo login com credenciais válidas e restringindo as funcionalidades de acordo com o perfil do usuário logado

#### Perfis de Acesso e Permissões
* **Motorista - Consulta:** Acesso exclusivo para visualizar a sua própria escala. Não pode realizar cadastros, edições ou exclusões.
* **Líder- Gerência:** Pode cadastrar, editar e excluir (desde que nunca incluída a uma escala) os registros de motoristas, veículos, rotas e projetos. Pode visualizar todas as escalas.
* **Administrador do Sistema - Gerência Completa:** Possui todas as permissões do Líder, além de poder gerenciar acessos de outros usuários, concedendo permissões (por exemplo, tornar um usuário Líder).    

#### Critérios de Aceitação
1. O sistema deve ter uma tela de login que exija um email e uma senha para acesso.
2. As senhas dos usuários devem ser armazenadas de forma criptografada no banco de dados.
3. Após o login, a tela inicial deve exibir o nome ou email do usuário logado, junto com um botão de saída (logout).
4. As funcionalidades de cadastro, edição e exclusão devem ser exibidas ou ocultadas de acordo com o perfil do usuário.

#### Critérios de Qualidade
* **Segurança:** O sistema deve ser protegido contra vulnerabilidades de segurança (como injeção de SQL) para garantir que apenas usuários autorizados tenham acesso aos dados.
* **Integridade:** As permissões de cada perfil devem ser rígidamente aplicadas pelo sistema, sem a possibilidade de burlar as restrições.
* **Usabilidade:** A gestão de perfis e permissões deve ser simples e intuitiva para o Administrador do Sistema.

#### Priorização
* **Must Have:** Este requisito é fundamental e não negociável. Sem um controle de acesso robusto, a aplicação não pode ser considerada segura ou funcional para um ambiente real de negócios.

#### Testabilidade
* Teste o login com credenciais válidas e inválidas para cada perfil.
* Verifique se um usuário Motorista não consegue acessar as telas de cadastro, edição de dados e geração de escalas.
* Confirme se um usuário Líder **consegue** inserir um motorista, veículo, rota e projeto.
* Confirme se um usuário Líder **não consegue** excluir um motorista, veículo, rota e projeto que já foi incluído em uma escala (esteja ela finalizada ou não).
* Confirme se um usuário Líder **consegue** gerar uma escala manualmente.
* Valide se um Administrador pode acessar todas as funcionalidades e gerenciar as permissões de outros usuários.
* A funcionalidade de **logout** deve ser validada para garantir que, após o clique no botão de saída, o usuário não consiga retornar às páginas internas da aplicação usando o botão "voltar" do navegador.  
* Testes de segurança, como tentativas de injeção de SQL nos campos de login, devem ser realizados para garantir a robustez do sistema.

## Requisito Não Funcional: Interface Responsiva
>**RNF-002: Interface Responsiva** O sistema deve ser uma aplicação web com uma interface responsiva, garantindo que o layout se adapte corretamente a diferentes tamanhos de tela, como desktops e smartphones. A aplicação deve ser totalmente funcional nos navegadores Firefox e Edge.

#### Critérios de Aceitação
1. O layout da aplicação deve se ajustar de forma fluida a telas de smartphones e desktops sem cortar o conteúdo ou exigir a barra de rolagem horizontal.  
2. A interface deve manter a usabilidade em telas menores, com botões e textos de tamanho adequado para interação com o toque.  
3. A aplicação deve ser totalmente funcional e visualmente consistente nos navegadores **Mozilla Firefox** e **Microsoft Edge**, sem apresentar erros de renderização.  
4. O tempo de carregamento da página em dispositivos móveis não deve comprometer a experiência do usuário.

#### Critérios de Qualidade
* **Usabilidade:** A experiência do usuário deve ser intuitiva e consistente em todos os dispositivos e navegadores suportados.  
* **Compatibilidade:** O sistema deve ser desenvolvido utilizando tecnologias que garantam sua compatibilidade com os navegadores especificados, além de se adaptar a diferentes resoluções de tela.  
* **Performance:** O carregamento da página deve ser otimizado para dispositivos móveis, com foco na compressão de imagens e no carregamento eficiente de scripts.

#### Priorização
* **Should Have:** Este requisito é de alto valor para a usabilidade e conveniência do cliente, permitindo o acesso via dispositivos móveis. No entanto, o sistema pode ser funcional sem ele em um primeiro momento, sendo uma melhoria importante para versões futuras.

#### Testabilidade
* O layout e a funcionalidade devem ser testados em emuladores de diferentes dispositivos móveis e em navegadores reais.  
* A compatibilidade deve ser validada nos navegadores **Firefox** e **Edge** para garantir que todas as funcionalidades e elementos visuais funcionem perfeitamente.
 

## Tabela de Priorização

| ID | Requisito | Prioridade | Justificativa |
| :---- | :---- | :---- | :---- |
| RF-001 | Cadastro de Motoristas | Must Have | Essencial para o funcionamento inicial do sistema, pois é a base para a alocação de motoristas nas escalas. |
| RF-002 | Cadastro de Veículo | Must Have | Essencial para o funcionamento inicial, pois a frota de veículos é um dos principais ativos do sistema. |
| RF-003 | Cadastro de Rotas | Must Have | Essencial para o funcionamento inicial do sistema, pois o planejamento das escalas depende diretamente das rotas disponíveis. |
| RF-004 | Geração de Escalas Inteligente | Should Have | É a funcionalidade mais avançada e o maior diferencial, mas o sistema pode funcionar em uma primeira versão com a geração manual. |
| RF-005 | Relatórios e Logs | Should Have | Essencial para o controle e análise da operação a longo prazo, mas o sistema pode ser utilizado sem ela na fase inicial |
| RNF-001 | Segurança de Acesso | Must Have | Requisito fundamental e não negociável para garantir a segurança dos dados e o acesso restrito dos usuários |
| RN-002 | Interface Responsiva | Should Have | Importante para usabilidade e conveniência, mas o sistema pode ser funcional sem ele em um primeiro momento. |
