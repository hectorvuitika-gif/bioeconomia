const fs = require('fs');
const path = require('path');

// Fontes fornecidas pelo usuário
const FONTES = [
    "https://www.gov.br/mdic/pt-br/assuntos/noticias/2026/marco/governo-lanca-plano-de-desenvolvimento-da-bioeconomia-para-fortalecer-industria-verde",
    "https://pesquisa.in.gov.br/imprensa/jsp/visualiza/index.jsp?data=01/04/2026&jornal=515&pagina=131&totalArquivos=222"
];

// Mock de dados simulando a extração das fontes (PNDBio - Indústria Verde)
const dadosExtraidos = {        "Criação de Departamentos focados: Patrimônio Genético (DEAMA), Descarbonização (DCARB) e Novas Economias (DNOVA).",

    titulo: "Plano Nacional de Desenvolvimento da Bioeconomia (PNDBio)",
    dataLancamento: "01/04/2026",
    orgao: "Ministério do Desenvolvimento, Indústria, Comércio e Serviços (MDIC)",
    pilares: [
        "Fortalecimento da Indústria Verde e inserção do Brasil em cadeias globais.",
        "Criação de Departamentos focados: Patrimônio Genético (DEAMA), Descarbonização (DCARB) e Novas Economias (DNOVA).",
        "Foco estratégico na sustentabilidade do bioma da Amazônia e valorização da biodiversidade."
    ]
};

// Função para garantir que os diretórios existam no repositório do GitHub
function inicializarPastas() {
    const pastas = [
        path.join(__dirname, 'conteudo-bioeconomia', 'posts'),
        path.join(__dirname, 'conteudo-bioeconomia', 'imagens'),
        path.join(__dirname, 'conteudo-bioeconomia', 'resumo')
    ];

    pastas.forEach(pasta => {
        if (!fs.existsSync(pasta)) {
            fs.mkdirSync(pasta, { recursive: true });
            console.log(`Pasta criada com sucesso: ${pasta}`);
        }
    });
}

// Geração de textos para Redes Sociais e Resumos
function gerarTextos() {
    // 1. Post focado no LinkedIn (Profissional)
    const postLinkedin = `🚀 BRASIL RUMO À INDÚSTRIA VERDE: Governo lança o PNDBio!

O Ministério do Desenvolvimento, Indústria, Comércio e Serviços (MDIC) oficializou o Plano Nacional de Desenvolvimento da Bioeconomia. O grande objetivo é impulsionar a nossa economia utilizando de forma sustentável a rica biodiversidade dos nossos biomas, com destaque para a Amazônia.

Principais frentes de atuação:
🌱 Criação do Departamento de Descarbonização e Finanças Verdes (DCARB)
🧬 Foco em Patrimônio Genético e Cadeias Produtivas (DEAMA)
📈 Inserção competitiva do Brasil nas cadeias globais de valor

A transição ecológica não é apenas uma meta de futuro, ela está acontecendo agora em 2026 através de políticas estruturadas.

#Bioeconomia #IndustriaVerde #Sustentabilidade #MDIC #TransicaoEcologica #ESG`;

    // 2. Post dinâmico para Instagram / X (Twitter)
    const postRedesVisuais = `🚨 NOVIDADE: O Plano Nacional de Desenvolvimento da Bioeconomia (PNDBio) foi lançado oficialmente! 🇧🇷🌱

O plano estratégico do MDIC quer colocar o Brasil na liderança global da indústria verde. O foco está na descarbonização, na proteção dos biomas (como a Amazônia) e na criação de novas economias sustentáveis. 

Arraste para o lado para entender os novos departamentos criados e o que muda na prática! ➡️

#Sustentabilidade #Amazônia #EconomiaVerde #Brasil2026`;

    // 3. Resumo de notícias estruturado em Markdown
    const resumoNoticia = `# Resumo Executivo: Lançamento do PNDBio 2026
**Data de Publicação Original:** 01/04/2026
**Fonte Primária:** MDIC & Diário Oficial da União (Edição 515, Pág. 131)

## Contexto
O Governo Federal lançou o **Plano Nacional de Desenvolvimento da Bioeconomia (PNDBio)**. O projeto visa expandir a capacidade bioindustrial brasileira através de ativos biológicos e tecnológicos nativos.

## Estrutura Administrativa e Focos Declarados
Para garantir a execução do plano, novos departamentos estratégicos foram desenhados:
* **DEAMA:** Departamento de Patrimônio Genético e Cadeias Produtivas dos Biomas e Amazônia.
* **DCARB:** Departamento de Descarbonização e Finanças Verdes.
* **DNOVA:** Departamento de Novas Economias.

## Fontes Analisadas
* Notícia MDIC: ${FONTES[0]}
* Publicação DOU: ${FONTES[1]}
`;

    return { postLinkedin, postRedesVisuais, resumoNoticia };
}

