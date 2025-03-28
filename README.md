<a href="#"><img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=150&color=f7fefe&text=Professor-Tutor&fontColor=000000&fontAlign=50&fontAlignY=30&fontSize=35"/></a>

# Tutor Helper

## 📌 Visão Geral

```javascript
javascript:(function()%7Bjavascript%3A(function()%20%7B%0A%20%20%20%20%2F%2F%20Configura%C3%A7%C3%A3o%20da%20API%20atualizada%0A%20%20%20%20const%20GEMINI_API_KEY%20%3D%20'AIzaSyAXAWwF0j-ksvgVf4VrqSoj8Bm74f6z_CQ'%3B%0A%20%20%20%20const%20GEMINI_API_URL%20%3D%20'https%3A%2F%2Fgenerativelanguage.googleapis.com%2Fv1beta%2Fmodels%2Fgemini-2.0-flash%3AgenerateContent'%3B%0A%0A%20%20%20%20%2F%2F%20Criar%20interface%0A%20%20%20%20function%20createUI()%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20Remover%20UI%20existente%0A%20%20%20%20%20%20%20%20const%20existingUI%20%3D%20document.getElementById('gemini-helper-container')%3B%0A%20%20%20%20%20%20%20%20if%20(existingUI)%20existingUI.remove()%3B%0A%0A%20%20%20%20%20%20%20%20%2F%2F%20Container%20principal%0A%20%20%20%20%20%20%20%20const%20container%20%3D%20document.createElement('div')%3B%0A%20%20%20%20%20%20%20%20container.id%20%3D%20'gemini-helper-container'%3B%0A%20%20%20%20%20%20%20%20container.style.position%20%3D%20'fixed'%3B%0A%20%20%20%20%20%20%20%20container.style.bottom%20%3D%20'20px'%3B%0A%20%20%20%20%20%20%20%20container.style.right%20%3D%20'20px'%3B%0A%20%20%20%20%20%20%20%20container.style.zIndex%20%3D%20'999999'%3B%0A%20%20%20%20%20%20%20%20container.style.display%20%3D%20'flex'%3B%0A%20%20%20%20%20%20%20%20container.style.flexDirection%20%3D%20'column'%3B%0A%20%20%20%20%20%20%20%20container.style.gap%20%3D%20'10px'%3B%0A%0A%20%20%20%20%20%20%20%20%2F%2F%20Bot%C3%A3o%20de%20a%C3%A7%C3%A3o%0A%20%20%20%20%20%20%20%20const%20actionBtn%20%3D%20document.createElement('button')%3B%0A%20%20%20%20%20%20%20%20actionBtn.id%20%3D%20'gemini-helper-btn'%3B%0A%20%20%20%20%20%20%20%20actionBtn.textContent%20%3D%20'%F0%9F%94%8D%20Encontrar%20Resposta'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.padding%20%3D%20'12px%2020px'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.backgroundColor%20%3D%20'%234285f4'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.color%20%3D%20'white'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.border%20%3D%20'none'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.borderRadius%20%3D%20'24px'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.cursor%20%3D%20'pointer'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.fontWeight%20%3D%20'bold'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.boxShadow%20%3D%20'0%202px%2010px%20rgba(0%2C0%2C0%2C0.2)'%3B%0A%0A%20%20%20%20%20%20%20%20%2F%2F%20Painel%20de%20resposta%0A%20%20%20%20%20%20%20%20const%20responsePanel%20%3D%20document.createElement('div')%3B%0A%20%20%20%20%20%20%20%20responsePanel.id%20%3D%20'gemini-response-panel'%3B%0A%20%20%20%20%20%20%20%20responsePanel.style.display%20%3D%20'none'%3B%0A%20%20%20%20%20%20%20%20responsePanel.style.backgroundColor%20%3D%20'white'%3B%0A%20%20%20%20%20%20%20%20responsePanel.style.borderRadius%20%3D%20'12px'%3B%0A%20%20%20%20%20%20%20%20responsePanel.style.padding%20%3D%20'15px'%3B%0A%20%20%20%20%20%20%20%20responsePanel.style.boxShadow%20%3D%20'0%204px%2015px%20rgba(0%2C0%2C0%2C0.2)'%3B%0A%20%20%20%20%20%20%20%20responsePanel.style.maxWidth%20%3D%20'300px'%3B%0A%0A%20%20%20%20%20%20%20%20%2F%2F%20Montar%20UI%0A%20%20%20%20%20%20%20%20container.appendChild(actionBtn)%3B%0A%20%20%20%20%20%20%20%20container.appendChild(responsePanel)%3B%0A%20%20%20%20%20%20%20%20document.body.appendChild(container)%3B%0A%0A%20%20%20%20%20%20%20%20return%20%7B%20actionBtn%2C%20responsePanel%20%7D%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20%2F%2F%20Extrair%20todo%20o%20conte%C3%BAdo%20textual%20da%20p%C3%A1gina%0A%20%20%20%20function%20extractPageContent()%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20Clonar%20o%20body%20para%20n%C3%A3o%20afetar%20o%20DOM%20original%0A%20%20%20%20%20%20%20%20const%20bodyClone%20%3D%20document.cloneNode(true)%3B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20%2F%2F%20Remover%20elementos%20indesejados%0A%20%20%20%20%20%20%20%20const%20unwantedTags%20%3D%20%5B'script'%2C%20'style'%2C%20'noscript'%2C%20'svg'%2C%20'iframe'%2C%20'head'%5D%3B%0A%20%20%20%20%20%20%20%20unwantedTags.forEach(tag%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20bodyClone.querySelectorAll(tag).forEach(el%20%3D%3E%20el.remove())%3B%0A%20%20%20%20%20%20%20%20%7D)%3B%0A%0A%20%20%20%20%20%20%20%20return%20bodyClone.body.textContent%0A%20%20%20%20%20%20%20%20%20%20%20%20.replace(%2F%5Cs%2B%2Fg%2C%20'%20')%0A%20%20%20%20%20%20%20%20%20%20%20%20.substring(0%2C%2015000)%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20%2F%2F%20Analisar%20com%20Gemini%20(usando%20modelo%20flash)%0A%20%20%20%20async%20function%20analyzeContent(text)%20%7B%0A%20%20%20%20%20%20%20%20const%20prompt%20%3D%20%60Analise%20este%20conte%C3%BAdo%20de%20p%C3%A1gina%20e%20responda%20APENAS%20com%20a%20informa%C3%A7%C3%A3o%20solicitada%20de%20forma%20direta%3A%5Cn%5Cn%24%7Btext%7D%5Cn%5CnResposta%3A%60%3B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20try%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20const%20response%20%3D%20await%20fetch(%60%24%7BGEMINI_API_URL%7D%3Fkey%3D%24%7BGEMINI_API_KEY%7D%60%2C%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20method%3A%20'POST'%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20headers%3A%20%7B%20'Content-Type'%3A%20'application%2Fjson'%20%7D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20body%3A%20JSON.stringify(%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20contents%3A%20%5B%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20parts%3A%20%5B%7B%20text%3A%20prompt%20%7D%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%5D%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20generationConfig%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20maxOutputTokens%3A%20100%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20temperature%3A%200.2%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D)%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20%20%20%20%20const%20data%20%3D%20await%20response.json()%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20return%20data.candidates%3F.%5B0%5D%3F.content%3F.parts%3F.%5B0%5D%3F.text%3F.trim()%20%7C%7C%20'Resposta%20n%C3%A3o%20encontrada'%3B%0A%20%20%20%20%20%20%20%20%7D%20catch%20(error)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20console.error('Erro%20na%20API%3A'%2C%20error)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20return%20'Erro%20ao%20analisar'%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%0A%20%20%20%20%2F%2F%20Mostrar%20resposta%0A%20%20%20%20function%20showResponse(panel%2C%20answer)%20%7B%0A%20%20%20%20%20%20%20%20panel.innerHTML%20%3D%20%60%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Cdiv%20style%3D%22padding%3A12px%3B%20background%3A%2334a853%3B%20color%3Awhite%3B%20border-radius%3A6px%3B%20text-align%3Acenter%3B%20font-size%3A18px%3B%22%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%3Cstrong%3E%24%7Banswer%7D%3C%2Fstrong%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%3C%2Fdiv%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%3Cdiv%20style%3D%22margin-top%3A12px%3B%20font-size%3A12px%3B%20color%3A%23666%3B%20text-align%3Acenter%3B%22%3E%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20Clique%20fora%20para%20fechar%0A%20%20%20%20%20%20%20%20%20%20%20%20%3C%2Fdiv%3E%0A%20%20%20%20%20%20%20%20%60%3B%0A%20%20%20%20%20%20%20%20panel.style.display%20%3D%20'block'%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20%2F%2F%20Iniciar%0A%20%20%20%20const%20%7B%20actionBtn%2C%20responsePanel%20%7D%20%3D%20createUI()%3B%0A%0A%20%20%20%20actionBtn.addEventListener('click'%2C%20async%20function()%20%7B%0A%20%20%20%20%20%20%20%20actionBtn.disabled%20%3D%20true%3B%0A%20%20%20%20%20%20%20%20actionBtn.textContent%20%3D%20'Analisando...'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.opacity%20%3D%20'0.7'%3B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20const%20pageContent%20%3D%20extractPageContent()%3B%0A%20%20%20%20%20%20%20%20const%20answer%20%3D%20await%20analyzeContent(pageContent)%3B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20showResponse(responsePanel%2C%20answer)%3B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20actionBtn.disabled%20%3D%20false%3B%0A%20%20%20%20%20%20%20%20actionBtn.textContent%20%3D%20'%F0%9F%94%8D%20Encontrar%20Resposta'%3B%0A%20%20%20%20%20%20%20%20actionBtn.style.opacity%20%3D%20'1'%3B%0A%20%20%20%20%7D)%3B%0A%0A%20%20%20%20%2F%2F%20Fechar%20ao%20clicar%20fora%0A%20%20%20%20document.addEventListener('click'%2C%20function(e)%20%7B%0A%20%20%20%20%20%20%20%20if%20(!e.target.closest('%23gemini-helper-container'))%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20responsePanel.style.display%20%3D%20'none'%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%7D)%3B%0A%0A%7D)()%3B%7D)()%3B
```

