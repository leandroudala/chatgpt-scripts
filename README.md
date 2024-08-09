# Alterações em layout
O ChatGPT limita a largura máxima de seu chat, deixando faixas grandes aos lados quando a resolução do monitor é muito grande (por exemplo, os monitores ultrawide).

Para resolver isso, copie o comando abaixo e cole no DevTools* do navegador, na guia 'Console':
```JavaScript
// Este código perderá o efeito após o refresh da página
// deverá ser copiado e colado no console
(() => {
    const cssWidthLimitator = 'max-w'; // conteúdo das classe css que limita o tamanho da largura no chatgpt
    // realizar busca em todos os stylesheets
    for (let h = 0; h < document.styleSheets.length; h++) {
        const stylesheet = document.styleSheets[h];
        for (let i = 0; i < stylesheet.cssRules.length; i++) {
            // selecionar apenas rules do tipo `CSSMediaRule`
            const rule = stylesheet.cssRules[i];
            if (!(rule instanceof CSSMediaRule)) {
                continue;
            }
    
            for (let j = 0; j < rule.cssRules.length; j++) {
                const mediaRule = rule.cssRules[j];
                // seecionar apenas mediaRules do tipo `CSSStyleRule`
                if (!(mediaRule instanceof CSSStyleRule)) {
                    continue;
                }
                if (mediaRule.selectorText.indexOf(cssWidthLimitator) !== -1) {
                    mediaRule.style.maxWidth = '100%'; // agora max-width será 100%
                }
            }
        }
    }
})();
```

*DevTools - disponível ao apertar a tecla `F12`, é uma ferramenta que auxilia os desenvolvedores web a visualizar logs no frontend, requisições realizadas, etc.