// Geração de briefings ou manipulação/metadados das Imagens
// Nota: Em repositórios de automação, imagens automatizadas costumam ser criadas por canvas (ex: node-canvas) 
// ou enviando o briefing de imagem (texto descritivo) para ferramentas como DALL-E/Midjourney.
function gerarPromptsImagens() {
    const imagemLinkedin = {
        tipo: "Card Corporativo / Infográfico",
        dimensoes: "1200x628 (Recomendado LinkedIn)",
        elementos_visuais: "Fundo clean em tons de verde musgo desaturado e cinza claro corporativo. Gráfico vetorizado simbolizando folha estilizada fundida com engrenagem industrial.",
        texto_da_imagem: "PNDBio: O Plano do Brasil para a Indústria Verde"
    };

    const imagemInstagram = {
        tipo: "Carrossel Informativo",
        dimensoes: "1080x1350 (Vertical)",
        slide_1: "Título forte: O que é o PNDBio? (Imagem da Amazônia ao fundo com opacidade reduzida)",
        slide_2: "Tópicos dos novos departamentos: DEAMA, DCARB e DNOVA.",
        slide_3: "CTA: Salve este post para consultar depois."
    };

    return {
        briefingLinkedin: JSON.stringify(imagemLinkedin, null, 2),
        briefingInstagram: JSON.stringify(imagemInstagram, null, 2)
    };
}

// Salva tudo de forma organizada na árvore de arquivos do repositório
function salvarNoRepositorio() {
    inicializarPastas();
    
    const textos = gerarTextos();
    const imagens = gerarPromptsImagens();

    const caminhos = {
        linkedinTxt: path.join(__dirname, 'conteudo-bioeconomia', 'posts', 'post_linkedin.txt'),
        instagramTxt: path.join(__dirname, 'conteudo-bioeconomia', 'posts', 'post_redes_visuais.txt'),
        resumoMd: path.join(__dirname, 'conteudo-bioeconomia', 'resumo', 'resumo_noticia.md'),
        imgLinkedinTxt: path.join(__dirname, 'conteudo-bioeconomia', 'imagens', 'briefing_imagem_linkedin.txt'),
        imgInstagramTxt: path.join(__dirname, 'conteudo-bioeconomia', 'imagens', 'briefing_imagem_instagram.txt')
    };

    // Escrevendo os arquivos de texto e markdown
    fs.writeFileSync(caminhos.linkedinTxt, textos.postLinkedin, 'utf-8');
    fs.writeFileSync(caminhos.instagramTxt, textos.postRedesVisuais, 'utf-8');
    fs.writeFileSync(caminhos.resumoMd, textos.resumoNoticia, 'utf-8');

    // Escrevendo as especificações estruturadas de imagem
    fs.writeFileSync(caminhos.imgLinkedinTxt, imagens.briefingLinkedin, 'utf-8');
    fs.writeFileSync(caminhos.imgInstagramTxt, imagens.briefingInstagram, 'utf-8');

    console.log("=========================================================");
    console.log("🎉 TODOS OS ARQUIVOS FORAM CRIADOS E SALVOS NA PASTA!");
    console.log("Pronto para o commit e push automáticos no GitHub.");
    console.log("=========================================================");
}

// Executa o script
salvarNoRepositorio();
