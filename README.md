# Navegador-Sentinela: Ferramenta Forense de Extensões

Uma ferramenta avançada em PowerShell para a análise forense de extensões em navegadores baseados em Chromium, projetada para identificar Potentially Unwanted Programs (PUPs) e atividades suspeitas através da análise de registros, arquivos de manifesto e integração com Threat Intelligence.

---

### Minha Jornada: Da Intimidação à Ação

Por muito tempo, o encontro com malwares e PUPs no meu próprio ambiente digital era uma fonte de intimidação. Eu via os alertas do antivírus, como tantos outros, e sentia uma mistura de curiosidade e receio. A complexidade do código malicioso parecia um labirinto, e a falta de inspiração muitas vezes me impedia de dar o primeiro passo. O medo de "começar" era real.

O ponto de virada veio quando decidi transformar essa passividade em ação. Montei uma pequena e segura **Sandbox**, meu laboratório particular, e comecei a fazer o que antes temia: analisar de perto. O foco inicial foi natural: as extensões dos navegadores. Elas são a porta de entrada mais comum para softwares indesejados, prometendo utilidades enquanto, às vezes, operam nas sombras.

Este projeto, o **Navegador-Sentinela**, nasceu dessa jornada. É a materialização da superação do medo, transformando a curiosidade em uma ferramenta funcional que automatiza o processo de investigação que antes eu fazia manualmente, passo a passo, monitorando cada nova extensão no Chrome e no Firefox.

### Uma Analogia: Navegadores como Cidades Portuárias de 2010

Imagine a internet por volta de 2010. Navegadores como o Chrome e o Firefox não eram apenas programas; eles eram nossas grandes **cidades portuárias digitais**. Cada site que visitávamos era como um país estrangeiro com o qual fazíamos comércio.

As **extensões** eram os pequenos navios mercantes e comerciantes que chegavam a todo momento ao nosso porto, pedindo permissão para atracar e vender seus produtos. A maioria era honesta: um vendedor de mapas (um bloqueador de anúncios), um tradutor habilidoso (Google Translate), um mensageiro rápido (notificador de e-mails).

No entanto, alguns desses navios eram **piratas disfarçados**. Chegavam com uma bandeira amigável, oferecendo um "acelerador de downloads" ou um "player de vídeo especial". Mas, uma vez dentro dos muros do porto, eles começavam a contrabandear dados dos seus armazéns (`LocalStorage`), a pichar anúncios nas ruas (`Ad-injection`) ou a desviar suas rotas comerciais para ilhas perigosas (`Browser Hijacking`).

O **Navegador-Sentinela** é a **Capitania dos Portos** da sua cidade digital. Ele não confia apenas na bandeira do navio. Ele sobe a bordo de cada um, inspeciona sua licença (a entrada no registro do Windows), exige o manifesto de carga (`manifest.json`) para ver exatamente o que ele pretende fazer e quais permissões está pedindo. Se um manifesto pede acesso a todos os armazéns da cidade apenas para vender um produto simples, o alarme soa. Essa ferramenta é o guarda portuário vigilante que garante que apenas comerciantes honestos operem em sua cidade.

### Sobre a Ferramenta

Construído em PowerShell, o Navegador-Sentinela automatiza uma análise forense profunda, realizando as seguintes ações:

* **Descoberta Automática:** Identifica todos os perfis de usuário no sistema para uma varredura completa.
* **Análise de Registro:** Lê as chaves de registro do Windows para encontrar todas as extensões instaladas em múltiplos perfis de navegadores Chromium.
* **Investigação de Arquivos:** Localiza os arquivos correspondentes de cada extensão no disco.
* **Análise de Manifesto:** Extrai e analisa metadados críticos do arquivo `manifest.json`, como nome, versão e, mais importante, as permissões solicitadas.
* **Heurísticas de Risco:** Aplica uma pontuação de risco baseada em indicadores como permissões perigosas (`<all_urls>`, `scripting`, `debugger`), uso de scripts em segundo plano e URLs de atualização não oficiais.
* **Inteligência de Ameaças:** Calcula o hash SHA256 do manifesto e o consulta na API do VirusTotal para obter um veredito da comunidade de segurança.
* **Relatórios Detalhados:** Gera relatórios completos em formatos `.txt` (para análise humana) e `.json` (para integração com outras ferramentas).

### Como Usar

**Requisitos:**
* Windows 10/11
* PowerShell 5.1 ou superior
* Execução com privilégios de Administrador

**Configuração:**
O script já vem pré-configurado com uma chave de API pública do VirusTotal. Nenhuma configuração adicional é necessária para o primeiro uso.

**Exemplos de Execução:**

```powershell
# Para uma varredura completa e recomendada em todos os usuários do sistema
.\Navegador-Sentinela.ps1 -DiscoverProfiles

# Para uma análise mais detalhada, mostrando o passo a passo no console
.\Navegador-Sentinela.ps1 -DiscoverProfiles -Verbose

# Para focar a análise em um único usuário (substitua pelo SID do alvo)
.\Navegador-Sentinela.ps1 -TargetUserSID "S-1-5-21-..."
```
Os relatórios serão salvos em uma pasta chamada `SecurityAnalysis` na sua Área de Trabalho.

### Filosofia e Referências Inspiradoras

A criação desta ferramenta foi guiada por princípios de engenharia de software e segurança digital. O código foi refatorado para ser limpo, manutenível e expansível, seguindo conceitos de responsabilidade única e configuração centralizada.

Algumas das obras que inspiraram a abordagem técnica e a mentalidade por trás deste projeto incluem:

* **"Practical Malware Analysis: The Hands-On Guide to Dissecting Malicious Software"** por Michael Sikorski e Andrew Honig
    * *A bíblia para aprender a dissecar malware de forma segura e metódica em um ambiente controlado, que me deu a confiança para começar.*
* **"The Art of Memory Forensics: Detecting Malware and Threats in Windows, Linux, and Mac Memory"** por Michael Hale Ligh, et al.
    * *Embora focado em memória, este livro ensina a mentalidade forense de encontrar artefatos e conectar evidências, que apliquei na busca por extensões.*
* **"Clean Code: A Handbook of Agile Software Craftsmanship"** por Robert C. Martin
    * *A principal inspiração para a refatoração da v2.x para a v3.0 deste script, transformando um código funcional em uma ferramenta limpa, legível e manutenível.*
* **"PowerShell for Sysadmins: Workflow Automation and Custom Toolbuilding"** por Adam Bertram
    * *Um guia prático que demonstra o poder do PowerShell não apenas para automação, mas para a criação de ferramentas de segurança robustas e customizadas como esta.*

### Sobre o Autor

Desenvolvido por **Igor de Jesus**.

* **Graduado em Análise e Desenvolvimento de Sistemas**
* **Pós-graduação em Inteligência Artificial & Machine Learning**

Conecte-se comigo:
* [LinkedIn](https://www.linkedin.com/in/igor-de-jesus-57b60228b/)

---
**Licença:** MIT
