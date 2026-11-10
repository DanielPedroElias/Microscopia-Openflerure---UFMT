🔬 Microscopia Acessível com OpenFlexure: Democratização da Ciência no Araguaia

Projeto de Extensão e Inovação Tecnológica (Bolsa ET 2025 – FAPEMAT / UFMT Campus Araguaia)

Processo FAPEMAT: PRO.0002166/2025 | Termo de Outorga: Cooperação nº 0140/2025

Coordenador/Bolsista: Daniel Pedro Elias dos Santos

Orientador: Prof. Robson da Silva Lopes

📌 Sobre o Projeto

Este projeto tem como objetivo democratizar o acesso à microscopia científica em escolas públicas da região do Araguaia (Mato Grosso), utilizando hardware livre impresso em 3D. A iniciativa desenvolve e adapta o OpenFlexure Microscope para duas abordagens principais:

Versão Manual com Webcam (Logitech): Voltada para uso didático em salas de aula, priorizando facilidade de manutenção e sensor de simples limpeza.

Versão Computacional (Raspberry Pi v2): Voltada para automação, captura de imagens em alta resolução e processamento digital (visão computacional / mosaicos de imagens).

🛠️ Montagem & Configuração da Impressora 3DCloner DH

Para a fabricação das peças do OpenFlexure (v7.0.0-beta5), utilizou-se a impressora 3DCloner DH do laboratório.

Softwares Originais da 3DCloner

Caso necessite dos softwares proprietários da impressora (fatiador original e leitor/enviador de G-code responsável por gerenciar a impressão):

💾 Download do Setup 3DCloner: SetupClonerGen3D_V1.01.rar

⚙️ Configurações Recomendadas no PrusaSlicer

Embora o fatiador original da 3DCloner seja suficiente para peças estruturais simples, ele se provou insuficiente para a precisão exigida pelo corpo principal (main body) do microscópio. Para garantir o alinhamento das engrenagens e a flexibilidade das pontes móveis, é obrigatório utilizar o PrusaSlicer com os seguintes parâmetros:

1. Aba Camadas e Perímetros (Layers and Perimeters)

Altura da Camada (Layer height): 0.2 mm

Altura da Primeira Camada (First layer height): 0.2 mm ou 0.25 mm (para melhor adesão à mesa)

Perímetros / Paredes (Perimeters): Mínimo de 3 percursos (garante a resistência mecânica das alavancas flexíveis)

Camadas Sólidas (Solid layers): 4 no topo (Top) e 4 na base (Bottom)

2. Preenchimento (Infill)

Densidade (Fill density): 20% a 30%

Padrão de Preenchimento (Fill pattern): Giroide (Gyroid) ou Grade (Grid) — o padrão Giroide distribui melhor o estresse mecânico no movimento das alavancas.

3. Velocidade (Speed)

Perímetros (Perimeters): 30 - 40 mm/s (reduza a velocidade para garantir precisão dimensional nas engrenagens)

Perímetros Externos (Small/External perimeters): 20 - 25 mm/s

Preenchimento (Infill): 45 - 50 mm/s

Primeira Camada (First layer speed): 15 - 20 mm/s

4. Filamento (Filament Settings)

Temperatura do Bico (Nozzle Temperature):

Observação importante: Para filamentos de cores mais claras (como o branco), a temperatura de extrusão deve ser mais alta (ex: 205°C - 215°C para PLA) para garantir uma fusão perfeita entre as camadas e evitar delaminação durante a movimentação mecânica.

Temperatura da Mesa (Bed Temperature): 60°C (com aplicação de adesivo/spray de fixação).

🪛 Soluções de Problemas & Gambiarras Técnicas (Troubleshooting)

1. Substituição dos Anéis de Vedação (O-Rings) dos Atuadores

Problema: A documentação oficial do OpenFlexure exige anéis de vedação de Viton para exercer a força de retorno elástico nos atuadores do microscópio. Os anéis comuns de borracha sintética comprados no comércio local arrebentaram repetidamente durante os testes de estresse.

