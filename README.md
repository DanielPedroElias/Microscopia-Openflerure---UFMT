# 🔬 Microscopia Acessível com OpenFlexure: Democratização da Ciência no Araguaia

> **Projeto de Extensão e Inovação Tecnológica (Bolsa ET 2025 – FAPEMAT / UFMT Campus Araguaia)**  
> **Processo FAPEMAT:** PRO.0002166/2025 | **Termo de Outorga:** Cooperação nº 0140/2025  
> **Coordenador/Bolsista:** Daniel Pedro Elias dos Santos  
> **Orientador:** Prof. Robson da Silva Lopes  

---

## 📌 Sobre o Projeto

Este projeto tem como objetivo democratizar o acesso à microscopia científica em escolas públicas da região do Araguaia (Mato Grosso), utilizando hardware livre impresso em 3D. A iniciativa desenvolve e adapta o **OpenFlexure Microscope** para duas abordagens principais:
1. **Versão Manual com Webcam (Logitech):** Voltada para uso didático em salas de aula, priorizando facilidade de manutenção e sensor de simples limpeza.
2. **Versão Computacional (Raspberry Pi v2):** Voltada para automação, captura de imagens em alta resolução e processamento digital (digital pathology / stitching).

---

## 🛠️ Montagem & Preparação da Impressora 3D

Para a fabricação das peças do OpenFlexure v7.0.0-beta5, utilizou-se a impressora **3DCloner DH** presente no laboratório. 

⚠️ **Atenção:** O fatiador original da 3DCloner DH provou-se insuficiente para a precisão exigida pelo corpo principal (`main body`) do OpenFlexure. Recomenda-se o uso do **PrusaSlicer** com as seguintes adaptações:

* **Fatiador recomendado:** PrusaSlicer.
* **Peças de alta precisão (`main body`, atuadores):** Utilizar configurações rigorosas de altura de camada e suporte conforme a documentação oficial.
* **Peças estruturais simples:** Podem utilizar perfis padrão.
* **Ajuste por filamento:** Em filamentos de cores mais claras (como o branco), aumente ligeiramente a temperatura de extrusão em relação ao padrão para garantir fusão de camadas e rigidez mecânica.

---

## 🪛 Solução de Problemas Técnicos (Troubleshooting)

### 1. Vedação do Módulo Óptico contra Poeira e Mofo
* **Problema:** A poeira local e a umidade causaram contaminação nos sensores ópticos. No sensor da Raspberry Pi Camera v2, o mofo/sujeira acumulado internamente inutilizou o módulo. Na webcam Logitech, embora a limpeza seja viável devido ao sensor plano, a entrada de poeira permaneceu frequente.
* **Medida Mitigatória:** Recomenda-se vedar completamente o módulo óptico durante o armazenamento e utilizar capas de proteção contra poeira logo após as oficinas. No caso do sensor exposto da Pi Camera, a desmontagem só deve ser feita em ambiente limpo e vedado.

### 2. Anéis de Vedação dos Atuadores Mecânicos
* **Problema:** A documentação padrão especifica o uso de anéis de vedação de *Viton* para a força elástica dos atuadores. Os anéis comuns de borracha sintética localmente encontrados arrebentaram sob tensão contínua.
* **Status:** Testes contínuos estão sendo realizados com materiais alternativos (ex: elastômeros de silicone ou molas impressas/metálicas adaptadas).

---

## 💻 Processamento de Imagens: Stitching (Mosaico 2D)

Para varreduras de lâminas completas (*Stack and Scan* / mosaicos de grande área), utilizamos a ferramenta em linha de comando `openflexure-stitch`.

### Pré-requisitos
Verifique se o utilitário está instalado no seu terminal:
```bash
where openflexure-stitch
openflexure-stitch --help