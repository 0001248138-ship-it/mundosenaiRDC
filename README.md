# Cisco Network Lab 3D — Edição VR (v3.0)

Adaptação da experiência HTML/WebGL da topologia Cisco para **óculos de realidade virtual compatíveis com WebXR** e para **visores de celular do tipo Cardboard**.

## Primeiro: qual é o tipo de óculos?

| Equipamento | Modo indicado | Requisitos |
|---|---|---|
| Meta Quest / headset VR com navegador WebXR | **Entrar no VR imersivo** | Site aberto por **HTTPS**, browser com WebXR, controles ou seleção pelo olhar |
| Google Cardboard / visor onde se encaixa um smartphone | **3D lado a lado** | Smartphone com navegador, preferencialmente paisagem, giroscópio opcional |
| Óculos 3D passivo de cinema / TV | **Não é diretamente compatível** | Exige TV/projetor que aceite o formato estereoscópico específico; verifique o modelo |
| Notebook ou PC | **Modo normal 3D** | Navegador recente; WebGL recomendado. Existe desenho 2D alternativo se WebGL não estiver disponível |

## Como apresentar em um headset WebXR

1. Publique o conteúdo da pasta `Preview/` em um endereço **HTTPS**. O arquivo `Cisco_Network_VR_Standalone.html` também pode ser publicado sozinho.
2. Abra o site **no navegador de dentro do headset** (por exemplo, o navegador do Meta Quest).
3. Pressione **Entrar no VR imersivo** e aceite o pedido de acesso ao VR. O botão é oferecido somente quando o aparelho e navegador informam suporte.
4. Olhe para um equipamento; use o **gatilho do controle** para inspecionar. Na base da cena há quatro opções: **Iniciar tour**, **Ping visual**, **Falha demo** e **Restaurar**. Aponte e pressione o gatilho. Se não houver alvo selecionado, o gatilho inicia/avança o tour.
5. Use o menu do sistema do óculos para encerrar o modo VR.

**Por que HTTPS?** WebXR usa recursos seguros do navegador e uma solicitação de sessão VR feita por ação do usuário. Abrir um HTML local (`file://`) ou um site HTTP normal não equivale a publicar em HTTPS. O atalho `localhost` pode ser confiável no próprio dispositivo, mas **localhost do headset não aponta para seu computador**.

## Como apresentar com óculos de celular/Cardboard

1. Abra a versão HTML no celular. Idealmente, use o site HTTPS também neste modo.
2. Vire o aparelho na horizontal e toque **3D lado a lado**.
3. Veja duas imagens do mesmo cenário — uma para cada olho — e coloque o celular no visor compatível.
4. Toque **Usar movimento** para habilitar sensores do aparelho quando disponíveis. Você pode **Centralizar** ou usar **Próxima etapa**.
5. Sem sensor, a cena ainda pode ser girada arrastando o dedo na tela. Um olhar fixo por cerca de 1,5 s sobre um equipamento seleciona sua descrição.

O modo 3D lado a lado não é WebXR e não garante alinhamento perfeito para todos os tipos de lentes ou telas. Confira a orientação e o conforto antes da apresentação. **Permaneça sentado ou parado em um local seguro durante o uso do visor**.

## O que foi acrescentado

- Duas vistas por olho com deslocamento estereoscópico no modo de celular.
- Suporte a sessões `immersive-vr`, `XRWebGLLayer`, views e projeções por olho via WebXR.
- Cena centralizada à frente de quem veste o headset, sem rotação automática para maior conforto.
- Etiquetas e painel de informação como objetos 3D visíveis no headset (não dependem da interface 2D).
- Raycasting por direção de olhar ou controle para selecionar nós e menu VR 3D.
- Tour, ping educativo, falhas demonstrativas e restauração selecionáveis de dentro do headset.
- Controles de giroscópio opcionais e centralização para Cardboard.
- Versão integrada de um só HTML e versão modular editável em `Preview/`.
- Continuidade do modo computador e da topologia com 12 dispositivos e 11 links; todo tráfego é **simulado**, não comunicação ICMP real.

## Arquivos

- **Cisco_Network_VR_Standalone.html** — arquivo único (HTML, CSS e JavaScript incorporados)
- **Preview/index.html**, **Preview/style.css**, **Preview/app.js** — fontes editáveis
- **Media/** — imagens de teste da apresentação e vídeo cinematográfico original

## Hospedagem segura

Qualquer serviço de hospedagem estática que ofereça HTTPS pode servir os arquivos, incluindo GitHub Pages ou Netlify. Envie `index.html`, `style.css` e `app.js` da pasta `Preview` para a mesma pasta do host. Caso queira apenas um arquivo, publique o `Cisco_Network_VR_Standalone.html` como `index.html`.

Um servidor local de teste para computador pode ser iniciado dentro da pasta Preview:

```bash
python -m http.server 8000
```

Acesse `http://localhost:8000` no navegador do **próprio computador**. Para apresentar com o óculos, prefira a hospedagem HTTPS, pois endereços HTTP em outro dispositivo geralmente não autorizam WebXR.

## Verificação e limites

- Testes automatizados verificaram carregamento HTML, menus de modo, abertura/fechamento da tela dividida, botão de tour e ausência de exceções JavaScript nesses cenários, usando Chromium emulando desktop.
- O ambiente de testes não disponibilizou GPU WebGL nem um headset físico. **WebXR imersivo, projeção real nas lentes, controles e rastreamento de cabeça não puderam ser validados em hardware real**. Faça ensaio no seu modelo de óculos antes da apresentação.
- Acompanha alternativa 2D para navegadores sem WebGL, mas o modo imersivo exige WebGL real no óculos.
- Compatibilidade final depende de headset, navegador, sensores e permissões.