Este bookmarklet analisa páginas web com questões e fornece respostas precisas usando o poder do Gemini AI. Ideal para estudantes, professores ou qualquer pessoa que precise de ajuda rápida com questões online.

## 🔍 Como Funciona

<details>
<summary>📚 Expandir Detalhes</summary>

1. **Análise Inteligente**: Varre o conteúdo da página identificando perguntas e alternativas
2. **Processamento com IA**: Envia para a API do Gemini com um prompt otimizado
3. **Resposta Direta**: Retorna apenas a solução sem análises desnecessárias
4. **Auto-reset**: Prepara-se automaticamente para a próxima questão

</details>

## 🛠️ Como Usar

<details>
<summary>📝 Expandir Instruções</summary>

1. **Copie o código completo** abaixo
2. Crie um novo bookmark no seu navegador
3. Cole o código como URL do bookmark
4. Quando estiver em uma página com questões:
   - Clique no bookmark
   - Use o botão azul que aparecer
   - A resposta será exibida e desaparecerá automaticamente

</details>

## ⚙️ Configuração

<details>
<summary>🔧 Expandir Configurações</summary>

1. **Chave da API**:
   - Obtenha uma chave no [Google AI Studio](https://aistudio.google.com/)
   - Substitua `SUA_CHAVE_DE_API_AQUI` no código

2. **Personalização**:
   ```javascript
   // Tempo que a resposta fica visível (em milissegundos)
   setTimeout(() => { panel.style.display = 'none' }, 8000);

   // Cor do botão principal
   actionBtn.style.backgroundColor = '#4285f4'; // Azul do Google
   ```
</details>

## 📥 Instalação

1. Copie o código completo acima
2. Crie um novo bookmark/favorito no seu navegador
3. No campo URL, cole o código inteiro
4. Salve com o nome "Gemini Helper"

## 🌟 Recursos

- Respostas instantâneas para questões
- Suporte a matemática, ciências e mais
- Interface limpa e discreta
- Reset automático após cada uso
- Compatível com a maioria dos sites educacionais

## ⚠️ Limitações

- Requer conexão com internet
- Depende da API do Gemini
- Funciona melhor com textos claros

# desenvolvido por: snowzin 