Solução Técnica Adoptada: Os anéis de borracha foram substituídos pela base de borracha roletada de preservativos (camisinhas). O material apresentou a flexibilidade, o diâmetro e a resistência elástica perfeitos para o mecanismo, restaurando com sucesso o movimento dos eixos sem romper.

2. Vedação do Módulo Óptico contra Poeira e Mofo

Problema: O acúmulo de poeira e umidade local danificou o sensor exposto da câmera Raspberry Pi v2.

Medida Mitigatória: Utilização de tampas de proteção e vedação com fita de silicone nas junções das lentes logo após a montagem. Para a versão manual, priorizou-se a webcam Logitech, pois possui um sensor plano de fácil acesso e limpeza rápida em comparação com a Pi Camera.

💻 Processamento de Imagens: Instalação e Uso do openflexure-stitch

O openflexure-stitch é o programa em linha de comando usado para juntar a grade de fotos tiradas pelo microscópio e formar uma imagem panorâmica de alta resolução (stitching / mosaico 2D).

🚀 Como Baixar e Instalar

Certifique-se de ter o Python 3.8+ instalado em seu sistema.

Abra o terminal (Prompt de Comando ou PowerShell) e execute o comando via pip:

pip install openflexure-stitch


Para verificar se a instalação foi concluída corretamente, digite:

openflexure-stitch --help


📜 Guia Rápido de Comandos

Nota: Substitua "C:\Caminho\Para\Sua\Pasta" pelo diretório local onde estão salvas as fotos da sua varredura (Stack and Scan).

1. Stitching Padrão

openflexure-stitch "C:\Users\Aluno\Desktop\SCAN_TESTE"


2. Redução de Exigência de Sobreposição (--minimum_overlap)

Se o programa falhar ao tentar alinhar as imagens, ajuste o overlap mínimo:

# Overlap 5% (Recomendado para varreduras com poucos pontos de referência)
openflexure-stitch --minimum_overlap 0.05 "C:\Users\Aluno\Desktop\SCAN_TESTE"

# Overlap 10%
openflexure-stitch --minimum_overlap 0.10 "C:\Users\Aluno\Desktop\SCAN_TESTE"


3. Redução do Uso de Memória RAM (--no-pad)

Utilize este parâmetro se o seu computador der erro de memória insuficiente:

openflexure-stitch --no-pad "C:\Users\Aluno\Desktop\SCAN_TESTE"


4. Reduzir Resolução na Fase de Correlação (--resize)

Acelera o processamento de varreduras grandes:

openflexure-stitch --resize 0.5 "C:\Users\Aluno\Desktop\SCAN_TESTE"


5. Combinação para Scans Grandes (ex: Grade 7x7 travada / "Disconnected")

openflexure-stitch --no-pad --resize 0.5 --minimum_overlap 0.05 "C:\Users\Aluno\Desktop\SCAN_2026-09-22_21-14-47"


6. Especificar Pasta de Saída do Mosaico (-o)

openflexure-stitch --minimum_overlap 0.05 -o "C:\Users\Aluno\Desktop\RESULTADO_FINAL" "C:\Users\Aluno\Desktop\SCAN_TESTE"


🎨 Ações de Extensão & Impacto Comunitário

O projeto extrapolou o ambiente de laboratório e promoveu a divulgação científica em múltiplos eventos:

Mostra de Extensão da UFMT (20/08/2026): Exposição do banner institucional do projeto para a comunidade acadêmica.

Mostra de Cursos da UFMT (21/08/2026): Apresentação prática do protótipo funcional para alunos do ensino médio, demonstrando a aplicação da Ciência da Computação em hardware aberto e física/biologia.

Parceria Interdisciplinar (Agronomia): Início do diálogo com docentes do curso de Agronomia para automação da captura de imagens de fitonematoides via visão computacional.

Feira de Ciências da Escola COOPEMA: Exposição e oficina prática com estudantes do ensino básico, permitindo a observação direta de lâminas biológicas no microscópio montado.

🔗 Links Úteis & Referências

Download Softwares 3DCloner Gen3D v1.01

Documentação Oficial do OpenFlexure (v7.0.0-beta5)

Repositório Oficial do OpenFlexure Stitching (GitLab)