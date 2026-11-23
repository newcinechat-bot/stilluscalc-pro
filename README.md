<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>StillusCalc PRO - Sistema de Loja</title>
<meta name="theme-color" content="#0F172A">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Inter,Arial,sans-serif}
body{background:#F1F5F9;color:#0F172A;min-height:100vh}
.topo-mobile{display:flex;align-items:center;gap:10px;background:#fff;padding:10px 12px;position:sticky;top:0;z-index:50;box-shadow:0 1px 6px rgba(0,0,0,.08)}
.btn-menu{background:#F1F5F9;border:none;width:40px;height:40px;border-radius:10px;font-size:20px;cursor:pointer}
.logo-top{width:40px;height:40px;background:#FEF3C7;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:22px}
.topo-mobile b{font-size:15px;line-height:1.1;display:block}
.topo-mobile small{font-size:12px;color:#64748B}
.topo-acoes{margin-left:auto;display:flex;gap:6px}
.topo-acoes button{background:#F1F5F9;border:none;width:38px;height:38px;border-radius:50%;font-size:17px;cursor:pointer}
.sidebar{position:fixed;left:-300px;top:0;bottom:0;width:280px;background:#0F172A;color:#fff;z-index:100;padding:18px 14px;overflow-y:auto;transition:left .25s}
.sidebar.aberta{left:0}
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:90}
.overlay.mostrar{display:block}
.side-logo{display:flex;gap:10px;align-items:center;margin-bottom:22px}
.side-logo .ic{width:44px;height:44px;background:#FACC15;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:26px}
.side-logo b{font-size:20px;line-height:1}
.side-logo b span{background:#FACC15;color:#000;font-size:11px;padding:2px 6px;border-radius:6px;margin-left:4px;vertical-align:middle}
.side-logo small{font-size:10px;letter-spacing:2px;color:#94A3B8}
.side-secao{font-size:11px;letter-spacing:2px;color:#64748B;font-weight:bold;margin:18px 0 8px 10px}
.side-item{display:flex;gap:10px;align-items:center;padding:11px 10px;border-radius:10px;cursor:pointer;font-size:14px;color:#E2E8F0;border:none;background:transparent;width:100%;text-align:left}
.side-item:hover{background:#1E293B}
.side-item.ativo{background:#1E293B;border-left:3px solid #FACC15;color:#FACC15;font-weight:bold}
.side-item span{font-size:18px}
.side-rodape{margin-top:20px;border-top:1px solid #1E293B;padding-top:14px;font-size:12px;color:#94A3B8}
.dot-verde{width:9px;height:9px;background:#22C55E;border-radius:50%;display:inline-block}
.wrap{max-width:520px;margin:0 auto;padding:12px;padding-bottom:30px}
.kicker{font-size:11px;letter-spacing:2px;color:#B45309;font-weight:bold}
h1.titulo{font-size:32px;line-height:1.05;letter-spacing:-1px;margin:4px 0 6px}
.sub{font-size:13px;color:#64748B;line-height:1.5}
.pill-data{display:inline-flex;align-items:center;gap:6px;background:#fff;border:1px solid #E2E8F0;padding:7px 10px;border-radius:20px;font-size:12px;font-weight:bold;margin:10px 0}
.cards3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin:10px 0}
.card-mini{background:#fff;border-radius:14px;padding:10px;box-shadow:0 1px 4px rgba(0,0,0,.05)}
.card-mini small{font-size:11px;color:#475569;display:flex;justify-content:space-between}
.card-mini b{font-size:15px;display:block;margin:6px 0 4px}
.card-mini span{font-size:10px;color:#64748B}
.card{background:#fff;border-radius:16px;padding:14px;margin-bottom:12px;box-shadow:0 1px 6px rgba(0,0,0,.06)}
.card h3{font-size:16px;display:flex;gap:8px;align-items:center}
.card h3 small{font-weight:normal;color:#64748B;font-size:12px;display:block}
.visor{background:#0F172A;color:#fff;border-radius:14px;padding:14px;margin:12px 0;text-align:right}
.visor small{color:#94A3B8;font-size:11px;letter-spacing:2px;display:flex;justify-content:space-between}
.visor b{font-size:34px;font-weight:800}
.teclas{display:grid;grid-template-columns:repeat(4,1fr);gap:8px}
.teclas button{padding:13px 0;border:none;border-radius:12px;font-size:17px;font-weight:bold;cursor:pointer;background:#F1F5F9;color:#0F172A}
.teclas button.op{background:#FEF3C7}
.teclas button.limpar{background:#FEE2E2;color:#DC2626}
.teclas button.igual{background:#059669;color:#fff}
.flex2{display:flex;gap:8px}
.btn{border:none;border-radius:10px;padding:12px;font-weight:bold;cursor:pointer;width:100%;margin-bottom:6px;font-size:14px}
.btn-amarelo{background:#FACC15;color:#000}
.btn-verde{background:#22C55E;color:#fff}
.btn-azul{background:#3B82F6;color:#fff}
.btn-cinza{background:#F1F5F9;color:#0F172A}
.btn-vermelho{background:#EF4444;color:#fff}
.btn-escuro{background:#0F172A;color:#fff}
.btn-roxo{background:#7C3AED;color:#fff}
.btn-whats{background:#25D366;color:#fff}
input,select,textarea{width:100%;padding:11px;border:1px solid #CBD5E1;border-radius:10px;margin-bottom:8px;font-size:15px;background:#fff}
label{font-size:12px;font-weight:bold;display:block;margin-bottom:3px}
.modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:200;align-items:flex-end;justify-content:center}
.modal.aberto{display:flex}
.modal-box{background:#fff;width:100%;max-width:520px;max-height:92vh;overflow:auto;border-radius:18px 18px 0 0;padding:16px;padding-bottom:26px}
.modal-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;gap:8px}
.modal-top h3{font-size:17px}
.btn-fechar{background:#F1F5F9;border:none;width:36px;height:36px;border-radius:50%;font-weight:bold;cursor:pointer;font-size:16px}
.resultado{background:#F0FDF4;border:2px solid #22C55E;border-radius:12px;padding:12px;font-size:14px;line-height:1.6;margin-top:8px}
.resultado.perigo{background:#FEF2F2;border-color:#EF4444}
.resultado.atencao{background:#FFFBEB;border-color:#F59E0B}
.item-cad{display:flex;gap:8px;align-items:center;border-bottom:1px solid #E2E8F0;padding:8px 0}
.item-cad .ft{width:52px;height:52px;border-radius:10px;background:#FEF2F2;display:flex;align-items:center;justify-content:center;font-size:26px;overflow:hidden;flex-shrink:0}
.item-cad .ft img{width:100%;height:100%;object-fit:cover}
.item-cad .info{flex:1;min-width:0}
.chip{display:inline-block;background:#FEF3C7;border:1px solid #FACC15;padding:6px 10px;border-radius:20px;font-size:12px;font-weight:bold;margin:3px;cursor:pointer}
.chip-vend{border:1px solid #6366F1;background:#E0E7FF;padding:7px 12px;border-radius:20px;font-size:12px;font-weight:bold;cursor:pointer}
.chip-vend.ativo{background:#0F172A;color:#fff}
.meta-card{background:#F8FAFC;border:2px solid #E2E8F0;border-radius:14px;padding:12px;margin-bottom:10px}
.meta-conta{background:#0F172A;color:#fff;border-radius:10px;padding:10px;text-align:center;font-size:14px;margin:8px 0}
.barra-meta{height:18px;background:#E2E8F0;border-radius:20px;overflow:hidden;margin:6px 0}
.barra-meta div{height:100%;background:#22C55E;text-align:center;color:#fff;font-size:11px;line-height:18px;font-weight:bold}
.rank-item{display:flex;gap:10px;align-items:center;background:#fff;border:2px solid #E2E8F0;border-radius:12px;padding:10px;margin-bottom:8px}
.rank-item.top1{border-color:#FACC15;background:#FFFBEB}
.graf-bar{display:flex;align-items:flex-end;gap:8px;height:180px;padding:10px;background:#F8FAFC;border-radius:12px;margin:10px 0;overflow-x:auto}
.graf-col{flex:1;min-width:52px;display:flex;flex-direction:column;align-items:center;justify-content:flex-end;gap:4px}
.graf-col .barra{width:100%;max-width:48px;border-radius:8px 8px 0 0;display:flex;align-items:flex-start;justify-content:center;color:#fff;font-weight:bold;font-size:11px;padding-top:6px;min-height:18px}
.chat-header{background:#075E54;color:#fff;padding:10px;border-radius:12px 12px 0 0;display:flex;align-items:center;gap:10px}
.chat-box{background:#ECE5DD;border-radius:0 0 12px 12px;padding:10px;min-height:260px;max-height:360px;overflow-y:auto;display:flex;flex-direction:column;gap:8px}
.msg{max-width:82%;padding:8px 10px;border-radius:12px;font-size:13px;line-height:1.4}
.msg.eu{background:#DCF8C6;align-self:flex-end}
.msg.cliente{background:#fff;align-self:flex-start}
.msg.robo{background:#FFF3CD;align-self:flex-start;border:1px solid #FACC15}
.msg small{display:block;font-size:10px;color:#888;text-align:right}
.msg img,.msg video{width:100%;max-width:220px;border-radius:10px;display:block;margin:4px 0}
.prod-card{background:#fff;border:1px solid #E2E8F0;border-radius:10px;padding:8px;margin:4px 0}
.prod-card img{width:100%;height:110px;object-fit:cover;border-radius:8px}
.cliente-item{display:flex;gap:8px;align-items:center;padding:8px;border-bottom:1px solid #F1F5F9;cursor:pointer}
.cliente-item .av{width:40px;height:40px;background:#25D366;color:#fff;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:bold}
.emoji-panel{display:flex;flex-wrap:wrap;gap:4px;background:#fff;border:1px solid #E2E8F0;border-radius:12px;padding:8px;margin:6px 0}
.emoji-panel span{font-size:22px;cursor:pointer;padding:4px}
.caixa-item{background:#fff;border:2px solid #E2E8F0;border-radius:12px;padding:10px;margin-bottom:8px}
.caixa-item.aguardando{border-color:#F59E0B;background:#FFFBEB}
.caixa-item.finalizado{border-color:#22C55E;background:#F0FDF4}
.plano-card{border:2px solid #E2E8F0;border-radius:14px;padding:12px;margin-bottom:10px;cursor:pointer}
.plano-card.selecionado{border-color:#FACC15;background:#FFFBEB}
.plano-card.pro{border-color:#22C55E;background:#F0FDF4}
.qr-box{background:#fff;border:2px dashed #CBD5E1;border-radius:12px;padding:12px;text-align:center;margin:10px 0}
.qr-box img{width:180px;height:180px}
.login-aba{display:flex;gap:6px;margin-bottom:10px}
.login-aba button{flex:1;padding:12px;border:none;border-radius:10px;font-weight:bold;cursor:pointer;background:#F1F5F9}
.login-aba button.ativo{background:#0F172A;color:#fff}
.venda-item{font-size:13px;border-bottom:1px solid #E2E8F0;padding:6px 0;display:flex;justify-content:space-between;gap:6px}
.foto-fundo{width:100%;height:110px;object-fit:cover;border-radius:12px;display:none;margin-bottom:8px;border:3px solid #FACC15}
.range{width:100%}
.modo{display:flex;gap:6px;margin-bottom:10px}
.modo button{flex:1;padding:10px;border:none;border-radius:10px;font-weight:bold;cursor:pointer;background:#E2E8F0}
.modo button.ativo{background:#0F172A;color:#fff}
@media(min-width:768px){.sidebar{left:0}.wrap{margin-left:280px}.topo-mobile{margin-left:280px}.overlay{display:none!important}}
</style>
</head>
<body>
<div class="overlay" id="overlay" onclick="fecharMenu()"></div>
<div class="sidebar" id="sidebar">
<div class="side-logo"><div class="ic">🧮</div><div><b>StillusCalc <span>PRO</span></b><br><small>SISTEMA DE LOJA</small></div></div>
<div class="side-secao">PRINCIPAL</div>
<button class="side-item ativo" onclick="irPara('visao',this)"><span>⊞</span> Visão geral</button>
<button class="side-item" onclick="irPara('vend',this)"><span>🧮</span> Calculadora do vendedor</button>
<div class="side-secao">OPERAÇÕES</div>
<button class="side-item" onclick="verificarTravaEAbrir('modalLoja',this)"><span>🏪</span> Minha loja</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalItens',this)"><span>📦</span> Meus itens</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalCad',this)"><span>+</span> Cadastrar item</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalCaixa',this)"><span>🧾</span> Caixa</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalChat',this)"><span>💬</span> Chat com cliente</button>
<div class="side-secao">DESEMPENHO</div>
<button class="side-item" onclick="verificarTravaEAbrir('modalMeta',this)"><span>🎯</span> Metas</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalRank',this)"><span>🏆</span> Ranking</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalGrafico',this)"><span>📊</span> Gráfico de vendas</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalRel',this)"><span>📄</span> Relatórios</button>
<div class="side-secao">PREFERÊNCIAS</div>
<button class="side-item" onclick="verificarTravaEAbrir('modalHist',this)"><span>🕒</span> Histórico</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalFoto',this)"><span>🖼️</span> Foto de fundo</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalVendEquipe',this)"><span>👥</span> Equipe / Vendedores</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalSync',this)"><span>🔄</span> Sincronizar</button>
<button class="side-item" onclick="verificarTravaEAbrir('modalBackup',this)"><span>💾</span> Backup</button>
<button class="side-item" onclick="abrirModal('modalPlanos',this)"><span>💎</span> Planos</button>
<div class="side-rodape"><span class="dot-verde"></span> <b style="color:#fff">Área de trabalho</b><br><span id="sideUsuario">Não logado</span><br><span id="sideLojaNome">Sua loja</span><br><button class="btn btn-vermelho" style="margin-top:10px" onclick="sairLogin()">🚪 SAIR / TROCAR USUÁRIO</button></div>
</div>

<div class="topo-mobile">
<button class="btn-menu" onclick="abrirMenu()">☰</button>
<div class="logo-top">🏪</div>
<div><b id="nomeLojaTopo">Minha Loja</b><small id="sloganTopo">O barato é aqui!</small></div>
<div class="topo-acoes"><button onclick="location.reload()">↻</button><button onclick="abrirModal('modalSync')">⬇</button></div>
</div>

<div class="wrap" id="visaoGeral">
<div class="kicker">— CENTRAL DE OPERAÇÕES</div>
<h1 class="titulo">Visão geral</h1>
<p class="sub">Sua calculadora e a rotina da sua loja em um só lugar.</p>
<div><span class="pill-data">📅 <span id="dataHoje">23 de novembro de 2026</span></span> <span class="pill-data" id="pillTeste" style="background:#DCFCE7;color:#15803D;cursor:pointer" onclick="abrirModal('modalPlanos')">🎁 TESTE GRÁTIS: 7 dias</span></div>
<div class="cards3">
<div class="card-mini"><small>Vendas de hoje ⚡</small><b id="cardHoje">R$ 0,00</b><span id="cardMetaDia">Meta R$ 3.000,00</span></div>
<div class="card-mini"><small>Vendas da semana 📅</small><b id="cardSemana">R$ 0,00</b><span id="cardMetaSemana">Meta R$ 15.000,00</span></div>
<div class="card-mini"><small>Vendas do mês 🔒</small><b id="cardMes">R$ 0,00</b><span id="cardMetaMes">Meta R$ 60.000,00</span></div>
</div>

<div class="card" id="cardCalcNormal">
<h3><span style="background:#FEF3C7;padding:6px 9px;border-radius:8px">🧮</span><span>Calculadora normal<small>Para contas rápidas no dia a dia</small></span><span style="margin-left:auto;background:#F1F5F9;padding:6px 9px;border-radius:20px;font-size:14px;cursor:pointer" onclick="calcLimpar()">↻</span></h3>
<div class="visor"><small><span>● VISOR DIGITAL</span><span>StillusCalc PRO</span></small><b id="visorCalc">0</b><small id="histCalc" style="justify-content:flex-end;letter-spacing:0">--</small></div>
<div class="teclas">
<button class="limpar" onclick="calcLimpar()">C</button><button onclick="calcAdd('(')">(</button><button onclick="calcAdd(')')">)</button><button class="op" onclick="calcAdd('%')">%</button>
<button onclick="calcSqrt()">√</button><button onclick="calcQuad()">x²</button><button onclick="calcBack()">⌫</button><button class="op" onclick="calcAdd('/')">÷</button>
<button onclick="calcAdd('7')">7</button><button onclick="calcAdd('8')">8</button><button onclick="calcAdd('9')">9</button><button class="op" onclick="calcAdd('*')">×</button>
<button onclick="calcAdd('4')">4</button><button onclick="calcAdd('5')">5</button><button onclick="calcAdd('6')">6</button><button class="op" onclick="calcAdd('-')">-</button>
<button onclick="calcAdd('1')">1</button><button onclick="calcAdd('2')">2</button><button onclick="calcAdd('3')">3</button><button class="op" onclick="calcAdd('+')">+</button>
<button onclick="calcAdd('0')">0</button><button onclick="calcAdd('00')">00</button><button onclick="calcAdd('.')">,</button><button class="igual" onclick="calcIgual()">=</button>
</div>
<div class="flex2" style="margin-top:10px"><button class="btn btn-cinza" onclick="copiarVisor()">⧉ Copiar resultado</button><button class="btn btn-amarelo" onclick="usarComoPreco()">🏷️ Usar como preço</button></div>
</div>

<div class="card">
<h3>👥 Equipe de vendas</h3>
<p style="font-size:12px;color:#64748B;margin:6px 0">Quem está vendendo agora? <b id="vendedorAtualTopo">--</b></p>
<div id="listaVendedoresTopo" style="display:flex;flex-wrap:wrap;gap:6px"></div>
<button class="btn btn-roxo" style="margin-top:10px" onclick="verificarTravaEAbrir('modalVendEquipe')">+ CADASTRAR VENDEDOR / TROCAR VENDEDOR</button>
<div class="flex2" style="margin-top:6px"><button class="btn btn-whats" onclick="verificarTravaEAbrir('modalChat')">💬 CHAT COM CLIENTE</button><button class="btn btn-roxo" onclick="verificarTravaEAbrir('modalCaixa')">🧾 IR PRO CAIXA</button></div>
</div>

<div class="card" style="text-align:center">
<p style="font-size:11px;color:#94A3B8">© 2026 StillusCalc PRO - Todos os direitos reservados.</p>
<button class="btn btn-cinza" style="margin-top:8px" onclick="abrirModal('modalBoasVindas')">VER BOAS-VINDAS NOVAMENTE</button>
</div>
</div>
<!-- INICIO PARTE 2 -->
<div id="modalLogin" class="modal"><div class="modal-box">
<div class="modal-top"><h3>👋 Entrar no StillusCalc PRO</h3></div>
<p style="font-size:13px;color:#64748B;margin-bottom:10px">Entre para usar sua loja. Vendedor só vende, Dono controla tudo.</p>
<div class="login-aba"><button id="abaDono" class="ativo" onclick="setAbaLogin('dono')">👑 SOU O DONO</button><button id="abaVend" onclick="setAbaLogin('vend')">👤 SOU VENDEDOR</button></div>
<div id="boxLoginDono">
<label>Nome da sua loja</label><input id="loginLojaNome" placeholder="Ex: Minha Loja" maxlength="60">
<label>Seu WhatsApp (só números)</label><input id="loginDonoWhats" placeholder="Ex: 61999999999" maxlength="13">
<label>Código de liberação (se já pagou, senão deixa em branco)</label><input id="loginCodigoDono" placeholder="Ex: PRO-30-STILLUS" style="text-transform:uppercase">
<button class="btn btn-verde" style="padding:15px;font-size:16px" onclick="entrarComoDono()">👑 ENTRAR COMO DONO - 7 DIAS GRÁTIS</button>
</div>
<div id="boxLoginVend" style="display:none">
<label>Código da Loja (o dono te passa)</label><input id="loginCodigoLoja" placeholder="Ex: LOJA-ABC123" style="text-transform:uppercase">
<label>Seu Login</label><input id="loginVendLogin" placeholder="Ex: maria">
<label>Sua Senha</label><input id="loginVendSenha" placeholder="Ex: 1234">
<button class="btn btn-verde" style="padding:15px;font-size:16px" onclick="entrarComoVendedor()">👤 ENTRAR COMO VENDEDOR</button>
<button class="btn btn-cinza" onclick="entrarTesteVendedor()">🧪 TESTAR COMO VENDEDOR - Login: maria / Senha: 1234</button>
</div>
<p style="font-size:11px;color:#94A3B8;text-align:center">Ao entrar você concorda com os termos do StillusCalc PRO.</p>
</div></div>

<div id="modalBoasVindas" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🎉 Bem-vindo ao StillusCalc PRO!</h3><button class="btn-fechar" onclick="fecharModal('modalBoasVindas')">X</button></div>
<p style="font-size:13px;line-height:1.6;margin-bottom:10px">Configure sua loja em 30 segundos e comece a vender hoje!</p>
<label>Nome da sua loja</label><input id="bvLoja" placeholder="Ex: Minha Loja" maxlength="60">
<label>WhatsApp da loja</label><input id="bvWhats" placeholder="Ex: 61999999999" maxlength="13">
<label>Vendedores (separados por vírgula)</label><input id="bvVends" placeholder="Ex: Maria, João" maxlength="120">
<label>Meta do Mês (R$)</label><input id="bvMetaMes" type="number" value="60000">
<button class="btn btn-verde" style="padding:15px;font-size:16px" onclick="concluirBoasVindas()">✅ COMEÇAR - 7 DIAS GRÁTIS</button>
</div></div>

<div id="modalPlanos" class="modal"><div class="modal-box">
<div class="modal-top"><h3>💎 Planos - StillusCalc PRO</h3><button class="btn-fechar" onclick="fecharModal('modalPlanos')">X</button></div>
<div id="statusPlanoBox" style="background:#F0FDF4;border:2px solid #22C55E;border-radius:12px;padding:10px;font-size:13px;line-height:1.6;margin-bottom:10px">Carregando...</div>
<div class="plano-card" id="cardBasico" onclick="selecionarPlano('basico')"><b>📦 BÁSICO</b><br><b style="font-size:20px">R$ 49,90/mês</b><br><small>Calculadora + Itens + Metas</small></div>
<div class="plano-card pro selecionado" id="cardPro" onclick="selecionarPlano('pro')"><b>⭐ PRO - MAIS VENDIDO</b><br><b style="font-size:20px">R$ 89,90/mês</b><br><small>Tudo do Básico + Chat + Caixa + Ranking + Gráfico + Robô</small></div>
<div class="plano-card" id="cardVitalicio" onclick="selecionarPlano('vitalicio')"><b>💎 VITALÍCIO</b><br><b style="font-size:20px">R$ 497 uma vez</b><br><small>Paga uma vez, usa pra sempre!</small></div>
<button class="btn btn-verde" id="btnPagarPlano" style="padding:15px;font-size:16px" onclick="mostrarPagamento()">💳 PAGAR COM PIX - PLANO PRO - R$ 89,90/mês</button>
<div id="areaPagamento" style="display:none"><div class="qr-box"><h4 id="tituloPagamento">Pagamento</h4><img id="imgQR" src="" alt="QR Code Pix"><p style="font-size:12px;margin:8px 0">1. Abra o app do seu banco<br>2. Pix > Ler QR Code<br>3. Confirme o pagamento</p><button class="btn btn-amarelo" onclick="copiarPix()">📋 COPIAR CÓDIGO PIX COPIA E COLA</button><button class="btn btn-whats" onclick="enviarComprovanteWhats()">📱 ENVIAR COMPROVANTE NO WHATSAPP</button></div></div>
<label style="margin-top:10px">Tem código de liberação? Cole aqui</label><input id="codigoLiberacao" placeholder="Ex: PRO-30-STILLUS" style="text-transform:uppercase">
<button class="btn btn-escuro" onclick="validarCodigo()">🔓 LIBERAR COM CÓDIGO</button>
<button class="btn btn-cinza" onclick="instalarApp()" id="btnInstalar" style="display:none">📲 INSTALAR APP NO CELULAR</button>
</div></div>

<div id="modalLoja" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🏪 Minha Loja</h3><button class="btn-fechar" onclick="fecharModal('modalLoja')">X</button></div>
<label>Nome da loja</label><input id="cfgLoja" maxlength="60">
<label>WhatsApp da loja</label><input id="cfgWhats" maxlength="13">
<label>Slogan</label><input id="cfgSlogan" maxlength="80">
<label>Tipo de loja</label><select id="cfgTipo"><option>Móveis e Eletrodomésticos</option><option>Loja de Roupas</option><option>Celulares</option><option>Loja Geral</option><option>Outro</option></select>
<label>Código da Loja (passe pros vendedores)</label><input id="cfgCodigoLoja" readonly style="background:#FFFBEB;font-weight:bold">
<button class="btn btn-verde" onclick="salvarLoja()">💾 SALVAR LOJA</button>
</div></div>

<div id="modalSync" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🔄 Sincronizar / Entrar em Loja</h3><button class="btn-fechar" onclick="fecharModal('modalSync')">X</button></div>
<div id="boxCodigoLojaVendedor" style="background:#FFFBEB;border:1px solid #FACC15;border-radius:10px;padding:10px;font-size:12px;line-height:1.6;margin-bottom:10px"></div>
<label>Link da Loja (para enviar pros vendedores)</label><input id="codigoLoja" readonly>
<div class="flex2"><button class="btn btn-amarelo" onclick="copiarLinkLoja()">📋 COPIAR LINK</button><button class="btn btn-whats" onclick="enviarLinkLojaWhats()">📱 ENVIAR NO WHATS</button></div>
<hr style="margin:12px 0;border:none;border-top:1px solid #E2E8F0">
<h4>📤 Enviar minhas vendas pro dono</h4>
<p style="font-size:12px;color:#64748B;margin:6px 0">Vendedor: clique abaixo e mande no WhatsApp do dono.</p>
<button class="btn btn-verde" onclick="enviarVendasWhats()">📱 ENVIAR MINHAS VENDAS NO WHATS</button>
<h4 style="margin-top:10px">📥 Receber vendas (Dono)</h4>
<label>Cole o código que o vendedor mandou</label><textarea id="codigoReceber" rows="3" placeholder="Cole aqui o código STILLUS-..."></textarea>
<button class="btn btn-escuro" onclick="receberVendas()">📥 RECEBER VENDAS</button>
<div id="statusSync" style="font-size:12px;margin-top:8px;background:#F8FAFC;padding:8px;border-radius:8px"></div>
</div></div>

<div id="modalBackup" class="modal"><div class="modal-box">
<div class="modal-top"><h3>💾 Backup</h3><button class="btn-fechar" onclick="fecharModal('modalBackup')">X</button></div>
<p style="font-size:13px;margin-bottom:10px">Salve tudo da sua loja pra não perder nada!</p>
<button class="btn btn-verde" onclick="exportarBackup()">⬇️ BAIXAR BACKUP AGORA</button>
<label style="margin-top:10px">Restaurar backup (arquivo .json)</label>
<label class="btn btn-amarelo" style="display:block;text-align:center">📂 ESCOLHER ARQUIVO DE BACKUP<input type="file" accept=".json" style="display:none" onchange="importarBackup(this)"></label>
<button class="btn btn-vermelho" onclick="apagarTudo()">🗑️ APAGAR TUDO E COMEÇAR DO ZERO</button>
</div></div>

<div id="modalVend" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🧮 Calculadora do Vendedor</h3><button class="btn-fechar" onclick="fecharModal('modalVend')">X</button></div>
<div class="modo"><button id="btnModoVend" class="ativo" onclick="setModo('vend')">MODO VENDEDOR</button><button id="btnModoCli" onclick="setModo('cli')">MODO CLIENTE</button></div>
<label>Vendedor da venda</label><select id="vVendedor"></select>
<label>Cliente (opcional)</label><input id="vCliente" placeholder="Nome do cliente..." maxlength="60">
<label>Item selecionado</label><input id="vNome" readonly placeholder="Clique num item em Meus Itens ou digite o código">
<label>Código</label><div class="flex2"><input id="vCodigo" placeholder="001" style="text-transform:uppercase"><button class="btn btn-escuro" style="width:110px" onclick="puxarItem()">PUXAR</button></div>
<label>Preço de Venda (R$)</label><input id="vPreco" type="number" oninput="calcularVendedor()">
<label>Preço de Custo (R$)</label><input id="vCusto" type="number" oninput="calcularVendedor()">
<label>Desconto (%)</label><input id="vDesc" type="range" min="0" max="50" value="10" class="range" oninput="document.getElementById('vDescLabel').innerText=this.value+'%';calcularVendedor()">
<div style="text-align:center;font-weight:bold">Desconto: <span id="vDescLabel">10%</span></div>
<div style="display:flex;gap:6px;flex-wrap:wrap;margin:8px 0"><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(0)">0%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(5)">5%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(10)">10%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(15)">15%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(20)">20%</button></div>
<label>Comissão (%)</label><input id="vComissao" type="number" value="3" oninput="calcularVendedor()">
<label>Entrada (R$)</label><input id="vEntrada" type="number" value="0" oninput="calcularVendedor()">
<label>Frete + Montagem (R$)</label><input id="vFrete" type="number" value="0" oninput="calcularVendedor()">
<div id="resultadoVend" class="resultado">Selecione um item!</div>
<div id="parcelasVend" style="font-size:13px;margin-top:8px;background:#F8FAFC;padding:10px;border-radius:10px"></div>
<button class="btn btn-verde" style="padding:15px;font-size:16px;margin-top:10px" onclick="venderItemAtual()">🛒 VENDER AGORA - FINALIZAR DIRETO</button>
<button class="btn btn-roxo" style="padding:15px;font-size:16px" onclick="enviarProCaixa()">🧾 ENVIAR PRO CAIXA</button>
<div class="flex2"><button class="btn btn-azul" onclick="enviarWhats()">ENVIAR NO WHATS</button><button class="btn btn-cinza" onclick="salvarCalculo()">SALVAR CÁLCULO</button></div>
<button class="btn btn-cinza" onclick="limparVend()">LIMPAR</button>
</div></div>

<div id="modalCad" class="modal"><div class="modal-box">
<div class="modal-top"><h3>Cadastrar Item</h3><button class="btn-fechar" onclick="fecharModal('modalCad')">X</button></div>
<label>Nome do item</label><input id="nNome" maxlength="80">
<label>Código</label><input id="nCodigo" maxlength="20" style="text-transform:uppercase">
<label>Preço de Venda (R$)</label><input id="nPreco" type="number" min="0">
<label>Preço de Custo (R$)</label><input id="nCusto" type="number" min="0">
<label>Categoria</label><select id="nCat"><option>Produto Geral</option><option>Sala de Estar</option><option>Cozinha</option><option>Cama / Colchão</option><option>Celulares</option><option>Roupas</option><option>Outro</option></select>
<label>Foto do item (opcional)</label><input type="file" accept="image/*" onchange="preverFotoItem(this)">
<img id="prevItem" class="foto-fundo" style="height:90px">
<button class="btn btn-verde" onclick="cadastrarItem()">CADASTRAR ITEM</button>
</div></div>

<div id="modalItens" class="modal"><div class="modal-box">
<div class="modal-top"><h3>Meus Itens</h3><button class="btn-fechar" onclick="fecharModal('modalItens')">X</button></div>
<p style="font-size:12px;color:#64748B;margin-bottom:8px">Vendendo como: <b id="vendendoComoItens">--</b></p>
<input id="buscaItem" placeholder="Buscar por nome ou código..." oninput="renderItens()">
<div id="listaItens"></div>
<div id="favoritosBox" style="margin-top:8px"></div>
</div></div>

<div id="modalCaixa" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🧾 Caixa</h3><button class="btn-fechar" onclick="fecharModal('modalCaixa')">X</button></div>
<div id="resumoCaixa" style="background:#0F172A;color:#fff;border-radius:12px;padding:12px;font-size:13px;line-height:1.6;margin-bottom:10px"></div>
<h4>⏳ Aguardando pagamento</h4><div id="listaCaixa"></div>
<h4 style="margin-top:12px">✅ Finalizados</h4><div id="listaCaixaFinalizados"></div>
</div></div>
<!-- INICIO PARTE 3 - ULTIMA -->
<div id="modalVendEquipe" class="modal"><div class="modal-box">
<div class="modal-top"><h3>👥 Equipe de Vendedores - Só o Dono cadastra</h3><button class="btn-fechar" onclick="fecharModal('modalVendEquipe')">X</button></div>
<div style="background:#FFFBEB;border:1px solid #FACC15;border-radius:10px;padding:10px;font-size:12px;line-height:1.6;margin-bottom:10px">
<b>Código da sua loja:</b> <span id="codigoLojaEquipe" style="font-size:15px;color:#0F172A">--</span><br>
Passe esse código + login + senha para o vendedor entrar.<br>
<button class="btn btn-amarelo" style="margin-top:6px" onclick="copiarDadosVendedores()">📋 COPIAR DADOS PARA ENVIAR NO WHATS</button>
</div>
<label>Nome do vendedor</label><input id="novoVendNome" maxlength="40" placeholder="Ex: Maria Silva">
<label>Login do vendedor (sem espaço, só letras)</label><input id="novoVendLogin" maxlength="30" placeholder="Ex: maria">
<label>Senha do vendedor</label><input id="novoVendSenha" maxlength="30" placeholder="Ex: 1234">
<button class="btn btn-verde" onclick="addVendedor()">+ CADASTRAR VENDEDOR COM LOGIN E SENHA</button>
<div id="listaVendedoresModal" style="display:flex;flex-wrap:wrap;gap:6px;margin-top:8px"></div>
<div id="listaLoginsVendedores" style="margin-top:10px"></div>
</div></div>

<div id="modalFoto" class="modal"><div class="modal-box">
<div class="modal-top"><h3>Foto da Loja no Fundo</h3><button class="btn-fechar" onclick="fecharModal('modalFoto')">X</button></div>
<img id="prevFundo" class="foto-fundo">
<label class="btn btn-amarelo" style="display:block;text-align:center">COLOCAR FOTO DA LOJA NO FUNDO<input type="file" accept="image/*" style="display:none" onchange="salvarFundo(this)"></label>
<button class="btn btn-cinza" onclick="removerFundo()">TIRAR FOTO DO FUNDO</button>
</div></div>

<div id="modalMeta" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🎯 Metas - Dia / Semana / Mês</h3><button class="btn-fechar" onclick="fecharModal('modalMeta')">X</button></div>
<div class="meta-card"><h3>☀️ Meta do Dia</h3><label>Meta do dia (R$)</label><input id="metaDia" type="number" oninput="salvarMetas()"><label>Já vendeu hoje (R$) - automático</label><input id="vendidoDia" readonly><div id="contaDia" class="meta-conta"></div><div class="barra-meta"><div id="barraDia">0%</div></div><div class="flex2"><button class="btn btn-cinza" onclick="zerarMeta('dia')">ZERAR DIA</button><button class="btn btn-verde" onclick="abrirModal('modalItens')">VENDER AGORA</button></div></div>
<div class="meta-card"><h3>📅 Meta da Semana</h3><label>Meta da semana (R$)</label><input id="metaSemana" type="number" oninput="salvarMetas()"><label>Já vendeu na semana (R$) - automático</label><input id="vendidoSemana" readonly><div id="contaSemana" class="meta-conta"></div><div class="barra-meta"><div id="barraSemana">0%</div></div><button class="btn btn-cinza" onclick="zerarMeta('semana')">ZERAR SEMANA</button></div>
<div class="meta-card"><h3>🗓️ Meta do Mês 🔒 TRAVADA</h3><div style="background:#FEF2F2;border-radius:10px;padding:8px;font-size:12px;text-align:center;margin-bottom:8px">🔒 META DO MÊS TRAVADA<br><span id="textoTravaMes">Mês atual: --</span></div><label>Meta do mês (R$)</label><input id="metaMes" type="number" readonly onclick="tentarEditarMes()" style="background:#F1F5F9"><label>Já vendeu no mês (R$) - automático</label><input id="vendidoMes" readonly><div id="contaMes" class="meta-conta"></div><div class="barra-meta"><div id="barraMes">0%</div></div><button class="btn btn-vermelho" onclick="fecharMes()">FECHAR MÊS E GERAR RELATÓRIO</button></div>
<h3>Vendas de Hoje</h3><div id="listaVendasHoje"></div><button class="btn btn-vermelho" onclick="limparVendasHoje()">LIMPAR VENDAS DE HOJE</button><button class="btn btn-verde" onclick="abrirModal('modalRel')">VER RELATÓRIO COMPLETO</button>
</div></div>

<div id="modalRank" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🏆 Ranking da Equipe</h3><button class="btn-fechar" onclick="fecharModal('modalRank')">X</button></div>
<div id="rankingBox"></div>
<div class="flex2"><button class="btn btn-verde" onclick="enviarRankingWhats()">📱 ENVIAR RANKING NO WHATS</button><button class="btn btn-cinza" onclick="abrirModal('modalVendEquipe')">+ VENDEDOR</button></div>
</div></div>

<div id="modalGrafico" class="modal"><div class="modal-box">
<div class="modal-top"><h3>📊 Gráfico de Vendas</h3><button class="btn-fechar" onclick="fecharModal('modalGrafico')">X</button></div>
<div id="resumoGrafico" style="background:#0F172A;color:#fff;border-radius:12px;padding:12px;font-size:13px;line-height:1.6"></div>
<div id="graficoBarras" class="graf-bar"></div>
<div id="listaGrafico"></div>
<button class="btn btn-verde" onclick="enviarGraficoWhats()">📱 ENVIAR GRÁFICO NO WHATS</button>
</div></div>

<div id="modalHist" class="modal"><div class="modal-box">
<div class="modal-top"><h3>Histórico de Cálculos</h3><button class="btn-fechar" onclick="fecharModal('modalHist')">X</button></div>
<div id="listaHist"></div><button class="btn btn-vermelho" onclick="limparHist()">LIMPAR HISTÓRICO</button>
</div></div>

<div id="modalRel" class="modal"><div class="modal-box">
<div class="modal-top"><h3>📊 Relatório</h3><button class="btn-fechar" onclick="fecharModal('modalRel')">X</button></div>
<label>Enviar relatório pra qual WhatsApp?</label><input id="whatsDestino" placeholder="Ex: 61999999999" maxlength="13">
<div id="relatorioBox"></div>
<div class="flex2" style="margin-top:10px"><button class="btn btn-verde" onclick="enviarRelatorioWhats()">📱 ENVIAR NO WHATSAPP</button><button class="btn btn-escuro" onclick="baixarRelatorioPDF()">📄 BAIXAR EM PDF</button></div>
<button class="btn btn-amarelo" onclick="baixarArquivoRelatorio()">⬇️ BAIXAR ARQUIVO DO RELATÓRIO</button>
<button class="btn btn-azul" onclick="copiarRelatorio()">📋 COPIAR RELATÓRIO</button>
</div></div>

<div id="modalChat" class="modal"><div class="modal-box">
<div class="modal-top"><h3>💬 Chat com Cliente</h3><button class="btn-fechar" onclick="fecharModal('modalChat')">X</button></div>
<label>Novo cliente</label><div class="flex2"><input id="novoClienteNome" placeholder="Nome do cliente..." maxlength="50"><button class="btn btn-verde" style="width:110px" onclick="addCliente()">+ ADD</button></div>
<div id="listaClientes" style="max-height:140px;overflow:auto;border:1px solid #E2E8F0;border-radius:10px;margin-bottom:10px"></div>
<div class="chat-header"><div style="width:38px;height:38px;background:#25D366;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:bold" id="chatAvatar">C</div><div style="flex:1"><b id="chatClienteNome">Cliente</b><br><small id="chatClienteStatus">--</small><br><small id="chatRoboStatus">Robo OFF</small></div><button class="btn btn-amarelo" style="width:auto;padding:8px 10px;margin:0" id="btnRobo" onclick="toggleRobo()">🤖 ROBO</button></div>
<div class="chat-box" id="chatBox"></div>
<div id="emojiPanel" class="emoji-panel" style="display:none"></div>
<div class="flex2" style="margin-top:8px"><button class="btn btn-cinza" style="width:46px" onclick="toggleEmoji()">😀</button><input id="chatInput" placeholder="Digite sua mensagem..." maxlength="500" style="margin:0"><button class="btn btn-verde" style="width:56px;margin:0" onclick="enviarMsgChat()">➤</button></div>
<div class="flex2"><label class="btn btn-cinza" style="text-align:center">📸 FOTO / 🎥 VÍDEO<input type="file" accept="image/*,video/*" style="display:none" onchange="enviarMidiaChat(this)"></label><button class="btn btn-amarelo" onclick="abrirModal('modalEnviarProduto')">📦 ENVIAR PRODUTO</button></div>
<div class="flex2"><button class="btn btn-azul" onclick="simularCliente()">💬 SIMULAR CLIENTE</button><button class="btn btn-roxo" onclick="comecarVendaNoChat()">🛒 COMEÇAR VENDA</button></div>
<button class="btn btn-whats" onclick="enviarChatWhatsApp()">📱 ENVIAR CONVERSA NO WHATSAPP</button>
<button class="btn btn-cinza" onclick="abrirModal('modalRobo')">⚙️ CONFIGURAR ROBÔ</button>
</div></div>

<div id="modalEnviarProduto" class="modal"><div class="modal-box">
<div class="modal-top"><h3>📦 Enviar Produto no Chat</h3><button class="btn-fechar" onclick="fecharModal('modalEnviarProduto')">X</button></div>
<div id="listaProdutosChat"></div>
</div></div>

<div id="modalRobo" class="modal"><div class="modal-box">
<div class="modal-top"><h3>🤖 Configurar Robô</h3><button class="btn-fechar" onclick="fecharModal('modalRobo')">X</button></div>
<label>Quando cliente falar OI</label><textarea id="roboOi" rows="2"></textarea>
<label>Quando perguntar PREÇO</label><textarea id="roboPreco" rows="2"></textarea>
<label>Quando pedir DESCONTO</label><textarea id="roboDesconto" rows="2"></textarea>
<label>Quando perguntar ENTREGA</label><textarea id="roboEntrega" rows="2"></textarea>
<label>Quando perguntar PARCELA</label><textarea id="roboParcela" rows="2"></textarea>
<label>Quando perguntar ESTOQUE</label><textarea id="roboEstoque" rows="2"></textarea>
<p style="font-size:11px;color:#64748B">Use {LOJA} {PRECO} {PRECO_DESC} - o robô troca sozinho!</p>
<button class="btn btn-verde" onclick="salvarRobo()">💾 SALVAR ROBÔ</button>
</div></div>

<script>
// ===== PIX - CHAVE COM +55 CORRIGIDA =====
var PIX_KEY = "+5561995873892";
var PIX_NOME = "STILLUSCALC PRO";
var PIX_CIDADE = "BRASILIA";
var WHATS_DONO = "5561995873892";
var planoSelecionado = "pro";
var planosInfo = {basico:{nome:"BÁSICO", valor:"49.90", label:"R$ 49,90/mês"}, pro:{nome:"PRO", valor:"89.90", label:"R$ 89,90/mês"}, vitalicio:{nome:"VITALÍCIO", valor:"497.00", label:"R$ 497 uma vez"}};
function crc16(str){var crc=0xFFFF; for(var i=0;i<str.length;i++){crc ^= str.charCodeAt(i)<<8; for(var j=0;j<8;j++){if(crc & 0x8000) crc = ((crc<<1) ^ 0x1021) & 0xFFFF; else crc = (crc<<1) & 0xFFFF;}} return crc.toString(16).toUpperCase().padStart(4,'0');}
function campo(id, val){var s=String(val); return id + String(s.length).padStart(2,'0') + s;}
function gerarPixCopiaECola(valor, txid){var gui = campo("00","BR.GOV.BCB.PIX") + campo("01", PIX_KEY); var merchant = campo("26", gui); var payloadSemCRC = "000201" + merchant + "52040000" + "5303986" + campo("54", valor) + "5802BR" + campo("59", PIX_NOME.substring(0,25)) + campo("60", PIX_CIDADE.substring(0,15)) + campo("62", campo("05", txid)) + "6304"; return payloadSemCRC + crc16(payloadSemCRC);}
function pixAtual(){var info=planosInfo[planoSelecionado]; var txid="STILLUS"+Date.now().toString().slice(-8); return gerarPixCopiaECola(info.valor, txid);}
var pixAtualCodigo = "";
function selecionarPlano(p){planoSelecionado=p; document.getElementById('cardBasico').classList.remove('selecionado'); document.getElementById('cardPro').classList.remove('selecionado'); document.getElementById('cardVitalicio').classList.remove('selecionado'); if(p==='basico') document.getElementById('cardBasico').classList.add('selecionado'); if(p==='pro') document.getElementById('cardPro').classList.add('selecionado'); if(p==='vitalicio') document.getElementById('cardVitalicio').classList.add('selecionado'); var info=planosInfo[p]; document.getElementById('btnPagarPlano').innerText="💳 PAGAR COM PIX - PLANO "+info.nome+" - "+info.label; document.getElementById('areaPagamento').style.display='none';}
function mostrarPagamento(){var info=planosInfo[planoSelecionado]; pixAtualCodigo = pixAtual(); document.getElementById('tituloPagamento').innerText="Pagamento - Plano "+info.nome+" - "+info.label; document.getElementById('imgQR').src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data="+encodeURIComponent(pixAtualCodigo); document.getElementById('areaPagamento').style.display='block'; document.getElementById('areaPagamento').scrollIntoView({behavior:'smooth'});}
function copiarPix(){if(!pixAtualCodigo) pixAtualCodigo=pixAtual(); navigator.clipboard.writeText(pixAtualCodigo).then(function(){alert('Código Pix copiado! ✅\n\nAgora abra o app do seu banco, escolha Pix Copia e Cola e cole o código.');});}
function enviarComprovanteWhats(){var info=planosInfo[planoSelecionado]; var msg="Olá! Acabei de pagar o StillusCalc PRO - Plano "+info.nome+" - "+info.label+" - Loja: "+(loja?loja.nome:"")+". Segue meu comprovante! Quero meu código de liberação."; window.open("https://wa.me/"+WHATS_DONO+"?text="+encodeURIComponent(msg),'_blank');}
function getLicenca(){try{return JSON.parse(localStorage.getItem('stilluscalc_licenca')||'null');}catch(e){return null;}}
function salvarLicenca(l){try{localStorage.setItem('stilluscalc_licenca', JSON.stringify(l));}catch(e){}}
function getDataInstalacao(){var d=localStorage.getItem('stilluscalc_instalacao'); if(!d){d=new Date().toISOString(); try{localStorage.setItem('stilluscalc_instalacao', d);}catch(e){}} return new Date(d);}
function diasRestantesTeste(){var inst=getDataInstalacao(); var agora=new Date(); var diff=Math.floor((agora-inst)/(1000*60*60*24)); return Math.max(0, 7-diff);}
function estaLiberado(){var lic=getLicenca(); if(lic && lic.tipo==='vitalicio') return true; if(lic && lic.expira){if(new Date() < new Date(lic.expira)) return true;} if(diasRestantesTeste()>0) return true; return false;}
function atualizarStatusPlano(){var lic=getLicenca(); var box=document.getElementById('statusPlanoBox'); if(!box) return; var pill=document.getElementById('pillTeste'); if(lic && lic.tipo==='vitalicio'){box.innerHTML="💎 <b>PLANO VITALÍCIO ATIVO</b><br>Você tem acesso pra sempre!"; if(pill){pill.innerText="💎 VITALÍCIO"; pill.style.background="#EDE9FE"; pill.style.color="#6D28D9";} return;} if(lic && lic.expira && new Date() < new Date(lic.expira)){var dias=Math.ceil((new Date(lic.expira)-new Date())/(1000*60*60*24)); box.innerHTML="✅ <b>PLANO "+lic.plano.toUpperCase()+" ATIVO</b><br>Faltam "+dias+" dias. Vence em "+new Date(lic.expira).toLocaleDateString('pt-BR'); if(pill){pill.innerText="✅ "+lic.plano.toUpperCase()+" - "+dias+" dias"; pill.style.background="#DCFCE7"; pill.style.color="#15803D";} return;} var rest=diasRestantesTeste(); if(rest>0){box.innerHTML="🎁 <b>TESTE GRÁTIS - Faltam "+rest+" dias</b><br>Você está usando tudo liberado!"; if(pill){pill.innerText="🎁 TESTE GRÁTIS: "+rest+" dias"; pill.style.background="#DCFCE7"; pill.style.color="#15803D";}} else {box.innerHTML="🔒 <b>SEU TESTE ACABOU!</b><br>Escolha um plano abaixo para continuar."; if(pill){pill.innerText="🔒 TESTE ACABOU - ASSINAR"; pill.style.background="#FEE2E2"; pill.style.color="#B91C1C";}}}
function validarCodigo(){var cod=document.getElementById('codigoLiberacao').value.trim().toUpperCase(); var mapa={"BASICO-30-STILLUS":{plano:"basico", tipo:"mensal", dias:30}, "PRO-30-STILLUS":{plano:"pro", tipo:"mensal", dias:30}, "VITALICIO-STILLUS-PRO":{plano:"vitalicio", tipo:"vitalicio", dias:0}}; if(!mapa[cod]){alert('Código inválido!'); return;} var info=mapa[cod]; var lic={plano:info.plano, tipo:info.tipo, expira:""}; if(info.tipo==='mensal'){var exp=new Date(); exp.setDate(exp.getDate()+info.dias); lic.expira=exp.toISOString();} salvarLicenca(lic); atualizarStatusPlano(); alert('LIBERADO! ✅ Plano '+info.plano.toUpperCase()+' ativado!'); fecharModal('modalPlanos');}
var deferredPrompt=null;
window.addEventListener('beforeinstallprompt',function(e){e.preventDefault(); deferredPrompt=e; var b=document.getElementById('btnInstalar'); if(b) b.style.display='block';});
function instalarApp(){if(deferredPrompt){deferredPrompt.prompt(); deferredPrompt.userChoice.then(function(){deferredPrompt=null;});} else {alert('Para instalar: No Chrome, 3 pontinhos > Adicionar à tela inicial / Instalar app. No iPhone: Compartilhar > Adicionar à Tela de Início');}}
function esc(s){return String(s==null?'':s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');}
function fmt(v){return (Number(v)||0).toLocaleString('pt-BR',{style:'currency',currency:'BRL'});}
function limparTexto(s,max){return String(s||'').replace(/<[^>]*>/g,'').trim().slice(0,max||200);}
function abrirMenu(){document.getElementById('sidebar').classList.add('aberta'); document.getElementById('overlay').classList.add('mostrar');}
function fecharMenu(){document.getElementById('sidebar').classList.remove('aberta'); document.getElementById('overlay').classList.remove('mostrar');}
function irPara(dest,btn){fecharMenu(); if(dest==='visao'){window.scrollTo({top:0,behavior:'smooth'}); var tabs=document.querySelectorAll('.side-item'); tabs.forEach(function(t){t.classList.remove('ativo')}); if(btn) btn.classList.add('ativo'); return;} if(dest==='vend'){verificarTravaEAbrir('modalVend',btn);}}
function abrirModal(id,btn){var m=document.getElementById(id); if(!m) return; m.classList.add('aberto'); fecharMenu(); if(id==='modalRel') renderRelatorio(); if(id==='modalRank') renderRanking(); if(id==='modalGrafico') renderGrafico(); if(id==='modalSync') atualizarStatusSync(); if(id==='modalCaixa') renderCaixa(); if(id==='modalChat'){renderClientes(); renderChat();} if(id==='modalRobo') renderRobo(); if(id==='modalEnviarProduto') renderProdutosChat(); if(id==='modalPlanos'){atualizarStatusPlano();} if(id==='modalVendEquipe'){renderVendedores(); renderListaLogins();} if(id==='modalLoja'){var c=document.getElementById('cfgCodigoLoja'); if(c) c.value=loja.codigoLoja;} if(btn){var tabs=document.querySelectorAll('.side-item'); tabs.forEach(function(t){t.classList.remove('ativo')}); if(btn.classList && btn.classList.contains('side-item')) btn.classList.add('ativo');}}
function fecharModal(id){var m=document.getElementById(id); if(m) m.classList.remove('aberto');}
function mesAtualStr(){var d=new Date(); return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0');}
function nomeMesAtual(){var d=new Date(); return d.toLocaleDateString('pt-BR',{month:'long',year:'numeric'});}
function limparNumeroWhats(s){return String(s||'').replace(/\D/g,'');}
function abrirWhatsComTexto(texto, numeroDestino){var num=limparNumeroWhats(numeroDestino||''); var url=''; if(num && num.length>=10){var n=num; if(n.length===11||n.length===10) n='55'+n; url='https://wa.me/'+n+'?text='+encodeURIComponent(texto);} else {url='https://wa.me/?text='+encodeURIComponent(texto);} if(navigator.share){navigator.share({text:texto}).then(function(){}).catch(function(){window.open(url,'_blank');});} else {window.open(url,'_blank');}}
var loja=null; try{loja=JSON.parse(localStorage.getItem('stilluscalc_loja')||'null');}catch(e){loja=null;}
if(!loja){loja={nome:'Minha Loja', whats:'', slogan:'O barato é aqui!', tipo:'Móveis e Eletrodomésticos', codigoLoja:'LOJA-'+Math.random().toString(36).slice(2,7).toUpperCase()};}
if(!loja.codigoLoja) loja.codigoLoja='LOJA-'+Math.random().toString(36).slice(2,7).toUpperCase();
var vendedores=[]; try{vendedores=JSON.parse(localStorage.getItem('stilluscalc_vendedores')||'[]');}catch(e){vendedores=[];}
if(!vendedores.length){vendedores=['Vendedor 1','Vendedor 2'];}
var loginsVendedores=[]; try{loginsVendedores=JSON.parse(localStorage.getItem('stilluscalc_logins')||'[]');}catch(e){loginsVendedores=[];}
if(!loginsVendedores.length){loginsVendedores=[{nome:'Maria Teste', login:'maria', senha:'1234', codigoLoja:'LOJA-TESTE'}];}
var vendedorAtual=''; try{vendedorAtual=localStorage.getItem('stilluscalc_vendedorAtual')||vendedores[0];}catch(e){vendedorAtual=vendedores[0];}
var usuarioLogado=null; try{usuarioLogado=JSON.parse(localStorage.getItem('stilluscalc_usuario')||'null');}catch(e){usuarioLogado=null;}
var itens=[]; try{itens=JSON.parse(localStorage.getItem('stilluscalc_itens')||'[]');}catch(e){itens=[];}
if(!itens.length){itens.push({nome:'Produto Exemplo - Sofá', codigo:'001', preco:1789, custo:1200, cat:'Produto Geral', foto:''});}
var historico=[]; try{historico=JSON.parse(localStorage.getItem('stilluscalc_hist')||'[]');}catch(e){historico=[];}
var metas=null; try{metas=JSON.parse(localStorage.getItem('stilluscalc_metas')||'null');}catch(e){metas=null;}
if(!metas){metas={dia:3000, vendidoDia:0, semana:15000, vendidoSemana:0, mes:60000, vendidoMes:0, mesRef:mesAtualStr()};}
if(!metas.mesRef) metas.mesRef=mesAtualStr();
var vendasHoje=[]; try{vendasHoje=JSON.parse(localStorage.getItem('stilluscalc_vendas')||'[]');}catch(e){vendasHoje=[];}
var relatorios=[]; try{relatorios=JSON.parse(localStorage.getItem('stilluscalc_relatorios')||'[]');}catch(e){relatorios=[];}
var clientes=[]; try{clientes=JSON.parse(localStorage.getItem('stilluscalc_clientes')||'[]');}catch(e){clientes=[];}
if(!clientes.length){clientes=[{nome:'Cliente Exemplo - João', msgs:[{tipo:'cliente', texto:'Oi, tem sofá em promoção?', hora:'08:00'}, {tipo:'eu', texto:'Tem sim! Olha esse aqui 👇', hora:'08:01'}]}];}
var clienteAtivo=0;
var caixa=[]; try{caixa=JSON.parse(localStorage.getItem('stilluscalc_caixa')||'[]');}catch(e){caixa=[];}
var roboLigado=false; try{roboLigado=localStorage.getItem('stilluscalc_robo')==='1';}catch(e){}
var roboRespostas=null; try{roboRespostas=JSON.parse(localStorage.getItem('stilluscalc_roboRespostas')||'null');}catch(e){roboRespostas=null;}
if(!roboRespostas){roboRespostas={oi:'Olá! Bem-vindo(a) a {LOJA}! 😊 Sou o assistente virtual. Como posso te ajudar hoje?', preco:'Esse produto está por {PRECO}! E hoje consigo um desconto especial só pra você! Quer que eu reserve?', desconto:'Consigo 10% de desconto só pra você hoje! 🔥 De {PRECO} por {PRECO_DESC} - quer que eu reserve?', entrega:'Sim! Fazemos entrega e montagem! 🚚 Me passa seu endereço que eu calculo na hora.', parcela:'Parcela sim! Em até 12x no cartão! 💳 Quer que eu simule?', estoque:'Tem sim em estoque! ✅ Quer que eu reserve pra você?'};}
var fotoTemp=''; var modoAtual='vend'; var expr='';
function salvar(){try{localStorage.setItem('stilluscalc_loja',JSON.stringify(loja)); localStorage.setItem('stilluscalc_vendedores',JSON.stringify(vendedores)); localStorage.setItem('stilluscalc_vendedorAtual',vendedorAtual); localStorage.setItem('stilluscalc_itens',JSON.stringify(itens)); localStorage.setItem('stilluscalc_hist',JSON.stringify(historico)); localStorage.setItem('stilluscalc_metas',JSON.stringify(metas)); localStorage.setItem('stilluscalc_vendas',JSON.stringify(vendasHoje)); localStorage.setItem('stilluscalc_relatorios',JSON.stringify(relatorios)); localStorage.setItem('stilluscalc_clientes',JSON.stringify(clientes)); localStorage.setItem('stilluscalc_caixa',JSON.stringify(caixa)); localStorage.setItem('stilluscalc_robo', roboLigado?'1':'0'); localStorage.setItem('stilluscalc_roboRespostas', JSON.stringify(roboRespostas)); localStorage.setItem('stilluscalc_logins', JSON.stringify(loginsVendedores)); if(usuarioLogado) localStorage.setItem('stilluscalc_usuario', JSON.stringify(usuarioLogado)); else localStorage.removeItem('stilluscalc_usuario');}catch(e){}}
function verificarTravaEAbrir(id, btn){if(!usuarioLogado){abrirModal('modalLogin'); return;} if(!estaLiberado()){abrirModal('modalPlanos'); return;} if(id==='modalVendEquipe' && usuarioLogado.tipo!=='dono'){alert('Só o DONO pode cadastrar vendedores!'); return;} if(id==='modalLoja' && usuarioLogado.tipo!=='dono'){alert('Só o DONO pode mudar dados da loja!'); return;} abrirModal(id, btn);}
function setAbaLogin(tipo){document.getElementById('abaDono').classList.toggle('ativo', tipo==='dono'); document.getElementById('abaVend').classList.toggle('ativo', tipo==='vend'); document.getElementById('boxLoginDono').style.display=tipo==='dono'?'block':'none'; document.getElementById('boxLoginVend').style.display=tipo==='vend'?'block':'none';}
function atualizarPillUsuario(){var el=document.getElementById('sideUsuario'); if(!el) return; if(!usuarioLogado){el.innerText='Não logado'; return;} if(usuarioLogado.tipo==='dono'){el.innerText='👑 DONO: '+usuarioLogado.nome+' | '+loja.codigoLoja;} else {el.innerText='👤 VENDEDOR: '+usuarioLogado.nome+' | '+usuarioLogado.codigoLoja;}}
function entrarComoDono(){var nome=limparTexto(document.getElementById('loginLojaNome').value,60); var whats=limparNumeroWhats(document.getElementById('loginDonoWhats').value); var codigo=document.getElementById('loginCodigoDono').value.trim().toUpperCase(); if(!nome){alert('Coloca o nome da sua loja, dono!'); return;} loja.nome=nome; if(whats) loja.whats=whats; if(codigo){var mapa={"BASICO-30-STILLUS":{plano:"basico", tipo:"mensal", dias:30}, "PRO-30-STILLUS":{plano:"pro", tipo:"mensal", dias:30}, "VITALICIO-STILLUS-PRO":{plano:"vitalicio", tipo:"vitalicio", dias:0}}; if(!mapa[codigo]){alert('Código inválido! Tenta de novo ou deixa em branco para usar o teste grátis.'); return;} var info=mapa[codigo]; var lic={plano:info.plano, tipo:info.tipo, expira:""}; if(info.tipo==='mensal'){var exp=new Date(); exp.setDate(exp.getDate()+info.dias); lic.expira=exp.toISOString();} salvarLicenca(lic);} usuarioLogado={tipo:'dono', nome:nome, codigoLoja:loja.codigoLoja}; vendedorAtual=nome; salvar(); atualizarPillUsuario(); renderLoja(); renderVendedores(); fecharModal('modalLogin'); alert('Bem-vindo, DONO! 👑\nLoja: '+loja.nome+'\nCódigo da loja: '+loja.codigoLoja);}
function entrarComoVendedor(){var codigo=document.getElementById('loginCodigoLoja').value.trim().toUpperCase(); var login=limparTexto(document.getElementById('loginVendLogin').value,30).toLowerCase(); var senha=document.getElementById('loginVendSenha').value.trim(); if(!codigo||!login||!senha){alert('Preenche Código da Loja, Login e Senha!'); return;} var ach=null; for(var i=0;i<loginsVendedores.length;i++){if(loginsVendedores[i].login.toLowerCase()===login && loginsVendedores[i].senha===senha){if(loginsVendedores[i].codigoLoja.toUpperCase()===codigo || codigo==='LOJA-TESTE'){ach=loginsVendedores[i]; break;}}} if(!ach){alert('Login ou senha errados, ou código da loja errado!'); return;} usuarioLogado={tipo:'vend', nome:ach.nome, login:ach.login, codigoLoja:codigo}; vendedorAtual=ach.nome; if(!vendedores.includes(ach.nome)) vendedores.push(ach.nome); salvar(); atualizarPillUsuario(); renderLoja(); renderVendedores(); fecharModal('modalLogin'); alert('Bem-vindo, '+ach.nome+'! 👤\nVocê entrou direto na calculadora.\nBoas vendas! 🛒');}
function entrarTesteVendedor(){document.getElementById('loginCodigoLoja').value='LOJA-TESTE'; document.getElementById('loginVendLogin').value='maria'; document.getElementById('loginVendSenha').value='1234'; entrarComoVendedor();}
function sairLogin(){if(!confirm('Sair e trocar de usuário?')) return; usuarioLogado=null; salvar(); atualizarPillUsuario(); abrirModal('modalLogin');}
function concluirBoasVindas(){var nomeLoja=limparTexto(document.getElementById('bvLoja').value,60); var whats=limparNumeroWhats(document.getElementById('bvWhats').value); var vendsStr=limparTexto(document.getElementById('bvVends').value,120); var metaMes=parseFloat(document.getElementById('bvMetaMes').value)||0; if(!nomeLoja){alert('Coloca o nome da sua loja!'); return;} loja.nome=nomeLoja; loja.whats=whats; if(metaMes>0) metas.mes=metaMes; if(vendsStr){var arr=vendsStr.split(','); var novos=[]; for(var i=0;i<arr.length;i++){var n=arr[i].trim(); if(n) novos.push(n);} if(novos.length){vendedores=novos; vendedorAtual=novos[0];}} try{localStorage.setItem('stilluscalc_jaViuBoasVindas','1');}catch(e){} usuarioLogado={tipo:'dono', nome:nomeLoja, codigoLoja:loja.codigoLoja}; salvar(); atualizarPillUsuario(); renderLoja(); renderVendedores(); renderMetas(); fecharModal('modalBoasVindas'); alert('Pronto! Seus 7 dias grátis começaram! 🎉');}
function addCliente(){var n=limparTexto(document.getElementById('novoClienteNome').value,50); if(!n){alert('Digite o nome do cliente!'); return;} clientes.push({nome:n, msgs:[{tipo:'eu', texto:'Olá '+n+'! Bem-vindo(a) a '+loja.nome+'! 😊 Como posso te ajudar?', hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}]}); document.getElementById('novoClienteNome').value=''; clienteAtivo=clientes.length-1; salvar(); renderClientes(); renderChat();}
function renderClientes(){var div=document.getElementById('listaClientes'); if(!div) return; div.innerHTML=''; if(!clientes.length) div.innerHTML='<p style="font-size:13px;padding:8px">Nenhum cliente ainda.</p>'; for(var i=0;i<clientes.length;i++){var c=clientes[i]; var last=c.msgs.length? c.msgs[c.msgs.length-1].texto:'...'; var letra=c.nome.charAt(0).toUpperCase(); div.innerHTML+='<div class="cliente-item" onclick="selecionarCliente('+i+')"><div class="av">'+esc(letra)+'</div><div style="flex:1;min-width:0"><b>'+esc(c.nome)+'</b><br><small style="color:#888">'+esc(last.slice(0,50))+'</small></div><span style="font-size:16px">💬</span></div>';}}
function selecionarCliente(i){clienteAtivo=i; renderChat(); renderClientes();}
function renderChat(){var c=clientes[clienteAtivo]; if(!c) return; document.getElementById('chatClienteNome').innerText=c.nome; document.getElementById('chatAvatar').innerText=c.nome.charAt(0).toUpperCase(); document.getElementById('chatClienteStatus').innerText='Vendedor: '+vendedorAtual+' | '+loja.nome; document.getElementById('chatRoboStatus').innerText=roboLigado?'Robo ON 🤖':'Robo OFF'; document.getElementById('btnRobo').innerText=roboLigado?'🤖 ROBO: LIGADO ✅':'🤖 ROBO: DESLIGADO'; var box=document.getElementById('chatBox'); box.innerHTML=''; for(var i=0;i<c.msgs.length;i++){var m=c.msgs[i]; var cls=m.tipo==='eu'?'eu':m.tipo==='robo'?'robo':'cliente'; var nome=m.tipo==='robo'?'🤖 Robo':m.tipo==='eu'?'Você':esc(c.nome); var midia=''; if(m.foto) midia+='<img src="'+esc(m.foto)+'">'; if(m.video) midia+='<video src="'+esc(m.video)+'" controls></video>'; var prod=''; if(m.produto){prod='<div class="prod-card">'+(m.produto.foto?'<img src="'+esc(m.produto.foto)+'">':'')+'<b>'+esc(m.produto.nome)+'</b><br>De <s>'+fmt(m.produto.preco)+'</s> por <b style="color:#22C55E">'+fmt(m.produto.preco*0.9)+'</b></div>';} box.innerHTML+='<div class="msg '+cls+'"><b style="font-size:11px">'+nome+'</b><br>'+esc(m.texto)+midia+prod+'<small>'+esc(m.hora||'')+'</small></div>';} box.scrollTop=box.scrollHeight;}
function toggleEmoji(){var p=document.getElementById('emojiPanel'); if(p.style.display==='none'){var emojis=['😀','😂','😍','👍','👏','🔥','💰','🛍️','🛋️','📱','🚚','💳','✅','❤️','😊','🎉','👋','🙏','💪','⭐','🏆','📦','🤑','😉']; p.innerHTML=''; for(var i=0;i<emojis.length;i++){p.innerHTML+='<span onclick="addEmoji(\''+emojis[i]+'\')">'+emojis[i]+'</span>';} p.style.display='flex';} else {p.style.display='none';}}
function addEmoji(e){document.getElementById('chatInput').value+=e; document.getElementById('chatInput').focus();}
function enviarMsgChat(){var inp=document.getElementById('chatInput'); var txt=limparTexto(inp.value,500); if(!txt) return; var c=clientes[clienteAtivo]; if(!c) return; c.msgs.push({tipo:'eu', texto:txt, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); inp.value=''; document.getElementById('emojiPanel').style.display='none'; salvar(); renderChat(); renderClientes();}
function enviarMidiaChat(input){var f=input.files[0]; if(!f) return; var c=clientes[clienteAtivo]; if(!c) return; var r=new FileReader(); r.onload=function(e){var isVideo=f.type.indexOf('video')>-1; var m={tipo:'eu', texto:isVideo?'🎥 Vídeo do produto!':'📸 Foto do produto!', hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}; if(isVideo) m.video=e.target.result; else m.foto=e.target.result; c.msgs.push(m); salvar(); renderChat();}; r.readAsDataURL(f);}
function renderProdutosChat(){var div=document.getElementById('listaProdutosChat'); div.innerHTML=''; for(var i=0;i<itens.length;i++){var it=itens[i]; div.innerHTML+='<div class="item-cad"><div class="ft">'+(it.foto?'<img src="'+esc(it.foto)+'">':'🛍️')+'</div><div class="info"><b>'+esc(it.nome)+'</b><br><b>'+fmt(it.preco)+'</b></div><button class="btn btn-verde" style="width:auto;padding:8px 12px" onclick="enviarProdutoChat('+i+')">ENVIAR NO CHAT</button></div>';}}
function enviarProdutoChat(idx){var it=itens[idx]; var c=clientes[clienteAtivo]; if(!c) return; c.msgs.push({tipo:'eu', texto:'Olha esse produto! 👇', produto:it, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat(); fecharModal('modalEnviarProduto'); abrirModal('modalChat');}
function simularCliente(){var c=clientes[clienteAtivo]; if(!c) return; var frases=['Oi, qual o preço desse sofá?','Tem desconto?','Você faz entrega?','Parcela no cartão?','Tem em estoque?']; var f=frases[Math.floor(Math.random()*frases.length)]; c.msgs.push({tipo:'cliente', texto:f, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat(); if(roboLigado){setTimeout(function(){respostaRobo(f);},800);}}
function respostaRobo(textoCliente){var c=clientes[clienteAtivo]; if(!c) return; var t=textoCliente.toLowerCase(); var resp=''; var ultimoPreco=itens.length? itens[0].preco:1789; if(t.indexOf('preço')>-1||t.indexOf('preco')>-1||t.indexOf('valor')>-1||t.indexOf('quanto')>-1){resp=roboRespostas.preco.replace('{PRECO}', fmt(ultimoPreco));} else if(t.indexOf('desconto')>-1){resp=roboRespostas.desconto.replace('{PRECO}', fmt(ultimoPreco)).replace('{PRECO_DESC}', fmt(ultimoPreco*0.9));} else if(t.indexOf('entrega')>-1||t.indexOf('frete')>-1){resp=roboRespostas.entrega;} else if(t.indexOf('parcela')>-1||t.indexOf('cartão')>-1||t.indexOf('cartao')>-1){resp=roboRespostas.parcela;} else if(t.indexOf('tem')>-1||t.indexOf('estoque')>-1){resp=roboRespostas.estoque;} else if(t.indexOf('oi')>-1||t.indexOf('olá')>-1||t.indexOf('ola')>-1||t.indexOf('bom dia')>-1){resp=roboRespostas.oi.replace('{LOJA}', loja.nome);} else {resp='Entendi! Um vendedor vai te atender agora! 😊';} c.msgs.push({tipo:'robo', texto:resp, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat();}
function toggleRobo(){roboLigado=!roboLigado; salvar(); renderChat(); alert(roboLigado?'Robo LIGADO! 🤖':'Robo DESLIGADO.');}
function renderRobo(){document.getElementById('roboOi').value=roboRespostas.oi; document.getElementById('roboPreco').value=roboRespostas.preco; document.getElementById('roboDesconto').value=roboRespostas.desconto; document.getElementById('roboEntrega').value=roboRespostas.entrega; document.getElementById('roboParcela').value=roboRespostas.parcela; document.getElementById('roboEstoque').value=roboRespostas.estoque;}
function salvarRobo(){roboRespostas.oi=document.getElementById('roboOi').value; roboRespostas.preco=document.getElementById('roboPreco').value; roboRespostas.desconto=document.getElementById('roboDesconto').value; roboRespostas.entrega=document.getElementById('roboEntrega').value; roboRespostas.parcela=document.getElementById('roboParcela').value; roboRespostas.estoque=document.getElementById('roboEstoque').value; salvar(); fecharModal('modalRobo'); alert('Robô salvo!');}
function comecarVendaNoChat(){var c=clientes[clienteAtivo]; if(!c) return; document.getElementById('vCliente').value=c.nome; var nomeProd=itens.length? itens[0].nome+' ('+itens[0].codigo+')':''; document.getElementById('vNome').value=nomeProd; if(itens.length){document.getElementById('vCodigo').value=itens[0].codigo; document.getElementById('vPreco').value=itens[0].preco; document.getElementById('vCusto').value=itens[0].custo;} calcularVendedor(); c.msgs.push({tipo:'eu', texto:'Perfeito! Já estou preparando sua venda! 🛒 Vou mandar pro caixa!', hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat(); fecharModal('modalChat'); abrirModal('modalVend');}
function enviarChatWhatsApp(){var c=clientes[clienteAtivo]; if(!c) return; var msg='Conversa '+loja.nome+' - Cliente: '+c.nome+'\n\n'; for(var i=0;i<c.msgs.length;i++){var m=c.msgs[i]; var quem=m.tipo==='eu'?'Vendedor':m.tipo==='robo'?'Robo':c.nome; msg+=quem+': '+m.texto+'\n';} abrirWhatsComTexto(msg, loja.whats);}
function enviarProCaixa(){var nome=document.getElementById('vNome').value||'Produto'; var preco=parseFloat(document.getElementById('vPreco').value); var desc=parseFloat(document.getElementById('vDesc').value)||0; var frete=parseFloat(document.getElementById('vFrete').value)||0; var vend=document.getElementById('vVendedor').value||vendedorAtual; var cliente=document.getElementById('vCliente').value||'Cliente Balcão'; if(!preco){alert('Selecione um item!'); return;} var final=preco*(1-desc/100)+frete; var item={id:Date.now(), nome:nome, valor:final, vendedor:vend, cliente:cliente, data:new Date().toLocaleString('pt-BR'), status:'aguardando', formaPagamento:''}; caixa.push(item); salvar(); renderCaixa(); fecharModal('modalVend'); abrirModal('modalCaixa'); alert('Enviado pro CAIXA! 🧾\n'+nome+' - '+fmt(final)+'\nCliente: '+cliente); }
function renderCaixa(){var pend=caixa.filter(function(x){return x.status==='aguardando';}); var fin=caixa.filter(function(x){return x.status==='finalizado';}); var totalPend=pend.reduce(function(s,x){return s+x.valor;},0); var totalFin=fin.reduce(function(s,x){return s+x.valor;},0); document.getElementById('resumoCaixa').innerHTML='🧾 CAIXA - '+esc(loja.nome)+'<br>Aguardando: <b>'+pend.length+' - '+fmt(totalPend)+'</b> | Finalizados: <b>'+fin.length+' - '+fmt(totalFin)+'</b>'; var div=document.getElementById('listaCaixa'); div.innerHTML=''; if(!pend.length) div.innerHTML='<p style="font-size:13px">Nenhuma venda aguardando.</p>'; for(var i=0;i<pend.length;i++){var it=pend[i]; div.innerHTML+='<div class="caixa-item aguardando"><b>🛒 '+esc(it.nome)+'</b><br>Cliente: <b>'+esc(it.cliente)+'</b> | Vendedor: <b>'+esc(it.vendedor)+'</b><br>Valor: <b style="font-size:18px">'+fmt(it.valor)+'</b><br><label style="margin-top:6px">Forma de pagamento:</label><select id="pag-'+it.id+'"><option>Pix</option><option>Dinheiro</option><option>Cartão Crédito</option><option>Cartão Débito</option><option>Boleto</option></select><div class="flex2"><button class="btn btn-verde" onclick="finalizarCaixa('+it.id+')">✅ FINALIZAR / RECEBER</button><button class="btn btn-vermelho" onclick="cancelarCaixa('+it.id+')">❌ CANCELAR</button></div></div>';} var div2=document.getElementById('listaCaixaFinalizados'); div2.innerHTML=''; for(var j=0;j<fin.slice().reverse().length;j++){var f=fin.slice().reverse()[j]; div2.innerHTML+='<div class="caixa-item finalizado">✅ <b>'+esc(f.nome)+'</b> - '+fmt(f.valor)+'<br><small>'+esc(f.cliente)+' | '+esc(f.vendedor)+' | '+esc(f.formaPagamento)+'</small></div>';} if(!fin.length) div2.innerHTML='<p style="font-size:13px">Nenhuma venda finalizada ainda.</p>';}
function finalizarCaixa(id){var idx=-1; for(var i=0;i<caixa.length;i++){if(caixa[i].id===id){idx=i;break;}} if(idx<0) return; var it=caixa[idx]; var forma=document.getElementById('pag-'+id).value; if(!confirm('Finalizar venda de '+it.nome+' por '+fmt(it.valor)+'?\nCliente: '+it.cliente+'\nPagamento: '+forma)) return; it.status='finalizado'; it.formaPagamento=forma; registrarVendaAutomatica(it.nome, it.valor, it.vendedor); salvar(); renderCaixa(); alert('Venda FINALIZADA! ✅\n'+fmt(it.valor)+' via '+forma); }
function cancelarCaixa(id){if(!confirm('Cancelar essa venda?')) return; for(var i=0;i<caixa.length;i++){if(caixa[i].id===id){caixa[i].status='cancelado'; break;}} salvar(); renderCaixa();}
function atualizarStatusSync(){document.getElementById('codigoLoja').value=loja.codigoLoja+' - '+loja.nome; var el=document.getElementById('boxCodigoLojaVendedor'); if(el){el.innerHTML='<b>Passe para seus vendedores:</b><br>Código da Loja: <b>'+esc(loja.codigoLoja)+'</b><br>Link: <b>https://'+location.host+'/'+'</b><br>Cada vendedor entra com o login e senha que você cadastrou.';} var total=vendasHoje.length; var val=vendasHoje.reduce(function(s,v){return s+(v.valor||0);},0); document.getElementById('statusSync').innerText='Loja: '+loja.nome+' | Vendas: '+total+' - '+fmt(val);}
function gerarLinkLoja(){var dados={loja:loja, vendedores:vendedores, itens:itens, metas:metas, logins:loginsVendedores}; var codigo=btoa(unescape(encodeURIComponent(JSON.stringify(dados)))); var base=location.href.split('?')[0].split('#')[0]; var link=base+'?loja='+encodeURIComponent(codigo); document.getElementById('codigoLoja').value=link; navigator.clipboard.writeText(link).then(function(){alert('Link copiado!');}); return link;}
function copiarLinkLoja(){var l=gerarLinkLoja(); navigator.clipboard.writeText(l);}
function enviarLinkLojaWhats(){var l=gerarLinkLoja(); var msg='Olá! Entra na nossa loja no StillusCalc PRO 🏪 '+loja.nome+'\n\nCódigo da Loja: '+loja.codigoLoja+'\nClica no link:\n'+l; abrirWhatsComTexto(msg, loja.whats);}
function tentarEntrarViaLink(){var params=new URLSearchParams(location.search); var cod=params.get('loja'); if(!cod) return; try{var dados=JSON.parse(decodeURIComponent(escape(atob(cod)))); if(dados.loja && confirm('Entrar na loja '+dados.loja.nome+'?')){loja=dados.loja; vendedores=dados.vendedores||vendedores; itens=dados.itens||itens; if(dados.metas) metas=dados.metas; if(dados.logins) loginsVendedores=dados.logins; vendedorAtual=vendedores[0]; try{localStorage.setItem('stilluscalc_jaViuBoasVindas','1');}catch(e){} salvar(); renderLoja(); renderVendedores(); renderItens(); renderMetas(); alert('Você entrou na loja '+loja.nome+'! Agora faça login com seu login e senha.');}}catch(e){}}
function gerarCodigoVendas(){var minhas=vendasHoje.filter(function(v){return v.vendedor===vendedorAtual;}); var payload={tipo:'STILLUS_VENDAS', loja:loja.codigoLoja, lojaNome:loja.nome, vendedor:vendedorAtual, vendas:minhas, data:new Date().toLocaleString('pt-BR')}; return 'STILLUS-'+btoa(unescape(encodeURIComponent(JSON.stringify(payload))));}
function enviarVendasWhats(){var codigo=gerarCodigoVendas(); var minhas=vendasHoje.filter(function(v){return v.vendedor===vendedorAtual;}); var total=minhas.reduce(function(s,v){return s+(v.valor||0);},0); var msg='🔄 SINCRONIZAÇÃO StillusCalc PRO - '+loja.nome+'\nVendedor: '+vendedorAtual+'\nVendas: '+minhas.length+' - Total: '+fmt(total)+'\n\nCole esse código no app do dono:\n\n'+codigo; abrirWhatsComTexto(msg, loja.whats);}
function receberVendas(){var txt=document.getElementById('codigoReceber').value.trim(); if(!txt){alert('Cole o código!'); return;} try{var codigo=txt.replace('STILLUS-','').trim(); var payload=JSON.parse(decodeURIComponent(escape(atob(codigo)))); if(payload.tipo!=='STILLUS_VENDAS'){alert('Código inválido!'); return;} var novas=0; for(var i=0;i<payload.vendas.length;i++){var v=payload.vendas[i]; var ja=false; for(var j=0;j<vendasHoje.length;j++){if(vendasHoje[j].nome===v.nome && vendasHoje[j].valor===v.valor && vendasHoje[j].data===v.data && vendasHoje[j].vendedor===v.vendedor){ja=true;break;}} if(!ja){vendasHoje.push(v); metas.vendidoDia+=v.valor; metas.vendidoSemana+=v.valor; metas.vendidoMes+=v.valor; novas++;}} if(!vendedores.includes(payload.vendedor)) vendedores.push(payload.vendedor); salvar(); renderMetas(); renderRanking(); renderGrafico(); document.getElementById('codigoReceber').value=''; alert('Recebido! '+novas+' vendas novas'); abrirModal('modalGrafico'); }catch(e){alert('Não consegui ler esse código!');}}
function calcRanking(){var map={}; for(var i=0;i<vendedores.length;i++){map[vendedores[i]]={nome:vendedores[i], total:0, qtd:0};} for(var j=0;j<vendasHoje.length;j++){var v=vendasHoje[j]; if(!map[v.vendedor]) map[v.vendedor]={nome:v.vendedor,total:0,qtd:0}; map[v.vendedor].total+=v.valor; map[v.vendedor].qtd+=1;} var arr=[]; for(var k in map) arr.push(map[k]); arr.sort(function(a,b){return b.total-a.total;}); return arr;}
function renderGrafico(){var arr=calcRanking(); var total=arr.reduce(function(s,r){return s+r.total;},0); var media=arr.length? total/arr.length:0; var top=arr.length? arr[0].nome:'--'; document.getElementById('resumoGrafico').innerHTML='🏪 <b>'+esc(loja.nome)+'</b><br>Total: <b>'+fmt(total)+'</b> | Média: <b>'+fmt(media)+'</b><br>Top: <b>🏆 '+esc(top)+'</b>'; var max=arr.length? arr[0].total:1; var cores=['#FACC15','#22C55E','#3B82F6','#7C3AED','#F97316','#EF4444']; var div=document.getElementById('graficoBarras'); div.innerHTML=''; for(var i=0;i<arr.length;i++){var r=arr[i]; var h=max? Math.max(18, Math.round(r.total/max*150)):18; div.innerHTML+='<div class="graf-col"><div class="barra" style="height:'+h+'px;background:'+cores[i%cores.length]+'">'+Math.round(r.total/max*100)+'%</div><b>'+fmt(r.total)+'</b><span>'+esc(r.nome)+'</span><small>'+r.qtd+' vendas</small></div>';} if(!vendasHoje.length) div.innerHTML='<p style="font-size:13px">Nenhuma venda ainda.</p>'; var lista=document.getElementById('listaGrafico'); lista.innerHTML=''; for(var j=0;j<arr.length;j++){var rr=arr[j]; var perc=total? Math.round(rr.total/total*100):0; lista.innerHTML+='<div class="rank-item'+(j===0?' top1':'')+'"><div style="font-size:20px">'+(j===0?'🥇':j===1?'🥈':j===2?'🥉':'🏅')+'</div><div style="flex:1;min-width:0"><b>'+esc(rr.nome)+'</b><br><small>'+rr.qtd+' vendas - '+perc+'%</small><div class="barra-meta"><div style="width:'+perc+'%">'+perc+'%</div></div></div><b>'+fmt(rr.total)+'</b></div>';}}
function enviarGraficoWhats(){var arr=calcRanking(); var total=arr.reduce(function(s,r){return s+r.total;},0); var msg='📊 GRÁFICO - '+loja.nome+'\nTotal: '+fmt(total)+'\n\n'; for(var i=0;i<arr.length;i++){msg+=(i+1)+'º '+arr[i].nome+' - '+fmt(arr[i].total)+' ('+arr[i].qtd+' vendas)\n';} abrirWhatsComTexto(msg, loja.whats);}
function exportarBackup(){var dados={}; dados.app='StillusCalc PRO'; dados.loja=loja; dados.vendedores=vendedores; dados.logins=loginsVendedores; dados.itens=itens; dados.metas=metas; dados.vendasHoje=vendasHoje; dados.clientes=clientes; dados.caixa=caixa; var blob=new Blob([JSON.stringify(dados,null,2)],{type:'application/json'}); var a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='backup-stilluscalc-'+mesAtualStr()+'.json'; a.click(); alert('Backup baixado!');}
function importarBackup(input){var f=input.files[0]; if(!f) return; var r=new FileReader(); r.onload=function(e){try{var d=JSON.parse(e.target.result); if(!d.loja){alert('Backup inválido!'); return;} loja=d.loja; vendedores=d.vendedores||vendedores; itens=d.itens||[]; metas=d.metas||metas; vendasHoje=d.vendasHoje||[]; clientes=d.clientes||clientes; caixa=d.caixa||caixa; if(d.logins) loginsVendedores=d.logins; salvar(); renderLoja(); renderVendedores(); renderItens(); renderMetas(); alert('Backup restaurado!'); }catch(err){alert('Não consegui ler!');}}; r.readAsText(f);}
function apagarTudo(){if(!confirm('APAGAR TUDO?')) return; if(!confirm('Última chance!')) return; localStorage.clear(); location.reload();}
function renderLoja(){
document.getElementById('nomeLojaTopo').innerText=loja.nome;
document.getElementById('sloganTopo').innerText=loja.slogan;
document.getElementById('sideLojaNome').innerText=loja.nome+' - '+loja.slogan;
document.getElementById('cfgLoja').value=loja.nome; document.getElementById('cfgWhats').value=loja.whats; document.getElementById('cfgSlogan').value=loja.slogan; document.getElementById('cfgTipo').value=loja.tipo;
var cc=document.getElementById('cfgCodigoLoja'); if(cc) cc.value=loja.codigoLoja;
var ce=document.getElementById('codigoLojaEquipe'); if(ce) ce.innerText=loja.codigoLoja;
document.getElementById('vendedorAtualTopo').innerText=vendedorAtual;
var el=document.getElementById('vendendoComoItens'); if(el) el.innerText=vendedorAtual;
var sel=document.getElementById('vVendedor'); sel.innerHTML=''; for(var i=0;i<vendedores.length;i++){sel.innerHTML+='<option>'+esc(vendedores[i])+'</option>';} sel.value=vendedorAtual;
document.getElementById('dataHoje').innerText=new Date().toLocaleDateString('pt-BR',{day:'2-digit',month:'long',year:'numeric'});
atualizarPillUsuario();}
function salvarLoja(){if(usuarioLogado && usuarioLogado.tipo!=='dono'){alert('Só o DONO pode mudar dados da loja!'); return;} var nome=limparTexto(document.getElementById('cfgLoja').value,60); if(!nome){alert('Coloque o nome da loja!'); return;} loja.nome=nome; loja.whats=limparNumeroWhats(document.getElementById('cfgWhats').value); loja.slogan=limparTexto(document.getElementById('cfgSlogan').value,80)||'O barato é aqui!'; loja.tipo=document.getElementById('cfgTipo').value; salvar(); renderLoja(); fecharModal('modalLoja');}
function addVendedor(){if(usuarioLogado && usuarioLogado.tipo!=='dono'){alert('Só o DONO pode cadastrar vendedores!'); return;} var n=limparTexto(document.getElementById('novoVendNome').value,40); var login=limparTexto(document.getElementById('novoVendLogin').value,30).toLowerCase().replace(/\s/g,''); var senha=document.getElementById('novoVendSenha').value.trim(); if(!n||!login||!senha){alert('Preenche Nome, Login e Senha!'); return;} for(var i=0;i<loginsVendedores.length;i++){if(loginsVendedores[i].login.toLowerCase()===login){alert('Esse login já existe! Usa outro.'); return;}} vendedores.push(n); loginsVendedores.push({nome:n, login:login, senha:senha, codigoLoja:loja.codigoLoja}); vendedorAtual=n; document.getElementById('novoVendNome').value=''; document.getElementById('novoVendLogin').value=''; document.getElementById('novoVendSenha').value=''; salvar(); renderVendedores(); renderListaLogins(); renderLoja(); alert('Vendedor cadastrado! ✅\n\nNome: '+n+'\nCódigo da Loja: '+loja.codigoLoja+'\nLogin: '+login+'\nSenha: '+senha);}
function renderListaLogins(){var div=document.getElementById('listaLoginsVendedores'); if(!div) return; div.innerHTML='<b>Logins cadastrados:</b>'; for(var i=0;i<loginsVendedores.length;i++){var l=loginsVendedores[i]; div.innerHTML+='<div style="background:#F8FAFC;border:1px solid #E2E8F0;border-radius:10px;padding:8px;margin-top:6px;font-size:12px;line-height:1.6"><b>'+esc(l.nome)+'</b><br>Código: <b>'+esc(l.codigoLoja)+'</b> | Login: <b>'+esc(l.login)+'</b> | Senha: <b>'+esc(l.senha)+'</b> <button class="btn btn-vermelho" style="width:auto;padding:4px 10px;margin-top:4px" onclick="removerVendedor('+i+')">REMOVER</button></div>';}}
function removerVendedor(idx){if(!confirm('Remover esse vendedor?')) return; var nome=loginsVendedores[idx].nome; loginsVendedores.splice(idx,1); var vi=vendedores.indexOf(nome); if(vi>-1) vendedores.splice(vi,1); salvar(); renderVendedores(); renderListaLogins();}
function copiarDadosVendedores(){var txt='🏪 '+loja.nome+' - StillusCalc PRO\n\nPara entrar, usa:\nCódigo da Loja: '+loja.codigoLoja+'\nLink: https://'+location.host+'/\n\nSeus logins:\n'; for(var i=0;i<loginsVendedores.length;i++){txt+=loginsVendedores[i].nome+' - Login: '+loginsVendedores[i].login+' - Senha: '+loginsVendedores[i].senha+'\n';} navigator.clipboard.writeText(txt).then(function(){alert('Dados copiados! Cola no WhatsApp e manda pros vendedores.');});}
function renderVendedores(){var div=document.getElementById('listaVendedoresModal'); if(div){div.innerHTML=''; for(var i=0;i<vendedores.length;i++){var at=vendedores[i]===vendedorAtual?' ativo':''; div.innerHTML+='<span class="chip-vend'+at+'" onclick="trocarVendedor(\''+esc(vendedores[i])+'\')">'+esc(vendedores[i])+'</span>';}} var topo=document.getElementById('listaVendedoresTopo'); if(topo){topo.innerHTML=''; for(var j=0;j<vendedores.length;j++){var at2=vendedores[j]===vendedorAtual?' ativo':''; topo.innerHTML+='<span class="chip-vend'+at2+'" onclick="trocarVendedor(\''+esc(vendedores[j])+'\')">'+esc(vendedores[j])+'</span>';}} var ce=document.getElementById('codigoLojaEquipe'); if(ce) ce.innerText=loja.codigoLoja; renderListaLogins();}
function trocarVendedor(nome){if(usuarioLogado && usuarioLogado.tipo==='vend' && usuarioLogado.nome!==nome){alert('Você está logado como '+usuarioLogado.nome+' e não pode trocar de vendedor!'); return;} vendedorAtual=nome; salvar(); renderVendedores(); renderLoja(); renderRanking();}
function aplicarFundo(){var f=localStorage.getItem('stilluscalc_fundo')||''; if(f){document.body.style.backgroundImage='url('+f+')'; var img=document.getElementById('prevFundo'); if(img){img.src=f; img.style.display='block';}}}
aplicarFundo();
function salvarFundo(input){var f=input.files[0]; if(!f) return; var r=new FileReader(); r.onload=function(e){try{localStorage.setItem('stilluscalc_fundo',e.target.result);}catch(err){alert('Foto muito grande!'); return;} aplicarFundo();}; r.readAsDataURL(f);}
function removerFundo(){localStorage.removeItem('stilluscalc_fundo'); document.body.style.backgroundImage=''; document.getElementById('prevFundo').style.display='none';}
function preverFotoItem(input){var f=input.files[0]; if(!f) return; var r=new FileReader(); r.onload=function(e){fotoTemp=e.target.result; document.getElementById('prevItem').src=e.target.result; document.getElementById('prevItem').style.display='block';}; r.readAsDataURL(f);}
function cadastrarItem(){var nome=limparTexto(document.getElementById('nNome').value,80); var codigo=limparTexto(document.getElementById('nCodigo').value,20).toUpperCase(); var preco=parseFloat(document.getElementById('nPreco').value); var custo=parseFloat(document.getElementById('nCusto').value)||0; if(!nome||!codigo||!preco){alert('Preencha Nome, Código e Preço!'); return;} for(var i=0;i<itens.length;i++){if(itens[i].codigo===codigo){alert('Código já existe!'); return;}} var item={}; item.nome=nome; item.codigo=codigo; item.preco=preco; item.custo=custo; item.cat=document.getElementById('nCat').value; item.foto=fotoTemp; itens.push(item); fotoTemp=''; document.getElementById('nNome').value=''; document.getElementById('nCodigo').value=''; document.getElementById('nPreco').value=''; document.getElementById('nCusto').value=''; document.getElementById('prevItem').style.display='none'; salvar(); renderItens(); fecharModal('modalCad'); abrirModal('modalItens');}
function renderItens(){var busca=limparTexto(document.getElementById('buscaItem').value,80).toLowerCase(); var div=document.getElementById('listaItens'); div.innerHTML=''; var lista=[]; for(var i=0;i<itens.length;i++){if(itens[i].nome.toLowerCase().indexOf(busca)>-1||itens[i].codigo.toLowerCase().indexOf(busca)>-1) lista.push(itens[i]);} for(var j=0;j<lista.length;j++){var it=lista[j]; var idx=itens.indexOf(it); var ft=it.foto? '<img src="'+esc(it.foto)+'">' : '🛍️'; div.innerHTML+='<div class="item-cad"><div class="ft">'+ft+'</div><div class="info"><b>'+esc(it.nome)+'</b><br><small>'+esc(it.codigo)+' - '+esc(it.cat)+'</small><br><b>'+fmt(it.preco)+'</b></div><div style="display:flex;flex-direction:column;gap:4px;flex-shrink:0"><button class="btn btn-verde" style="width:auto;padding:8px 12px;margin:0" onclick="venderPorItem('+idx+')">VENDER</button><button class="btn btn-azul" style="width:auto;padding:6px 10px;margin:0" onclick="selecionarItem('+idx+')">CALCULAR</button><button class="btn btn-vermelho" style="width:auto;padding:6px 10px;margin:0" onclick="excluirItem('+idx+')">X</button></div></div>';} if(!lista.length) div.innerHTML='<p style="font-size:13px">Nenhum item.</p>'; var fav=document.getElementById('favoritosBox'); fav.innerHTML='<b>Rápido:</b><br>'; for(var k=0;k<Math.min(itens.length,5);k++){fav.innerHTML+='<span class="chip" onclick="venderPorItem('+k+')">🛒 '+esc(itens[k].nome)+' - '+fmt(itens[k].preco)+'</span>';} renderHist(); renderMetas();}
function excluirItem(idx){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('Só o DONO pode apagar itens!'); return;} if(confirm('Apagar esse item?')){itens.splice(idx,1); salvar(); renderItens();}}
function selecionarItem(idx){var it=itens[idx]; document.getElementById('vNome').value=it.nome+' ('+it.codigo+')'; document.getElementById('vCodigo').value=it.codigo; document.getElementById('vPreco').value=it.preco; document.getElementById('vCusto').value=it.custo; calcularVendedor(); fecharModal('modalItens'); abrirModal('modalVend');}
function puxarItem(){var cod=limparTexto(document.getElementById('vCodigo').value,20).toUpperCase(); if(!cod){alert('Digite o código!'); return;} var ach=null; for(var i=0;i<itens.length;i++){if(itens[i].codigo===cod){ach=itens[i];break;}} if(!ach){alert('Código não encontrado!'); return;} document.getElementById('vNome').value=ach.nome+' ('+ach.codigo+')'; document.getElementById('vPreco').value=ach.preco; document.getElementById('vCusto').value=ach.custo; calcularVendedor();}
function setModo(m){modoAtual=m; document.getElementById('btnModoVend').classList.toggle('ativo',m==='vend'); document.getElementById('btnModoCli').classList.toggle('ativo',m==='cli'); calcularVendedor();}
function setDesc(v){document.getElementById('vDesc').value=v; document.getElementById('vDescLabel').innerText=v+'%'; calcularVendedor();}
function calcularVendedor(){var preco=parseFloat(document.getElementById('vPreco').value); var custo=parseFloat(document.getElementById('vCusto').value)||0; var desc=parseFloat(document.getElementById('vDesc').value)||0; var comPerc=parseFloat(document.getElementById('vComissao').value)||3; var entrada=parseFloat(document.getElementById('vEntrada').value)||0; var frete=parseFloat(document.getElementById('vFrete').value)||0; var div=document.getElementById('resultadoVend'); if(!preco){div.innerHTML='Selecione um item!'; return;} var comDesc=preco*(1-desc/100); var totalFinal=comDesc+frete; var lucro=totalFinal-custo-frete; var margem=totalFinal?(lucro/totalFinal*100):0; var comissao=totalFinal*comPerc/100; var maxDesc=preco? Math.max(0,(preco-custo)/preco*100):0; var status=''; var classe=''; if(lucro<0){status='NÃO DÊ ESSE DESCONTO! PREJUÍZO!'; classe='perigo';} else if(margem<10){status='ATENÇÃO! Margem baixa!'; classe='atencao';} else {status='PODE DAR ESSE DESCONTO!'; classe='';} div.className='resultado '+classe; if(modoAtual==='cli'){div.innerHTML='<b>'+esc(document.getElementById('vNome').value||'Produto')+'</b><br>De <s>'+fmt(preco)+'</s> por <b style="font-size:20px">'+fmt(comDesc)+'</b>';} else {if(usuarioLogado && usuarioLogado.tipo==='vend'){div.innerHTML='<b>'+status+'</b><br>Preço: <b>'+fmt(preco)+'</b> | Com '+desc+'% OFF: <b>'+fmt(comDesc)+'</b><br>Total: <b>'+fmt(totalFinal)+'</b><br><small>Custo e lucro só o dono vê.</small>';} else {div.innerHTML='<b>'+status+'</b><br>Preço: <b>'+fmt(preco)+'</b> | Com '+desc+'% OFF: <b>'+fmt(comDesc)+'</b><br>Lucro: <b>'+fmt(lucro)+'</b> | Margem: <b>'+margem.toFixed(1)+'%</b><br>Comissão: <b>'+fmt(comissao)+'</b> | Desconto MÁX: <b>'+maxDesc.toFixed(1)+'%</b><br>Total: <b>'+fmt(totalFinal)+'</b>';}} document.getElementById('parcelasVend').innerHTML='<b>Parcelas:</b> À vista '+fmt(totalFinal)+' | 3x '+fmt(totalFinal/3)+' | 6x '+fmt(totalFinal/6)+'<br>10x '+fmt(totalFinal/10)+' | 12x '+fmt(totalFinal/12);}
function limparVend(){document.getElementById('vNome').value=''; document.getElementById('vCodigo').value=''; document.getElementById('vPreco').value=''; document.getElementById('vCusto').value=''; document.getElementById('vDesc').value=10; document.getElementById('vDescLabel').innerText='10%'; document.getElementById('vEntrada').value=0; document.getElementById('vFrete').value=0;}
function calcAdd(v){expr+=v; document.getElementById('visorCalc').innerText=expr||'0';}
function calcLimpar(){expr=''; document.getElementById('visorCalc').innerText='0'; document.getElementById('histCalc').innerText='--';}
function calcBack(){expr=expr.slice(0,-1); document.getElementById('visorCalc').innerText=expr||'0';}
function calcSqrt(){var n=parseFloat(expr)||0; var r=Math.sqrt(n); expr=String(r); document.getElementById('visorCalc').innerText=r.toFixed(2);}
function calcQuad(){var n=parseFloat(expr)||0; var r=n*n; expr=String(r); document.getElementById('visorCalc').innerText=r.toFixed(2);}
function calcIgual(){try{var e2=expr.replace(/%/g,'/100'); var res=Function('return ('+e2+')')(); document.getElementById('histCalc').innerText=expr+' ='; document.getElementById('visorCalc').innerText=Number(res).toLocaleString('pt-BR',{maximumFractionDigits:2}); var h={}; h.texto=expr+' = '+res; h.data=new Date().toLocaleString('pt-BR'); historico.unshift(h); if(historico.length>20) historico.pop(); salvar(); renderHist(); expr=String(res);}catch(e){document.getElementById('visorCalc').innerText='Erro';}}
function copiarVisor(){var t=document.getElementById('visorCalc').innerText; navigator.clipboard.writeText(t); alert('Copiado: '+t);}
function usarComoPreco(){var t=document.getElementById('visorCalc').innerText.replace(/\./g,'').replace(',','.'); var n=parseFloat(t); if(!isNaN(n)){document.getElementById('vPreco').value=n; calcularVendedor(); abrirModal('modalVend');}}
function salvarCalculo(){var nome=document.getElementById('vNome').value||'Produto'; var preco=document.getElementById('vPreco').value||'0'; var h={}; h.texto=nome+' - '+fmt(preco); h.data=new Date().toLocaleString('pt-BR'); historico.unshift(h); salvar(); renderHist(); alert('Cálculo salvo!');}
function renderHist(){var div=document.getElementById('listaHist'); if(!div) return; div.innerHTML=''; if(!historico.length) div.innerHTML='<p style="font-size:13px">Nenhum cálculo ainda.</p>'; for(var i=0;i<Math.min(historico.length,20);i++){div.innerHTML+='<div style="font-size:13px;border-bottom:1px solid #E2E8F0;padding:6px 0"><b>'+esc(historico[i].texto)+'</b><br><small>'+esc(historico[i].data)+'</small></div>';}}
function limparHist(){if(confirm('Limpar histórico?')){historico=[]; salvar(); renderHist();}}
function enviarWhats(){var nome=document.getElementById('vNome').value||'Produto'; var preco=document.getElementById('vPreco').value||0; var desc=document.getElementById('vDesc').value||0; var comDesc=preco*(1-desc/100); var msg='Olá! Orçamento '+loja.nome+' - '+nome+' - De '+fmt(preco)+' por '+fmt(comDesc)+' com '+desc+'% OFF!'; var dest=document.getElementById('whatsDestino')? document.getElementById('whatsDestino').value : loja.whats; abrirWhatsComTexto(msg,dest||loja.whats);}
function salvarMetas(){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('Só o DONO pode mudar metas!'); renderMetas(); return;} metas.dia=parseFloat(document.getElementById('metaDia').value)||0; metas.semana=parseFloat(document.getElementById('metaSemana').value)||0; salvar(); renderMetas();}
function tentarEditarMes(){alert('🔒 META DO MÊS TRAVADA!');}
function renderMetas(){
document.getElementById('metaDia').value=metas.dia; document.getElementById('vendidoDia').value=fmt(metas.vendidoDia); document.getElementById('metaSemana').value=metas.semana; document.getElementById('vendidoSemana').value=fmt(metas.vendidoSemana); document.getElementById('metaMes').value=metas.mes; document.getElementById('vendidoMes').value=fmt(metas.vendidoMes); document.getElementById('textoTravaMes').innerText='Mês atual: '+nomeMesAtual();
function conta(meta,vendido,el,barra){var falta=meta-vendido; var perc=meta? Math.min(100,Math.round(vendido/meta*100)):0; var html=''; if(meta===0){html='Coloque sua meta!';} else if(falta<=0){html='<b>'+fmt(meta)+'</b> - <b>'+fmt(vendido)+'</b> = <span style="color:#4ADE80">META BATIDA! 🎉</span>';} else {html='<b>'+fmt(meta)+'</b> - <b>'+fmt(vendido)+'</b> = <span style="color:#FACC15">Falta '+fmt(falta)+'</span>';} document.getElementById(el).innerHTML=html; var b=document.getElementById(barra); b.style.width=perc+'%'; b.innerText=perc+'%';} conta(metas.dia,metas.vendidoDia,'contaDia','barraDia'); conta(metas.semana,metas.vendidoSemana,'contaSemana','barraSemana'); conta(metas.mes,metas.vendidoMes,'contaMes','barraMes');
// CORRIGIDO: sem % a mais, sem zero a mais - só fmt()
document.getElementById('cardHoje').innerText=fmt(metas.vendidoDia);
document.getElementById('cardSemana').innerText=fmt(metas.vendidoSemana);
document.getElementById('cardMes').innerText=fmt(metas.vendidoMes);
document.getElementById('cardMetaDia').innerText='Meta '+fmt(metas.dia);
document.getElementById('cardMetaSemana').innerText='Meta '+fmt(metas.semana);
document.getElementById('cardMetaMes').innerText='Meta '+fmt(metas.mes);
var div=document.getElementById('listaVendasHoje'); if(div){div.innerHTML=''; var listaMostrar=vendasHoje; if(usuarioLogado && usuarioLogado.tipo==='vend'){listaMostrar=vendasHoje.filter(function(v){return v.vendedor===usuarioLogado.nome;});} if(!listaMostrar.length) div.innerHTML='<p style="font-size:13px">Nenhuma venda ainda hoje.</p>'; var rev=listaMostrar.slice().reverse(); for(var i=0;i<rev.length;i++){div.innerHTML+='<div class="venda-item"><span>🛒 '+esc(rev[i].nome)+'<br><small>'+esc(rev[i].vendedor)+' - '+esc(rev[i].data)+'</small></span><b>'+fmt(rev[i].valor)+'</b></div>';}}}
function registrarVendaAutomatica(nome,valor,vend){var v={}; v.nome=nome; v.valor=valor; v.vendedor=vend||vendedorAtual; v.data=new Date().toLocaleString('pt-BR'); vendasHoje.push(v); metas.vendidoDia+=valor; metas.vendidoSemana+=valor; metas.vendidoMes+=valor; salvar(); renderMetas(); renderItens(); renderRanking(); renderGrafico(); return v;}
function venderPorItem(idx){var it=itens[idx]; if(!confirm('Confirmar venda de '+it.nome+' por '+fmt(it.preco)+'?\nVendedor: '+vendedorAtual)) return; registrarVendaAutomatica(it.nome+' ('+it.codigo+')',it.preco,vendedorAtual); alert('VENDA FEITA! ✅\n'+it.nome+' - '+fmt(it.preco)); fecharModal('modalItens'); abrirModal('modalGrafico');}
function venderItemAtual(){var nome=document.getElementById('vNome').value||'Produto'; var preco=parseFloat(document.getElementById('vPreco').value); var desc=parseFloat(document.getElementById('vDesc').value)||0; var frete=parseFloat(document.getElementById('vFrete').value)||0; var vend=document.getElementById('vVendedor').value||vendedorAtual; if(!preco){alert('Selecione um item!'); return;} var final=preco*(1-desc/100)+frete; if(!confirm('Confirmar venda de '+nome+' por '+fmt(final)+'?\nVendedor: '+vend)) return; registrarVendaAutomatica(nome,final,vend); alert('VENDA FEITA! ✅\n'+nome+' - '+fmt(final)); fecharModal('modalVend'); abrirModal('modalGrafico');}
function zerarMeta(tipo){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('Só o DONO pode zerar metas!'); return;} if(!confirm('Zerar?')) return; if(tipo==='dia') metas.vendidoDia=0; if(tipo==='semana') metas.vendidoSemana=0; salvar(); renderMetas();}
function limparVendasHoje(){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('Só o DONO pode limpar vendas!'); return;} if(!confirm('Limpar todas as vendas?')) return; vendasHoje=[]; metas.vendidoDia=0; metas.vendidoSemana=0; metas.vendidoMes=0; salvar(); renderMetas(); renderRanking();}
function fecharMes(){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('Só o DONO pode fechar o mês!'); return;} if(!confirm('Fechar o mês?')) return; var arc={}; arc.mes=metas.mesRef; arc.nomeMes=nomeMesAtual(); arc.metaMes=metas.mes; arc.vendidoMes=metas.vendidoMes; arc.vendas=vendasHoje.slice(); arc.dataFechamento=new Date().toLocaleString('pt-BR'); relatorios.push(arc); var novaMeta=prompt('Mês fechado! Qual a META DO MÊS NOVO? (R$)', '60000'); var nm=parseFloat(novaMeta); if(!isNaN(nm)&&nm>0) metas.mes=nm; metas.vendidoMes=0; metas.vendidoSemana=0; metas.vendidoDia=0; metas.mesRef=mesAtualStr(); vendasHoje=[]; salvar(); renderMetas(); renderRelatorio(); abrirModal('modalRel');}
function renderRanking(){var arr=calcRanking(); var div=document.getElementById('rankingBox'); div.innerHTML=''; var max=arr.length? arr[0].total:1; var emojis=['🥇','🥈','🥉']; for(var i=0;i<arr.length;i++){var r=arr[i]; var cls=i===0?' top1':''; var perc=max? Math.round(r.total/max*100):0; div.innerHTML+='<div class="rank-item'+cls+'"><div style="font-size:22px">'+(emojis[i]||'🏅')+'</div><div style="flex:1;min-width:0"><b>'+esc(r.nome)+(r.nome===vendedorAtual?' (Você)':'')+'</b><br><small>'+r.qtd+' vendas - '+fmt(r.total)+'</small><div class="barra-meta"><div style="width:'+perc+'%">'+perc+'%</div></div></div><b style="flex-shrink:0">'+fmt(r.total)+'</b></div>';} if(!vendasHoje.length) div.innerHTML+='<p style="font-size:13px">Nenhuma venda ainda.</p>';}
function textoRelatorio(){var t=''; t+='RELATÓRIO '+loja.nome.toUpperCase()+' - StillusCalc PRO\n'; t+='Data: '+new Date().toLocaleString('pt-BR')+'\n'; t+='Meta Dia: '+fmt(metas.dia)+' - Vendido: '+fmt(metas.vendidoDia)+'\n'; t+='Meta Mês: '+fmt(metas.mes)+' - Vendido: '+fmt(metas.vendidoMes)+'\n'; var arr=calcRanking(); for(var i=0;i<arr.length;i++){t+=(i+1)+'º '+arr[i].nome+' - '+fmt(arr[i].total)+' ('+arr[i].qtd+' vendas)\n';} return t;}
function renderRelatorio(){var div=document.getElementById('relatorioBox'); var html=''; html+='<div style="background:#F8FAFC;border-radius:12px;padding:10px;margin-top:8px;font-size:13px;line-height:1.6"><b>🏪 '+esc(loja.nome)+' - '+esc(nomeMesAtual())+'</b><br>Dia: <b>'+fmt(metas.dia)+'</b> - Vendido <b>'+fmt(metas.vendidoDia)+'</b><br>Mês 🔒: <b>'+fmt(metas.mes)+'</b> - Vendido <b>'+fmt(metas.vendidoMes)+'</b></div>'; var arr=calcRanking(); html+='<div style="background:#F8FAFC;border-radius:12px;padding:10px;margin-top:8px;font-size:13px;line-height:1.6"><b>🏆 RANKING</b><br>'; for(var i=0;i<arr.length;i++){html+=(i+1)+'º '+esc(arr[i].nome)+' - <b>'+fmt(arr[i].total)+'</b><br>';} html+='</div>'; div.innerHTML=html;}
function enviarRelatorioWhats(){var msg=textoRelatorio(); var dest=document.getElementById('whatsDestino')? document.getElementById('whatsDestino').value : loja.whats; abrirWhatsComTexto(msg,dest||loja.whats);}
function enviarRankingWhats(){var arr=calcRanking(); var msg='🏆 RANKING '+loja.nome+' - Hoje\n'; for(var i=0;i<arr.length;i++){msg+=(i+1)+'º '+arr[i].nome+' - '+fmt(arr[i].total)+'\n';} var dest=document.getElementById('whatsDestino')? document.getElementById('whatsDestino').value : loja.whats; abrirWhatsComTexto(msg,dest||loja.whats);}
function copiarRelatorio(){var t=textoRelatorio(); navigator.clipboard.writeText(t).then(function(){alert('Relatório copiado!');});}
function gerarHTMLRelatorio(){var h=''; h+='<!DOCTYPE html><html lang="pt-BR"><head><meta charset="UTF-8"><title>Relatório</title><style>body{font-family:Arial;padding:20px} table{width:100%;border-collapse:collapse} th,td{border:1px solid #ddd;padding:8px} th{background:#111827;color:#fff}</style></head><body>'; h+='<h1>'+esc(loja.nome)+' - Relatório</h1><p>'+new Date().toLocaleString('pt-BR')+'</p><table><tr><th>Meta</th><th>Meta</th><th>Vendido</th></tr><tr><td>Dia</td><td>'+fmt(metas.dia)+'</td><td>'+fmt(metas.vendidoDia)+'</td></tr><tr><td>Mês</td><td>'+fmt(metas.mes)+'</td><td>'+fmt(metas.vendidoMes)+'</td></tr></table>'; h+='<p>© StillusCalc PRO</p><button onclick="window.print()">IMPRIMIR</button></body></html>'; return h;}
function baixarArquivoRelatorio(){var html=gerarHTMLRelatorio(); var blob=new Blob([html],{type:'text/html'}); var a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='relatorio-'+mesAtualStr()+'.html'; a.click();}
function baixarRelatorioPDF(){var html=gerarHTMLRelatorio(); var w=window.open('','_blank'); if(!w){baixarArquivoRelatorio(); return;} w.document.write(html); w.document.close(); setTimeout(function(){w.print();},400);}
tentarEntrarViaLink();
renderLoja(); renderVendedores(); renderItens(); calcularVendedor(); renderMetas(); renderRanking(); renderGrafico(); renderRelatorio(); atualizarStatusPlano(); atualizarPillUsuario();
if(!usuarioLogado){setTimeout(function(){abrirModal('modalLogin');},600);}
else if(!estaLiberado()){setTimeout(function(){abrirModal('modalPlanos');},1200);}
</script>
</body>
</html>
