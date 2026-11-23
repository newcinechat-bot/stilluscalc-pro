<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>StillusCalc PRO - Sistema Integrado da Loja</title>
<meta name="theme-color" content="#111827">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif}
body{background:#111827;color:#0f172a;min-height:100vh;background-size:cover;background-position:center;background-attachment:fixed}
body::before{content:"";position:fixed;inset:0;background:rgba(17,24,39,.82);z-index:-1}
.topo{background:rgba(0,0,0,.6);color:#fff;padding:12px 12px 8px;text-align:center;position:sticky;top:0;z-index:50}
.topo h1{font-size:24px;line-height:1.1}
.topo h1 span{color:#facc15}
.topo p{font-size:12px;opacity:.9}
.resumo-topo{display:flex;flex-wrap:wrap;gap:6px;justify-content:center;margin-top:8px}
.pill-topo{background:#facc15;color:#000;padding:5px 10px;border-radius:20px;font-size:11px;font-weight:bold;white-space:nowrap}
.pill-topo.branca{background:#fff;color:#000}
.pill-topo.teste{background:#22c55e;color:#fff}
.pill-topo.travado{background:#ef4444;color:#fff}
.tabs-bar{background:rgba(255,255,255,.97);padding:8px 8px 8px 10px;position:sticky;top:0;z-index:40;box-shadow:0 2px 8px rgba(0,0,0,.15)}
.tabs{display:flex;gap:8px;overflow-x:auto;scrollbar-width:none;-webkit-overflow-scrolling:touch;padding-bottom:2px}
.tabs::-webkit-scrollbar{display:none}
.tab{flex-shrink:0;border:1px solid #e2e8f0;background:#f8fafc;color:#0f172a;padding:8px 14px;border-radius:20px;font-size:13px;font-weight:bold;cursor:pointer;white-space:nowrap}
.tab.ativo{background:#0f172a;color:#fff;border-color:#0f172a}
.tab.destaque{background:#facc15;border-color:#facc15;color:#000}
.tab.chat{background:#25D366;border-color:#25D366;color:#fff}
.tab.caixa{background:#7c3aed;border-color:#7c3aed;color:#fff}
.tab.rel{background:#0f172a;color:#fff;border-color:#0f172a}
.wrap{max-width:460px;margin:0 auto;padding:10px}
.card{background:rgba(255,255,255,.97);border-radius:16px;padding:14px;margin-bottom:10px;box-shadow:0 4px 14px rgba(0,0,0,.25)}
.card h3{margin-bottom:8px;font-size:16px}
input,select,textarea{width:100%;padding:11px;border:1px solid #cbd5e1;border-radius:10px;margin-bottom:8px;font-size:15px;background:#fff}
input[readonly]{background:#f1f5f9;color:#334155;font-weight:bold}
input.travado{background:#fee2e2!important;border:2px solid #ef4444!important;color:#991b1b!important;cursor:not-allowed}
label{font-size:12px;font-weight:bold;display:block;margin-bottom:3px}
.btn{border:none;border-radius:10px;padding:12px;font-weight:bold;cursor:pointer;width:100%;margin-bottom:6px}
.btn-amarelo{background:#facc15}
.btn-verde{background:#22c55e;color:#fff}
.btn-azul{background:#007bff;color:#fff}
.btn-cinza{background:#e2e8f0}
.btn-vermelho{background:#ef4444;color:#fff}
.btn-escuro{background:#0f172a;color:#fff}
.btn-roxo{background:#7c3aed;color:#fff}
.btn-whats{background:#25D366;color:#fff}
.visor{background:#0f172a;color:#fff;border-radius:14px;padding:12px;text-align:right;margin-bottom:8px}
.visor small{color:#94a3b8;font-size:12px;display:block;min-height:16px;word-break:break-all}
.visor b{font-size:32px;word-break:break-all}
.teclas{display:grid;grid-template-columns:repeat(4,1fr);gap:6px}
.teclas button{padding:14px 0;border:none;border-radius:12px;font-size:18px;font-weight:bold;cursor:pointer;background:#f1f5f9;min-width:0}
.teclas button.op{background:#facc15}
.teclas button.igual{background:#22c55e;color:#fff;grid-column:span 2}
.teclas button.limpar{background:#ef4444;color:#fff}
.vendedores-wrap{display:flex;flex-wrap:wrap;gap:6px}
.chip-vend{border:1px solid #6366f1;background:#e0e7ff;padding:7px 12px;border-radius:20px;font-size:12px;font-weight:bold;cursor:pointer;white-space:nowrap;max-width:100%;overflow:hidden;text-overflow:ellipsis}
.chip-vend.ativo{background:#0f172a;color:#fff;border-color:#0f172a}
.modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,.65);z-index:100;align-items:flex-end;justify-content:center}
.modal.aberto{display:flex}
.modal-box{background:#fff;width:100%;max-width:460px;max-height:92vh;overflow:auto;border-radius:18px 18px 0 0;padding:14px;padding-bottom:24px}
.modal-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;gap:8px}
.modal-top h3{font-size:17px}
.btn-fechar{background:#e2e8f0;border:none;width:36px;height:36px;border-radius:50%;font-weight:bold;cursor:pointer;font-size:16px;flex-shrink:0}
.foto-fundo{width:100%;height:110px;object-fit:cover;border-radius:12px;display:none;margin-bottom:8px;border:3px solid #facc15}
.range{width:100%}
.resultado{background:#f0fdf4;border:2px solid #22c55e;border-radius:12px;padding:12px;font-size:14px;line-height:1.6;margin-top:8px;word-break:break-word}
.resultado.perigo{background:#fef2f2;border-color:#ef4444}
.resultado.atencao{background:#fffbeb;border-color:#f59e0b}
.item-cad{display:flex;gap:8px;align-items:center;border-bottom:1px solid #e2e8f0;padding:8px 0}
.item-cad .ft{width:52px;height:52px;border-radius:10px;background:#fef2f2;display:flex;align-items:center;justify-content:center;font-size:28px;overflow:hidden;flex-shrink:0}
.item-cad .ft img{width:100%;height:100%;object-fit:cover}
.item-cad .info{flex:1;min-width:0;word-break:break-word}
.chip{display:inline-block;background:#fef3c7;border:1px solid #facc15;padding:6px 10px;border-radius:20px;font-size:12px;font-weight:bold;margin:3px;cursor:pointer;max-width:100%}
.hist{font-size:13px;border-bottom:1px solid #f1f5f9;padding:6px 0;word-break:break-word}
.modo{display:flex;gap:6px;margin-bottom:10px}
.modo button{flex:1;padding:10px;border:none;border-radius:10px;font-weight:bold;cursor:pointer;background:#e2e8f0;min-width:0}
.modo button.ativo{background:#0f172a;color:#fff}
.meta-card{background:#f8fafc;border:2px solid #e2e8f0;border-radius:14px;padding:12px;margin-bottom:10px}
.meta-card.dia{border-color:#22c55e}
.meta-card.semana{border-color:#007bff}
.meta-card.mes{border-color:#ef4444;background:#fff7f7}
.meta-conta{background:#0f172a;color:#fff;border-radius:10px;padding:10px;text-align:center;font-size:14px;line-height:1.6;margin:8px 0;word-break:break-word}
.meta-conta b{font-size:16px}
.meta-conta .falta{color:#facc15}
.meta-conta .bateu{color:#22c55e}
.barra-meta{height:18px;background:#e2e8f0;border-radius:20px;overflow:hidden;margin:6px 0}
.barra-meta div{height:100%;background:#22c55e;text-align:center;color:#fff;font-size:11px;line-height:18px;font-weight:bold;white-space:nowrap}
.venda-item{font-size:13px;border-bottom:1px solid #e2e8f0;padding:6px 0;display:flex;justify-content:space-between;gap:6px}
.venda-item span{min-width:0;word-break:break-word}
.badge-auto{background:#dcfce7;color:#15803d;padding:3px 8px;border-radius:20px;font-size:11px;font-weight:bold;white-space:nowrap}
.badge-travado{background:#fee2e2;color:#991b1b;padding:3px 8px;border-radius:20px;font-size:11px;font-weight:bold;white-space:nowrap}
.cadeado{background:#fee2e2;border:1px solid #ef4444;border-radius:10px;padding:8px;font-size:12px;text-align:center;margin-bottom:8px;color:#991b1b;font-weight:bold}
.rel-box{background:#f8fafc;border:1px solid #e2e8f0;border-radius:12px;padding:10px;margin-bottom:8px;font-size:13px;line-height:1.6;word-break:break-word}
.rank-item{display:flex;gap:10px;align-items:center;background:#fff;border:2px solid #e2e8f0;border-radius:12px;padding:10px;margin-bottom:8px}
.rank-item.top1{border-color:#facc15;background:#fffbeb}
.rank-item.top2{border-color:#cbd5e1;background:#f8fafc}
.rank-item.top3{border-color:#fb923c;background:#fff7ed}
.podio{font-size:26px;flex-shrink:0}
.flex2{display:flex;gap:6px}
.flex2 .btn{flex:1}
.boas-vindas{text-align:center}
.boas-vindas .logo{font-size:48px;margin-bottom:8px}
.boas-vindas h2{font-size:22px;margin-bottom:6px}
.boas-vindas p{font-size:13px;color:#64748b;margin-bottom:12px;line-height:1.5}
.passo{background:#f8fafc;border:2px solid #e2e8f0;border-radius:12px;padding:10px;margin-bottom:8px;text-align:left}
.passo b{display:block;margin-bottom:4px}
.graf-bar{display:flex;align-items:flex-end;gap:8px;height:180px;padding:10px;background:#f8fafc;border-radius:12px;margin:10px 0;overflow-x:auto}
.graf-col{flex:1;min-width:52px;display:flex;flex-direction:column;align-items:center;justify-content:flex-end;gap:4px}
.graf-col .barra{width:100%;max-width:48px;border-radius:8px 8px 0 0;display:flex;align-items:flex-start;justify-content:center;color:#fff;font-weight:bold;font-size:11px;padding-top:6px;min-height:18px}
.graf-col span{font-size:11px;font-weight:bold;text-align:center;word-break:break-word}
.chat-header{background:#075E54;color:#fff;padding:10px;border-radius:12px 12px 0 0;display:flex;align-items:center;gap:10px}
.chat-header .avatar{width:38px;height:38px;background:#25D366;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
.chat-box{background:#ECE5DD;border-radius:0 0 12px 12px;padding:10px;min-height:280px;max-height:380px;overflow-y:auto;display:flex;flex-direction:column;gap:8px}
.msg{max-width:82%;padding:8px 10px;border-radius:12px;font-size:13px;line-height:1.4;word-break:break-word;position:relative}
.msg.eu{background:#DCF8C6;align-self:flex-end;border-bottom-right-radius:2px}
.msg.cliente{background:#fff;align-self:flex-start;border-bottom-left-radius:2px}
.msg.robo{background:#FFF3CD;align-self:flex-start;border:1px solid #facc15}
.msg small{display:block;font-size:10px;color:#888;text-align:right;margin-top:4px}
.msg img,.msg video{width:100%;max-width:220px;border-radius:10px;display:block;margin:4px 0}
.prod-card{background:#fff;border:1px solid #e2e8f0;border-radius:10px;padding:8px;margin:4px 0}
.prod-card img{width:100%;height:110px;object-fit:cover;border-radius:8px}
.cliente-item{display:flex;gap:8px;align-items:center;padding:8px;border-bottom:1px solid #f1f5f9;cursor:pointer}
.cliente-item .av{width:40px;height:40px;background:#25D366;color:#fff;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:bold;flex-shrink:0}
.emoji-panel{display:flex;flex-wrap:wrap;gap:4px;background:#fff;border:1px solid #e2e8f0;border-radius:12px;padding:8px;margin:6px 0}
.emoji-panel span{font-size:22px;cursor:pointer;padding:4px}
.caixa-item{background:#fff;border:2px solid #e2e8f0;border-radius:12px;padding:10px;margin-bottom:8px}
.caixa-item.aguardando{border-color:#f59e0b;background:#FFFBEB}
.caixa-item.finalizado{border-color:#22c55e;background:#F0FDF4}
.caixa-item.cancelado{border-color:#ef4444;background:#FEF2F2;opacity:.7}
.plano-card{border:2px solid #e2e8f0;border-radius:14px;padding:12px;margin-bottom:10px;cursor:pointer}
.plano-card.selecionado{border-color:#facc15;background:#FFFBEB;box-shadow:0 4px 12px rgba(250,204,21,.3)}
.plano-card.pro{border-color:#22c55e;background:#F0FDF4}
.plano-card.pro.selecionado{border-color:#22c55e;background:#DCFCE7}
.qr-box{background:#fff;border:2px dashed #cbd5e1;border-radius:12px;padding:12px;text-align:center;margin:10px 0}
.qr-box img{width:180px;height:180px}
.login-box{background:#fff;border-radius:16px;padding:16px;margin:10px 0}
.login-aba{display:flex;gap:6px;margin-bottom:10px}
.login-aba button{flex:1;padding:12px;border:none;border-radius:10px;font-weight:bold;cursor:pointer;background:#e2e8f0}
.login-aba button.ativo{background:#0f172a;color:#fff}
@media print{body{background:#fff!important} body::before{display:none!important} body *{visibility:hidden} #areaImpressao, #areaImpressao *{visibility:visible} #areaImpressao{position:absolute;left:0;top:0;width:100%;padding:10px;display:block!important} .topo,.wrap,.modal,.tabs-bar{display:none!important}}
#areaImpressao{display:none}
</style>
</head>
<body>
<div class="topo">
<h1>StillusCalc <span>PRO</span></h1>
<p id="nomeLojaTopo">Sua Loja - O barato e aqui!</p>
<div class="resumo-topo">
<span class="pill-topo" id="vendedorAtualTopo">Vendedor: --</span>
<span class="pill-topo branca" id="resumoDiaTopo">Dia: --</span>
<span class="pill-topo branca" id="resumoMesTopo">Mes: -- 🔒</span>
</div>
<div style="margin-top:8px;display:flex;gap:6px;justify-content:center;flex-wrap:wrap">
<span class="pill-topo teste" id="pillTeste" style="cursor:pointer" onclick="abrirModal('modalPlanos')">🎁 TESTE GRATIS: --</span>
<span class="pill-topo" id="pillUsuario" style="background:#fff;color:#000">👤 --</span>
<button id="btnInstalar" onclick="instalarApp()" style="display:none;background:#facc15;border:none;padding:6px 14px;border-radius:20px;font-weight:bold;font-size:12px;cursor:pointer">📲 INSTALAR APP</button>
<button onclick="abrirModal('modalSync')" style="background:#22c55e;color:#fff;border:none;padding:6px 14px;border-radius:20px;font-weight:bold;font-size:12px;cursor:pointer">🔄 SINCRONIZAR</button>
<button onclick="abrirModal('modalBackup')" style="background:#fff;border:none;padding:6px 14px;border-radius:20px;font-weight:bold;font-size:12px;cursor:pointer">💾 BACKUP</button>
<button onclick="sairLogin()" style="background:#ef4444;color:#fff;border:none;padding:6px 14px;border-radius:20px;font-weight:bold;font-size:12px;cursor:pointer">🚪 SAIR</button>
</div>
</div>
<div class="tabs-bar">
<div class="tabs" id="tabsBar">
<button class="tab" onclick="verificarTravaEAbrir('modalLoja',this)">🏪 Minha Loja</button>
<button class="tab chat" onclick="verificarTravaEAbrir('modalChat',this)">💬 Chat Cliente</button>
<button class="tab caixa" onclick="verificarTravaEAbrir('modalCaixa',this)">🧾 Caixa</button>
<button class="tab" onclick="verificarTravaEAbrir('modalFoto',this)">🖼️ Foto Fundo</button>
<button class="tab" onclick="verificarTravaEAbrir('modalCad',this)">➕ Cadastrar</button>
<button class="tab" onclick="verificarTravaEAbrir('modalItens',this)">📦 Meus Itens</button>
<button class="tab" onclick="verificarTravaEAbrir('modalVend',this)">💰 Vendedor</button>
<button class="tab" onclick="verificarTravaEAbrir('modalMeta',this)">🎯 Metas</button>
<button class="tab destaque" onclick="verificarTravaEAbrir('modalRank',this)">🏆 Ranking</button>
<button class="tab" onclick="verificarTravaEAbrir('modalGrafico',this)">📊 Grafico</button>
<button class="tab" onclick="verificarTravaEAbrir('modalSync',this)">🔄 Sincronizar</button>
<button class="tab" onclick="verificarTravaEAbrir('modalHist',this)">🕒 Historico</button>
<button class="tab" onclick="verificarTravaEAbrir('modalBackup',this)">💾 Backup</button>
<button class="tab" onclick="abrirModal('modalPlanos',this)">💎 PLANOS</button>
<button class="tab rel" onclick="verificarTravaEAbrir('modalRel',this)">📊 Relatorio</button>
</div>
</div>
<div id="areaImpressao"></div>
<div class="wrap">
<div class="card">
<h3>Calculadora Normal</h3>
<div class="visor"><small id="histCalc">StillusCalc PRO</small><b id="visorCalc">0</b></div>
<div class="teclas">
<button class="limpar" onclick="calcLimpar()">C</button>
<button onclick="calcAdd('(')">(</button>
<button onclick="calcAdd(')')">)</button>
<button class="op" onclick="calcAdd('%')">%</button>
<button onclick="calcSqrt()">Raiz</button>
<button onclick="calcQuad()">x²</button>
<button onclick="calcBack()">Apagar</button>
<button class="op" onclick="calcAdd('/')">/</button>
<button onclick="calcAdd('7')">7</button>
<button onclick="calcAdd('8')">8</button>
<button onclick="calcAdd('9')">9</button>
<button class="op" onclick="calcAdd('*')">x</button>
<button onclick="calcAdd('4')">4</button>
<button onclick="calcAdd('5')">5</button>
<button onclick="calcAdd('6')">6</button>
<button class="op" onclick="calcAdd('-')">-</button>
<button onclick="calcAdd('1')">1</button>
<button onclick="calcAdd('2')">2</button>
<button onclick="calcAdd('3')">3</button>
<button class="op" onclick="calcAdd('+')">+</button>
<button onclick="calcAdd('0')">0</button>
<button onclick="calcAdd('00')">00</button>
<button onclick="calcAdd('.')">.</button>
<button class="igual" onclick="calcIgual()">=</button>
</div>
<div class="flex2" style="margin-top:8px">
<button class="btn btn-azul" onclick="copiarVisor()">COPIAR</button>
<button class="btn btn-cinza" onclick="usarComoPreco()">USAR COMO PRECO</button>
</div>
</div>
<div class="card">
<label>Quem esta vendendo agora?</label>
<div id="listaVendedoresTopo" class="vendedores-wrap"></div>
<button class="btn btn-roxo" style="margin-top:8px" onclick="verificarTravaEAbrir('modalVendEquipe')">+ CADASTRAR VENDEDOR / TROCAR VENDEDOR</button>
</div>
<div class="card" style="display:flex;gap:6px">
<button class="btn btn-whats" onclick="verificarTravaEAbrir('modalChat')">💬 ABRIR CHAT COM CLIENTE</button>
<button class="btn btn-roxo" onclick="verificarTravaEAbrir('modalCaixa')">🧾 IR PRO CAIXA</button>
</div>
<div class="card" style="text-align:center">
<p style="font-size:11px;color:#64748b">© 2026 StillusCalc PRO - Todos os direitos reservados.<br>Proibida a reproducao sem autorizacao.</p>
<button class="btn btn-cinza" style="margin-top:8px" onclick="abrirModal('modalBoasVindas')">VER TELA DE BOAS-VINDAS NOVAMENTE</button>
</div>
</div>
<div id="modalLogin" class="modal">
<div class="modal-box">
<div class="boas-vindas"><div class="logo">💰</div><h2>StillusCalc PRO</h2><p>Entre para vender! O dono cadastra os vendedores com login e senha.</p></div>
<div class="login-aba">
<button id="abaDono" class="ativo" onclick="setAbaLogin('dono')">👑 SOU O DONO</button>
<button id="abaVend" onclick="setAbaLogin('vend')">👤 SOU VENDEDOR</button>
</div>
<div id="boxLoginDono">
<label>Nome da sua loja</label><input id="loginLojaNome" placeholder="Ex: Loja do Joao..." maxlength="60">
<label>Seu WhatsApp (dono)</label><input id="loginDonoWhats" placeholder="Ex: 61999999999" maxlength="13">
<label>Codigo de liberacao (apos pagar) ou deixe em branco no teste gratis</label><input id="loginCodigoDono" placeholder="Ex: PRO-30-STILLUS ou VITALICIO-STILLUS-PRO" style="text-transform:uppercase">
<button class="btn btn-escuro" style="padding:15px;font-size:16px" onclick="entrarComoDono()">👑 ENTRAR COMO DONO</button>
<p style="font-size:12px;color:#64748b;text-align:center">No teste gratis de 7 dias, pode entrar sem codigo.<br>Depois do teste, precisa pagar e digitar o codigo.</p>
</div>
<div id="boxLoginVend" style="display:none">
<label>Codigo da Loja (o dono te passa)</label><input id="loginCodigoLoja" placeholder="Ex: LOJA-ABC123" style="text-transform:uppercase">
<label>Seu Login</label><input id="loginVendLogin" placeholder="Ex: maria" maxlength="30">
<label>Sua Senha</label><input id="loginVendSenha" type="password" placeholder="Sua senha..." maxlength="30">
<button class="btn btn-verde" style="padding:15px;font-size:16px" onclick="entrarComoVendedor()">👤 ENTRAR COMO VENDEDOR</button>
<p style="font-size:12px;color:#64748b;text-align:center">Nao tem login? Peca para o dono cadastrar voce em Equipe &gt; Cadastrar Vendedor.</p>
<div style="background:#FFFBEB;border:1px solid #facc15;border-radius:10px;padding:10px;font-size:12px;line-height:1.6;margin-top:8px">
<b>Teste rapido sem dono:</b><br>Codigo da Loja: <b>LOJA-TESTE</b><br>Login: <b>maria</b> / Senha: <b>1234</b><br><button class="btn btn-amarelo" style="margin-top:6px" onclick="entrarTesteVendedor()">⚡ ENTRAR COM CONTA TESTE</button>
</div>
</div>
<button class="btn btn-cinza" onclick="abrirModal('modalPlanos')">💎 VER PLANOS E PAGAR COM PIX</button>
</div>
</div>

<div id="modalPlanos" class="modal">
<div class="modal-box">
<div class="modal-top"><h3>💎 Planos - StillusCalc PRO</h3><button class="btn-fechar" onclick="fecharModal('modalPlanos')">X</button></div>
<div id="statusPlanoBox" style="background:#0f172a;color:#fff;border-radius:12px;padding:12px;text-align:center;font-size:13px;line-height:1.6;margin-bottom:10px"></div>
<p style="font-size:12px;color:#64748b;margin-bottom:10px;text-align:center">Escolha seu plano. Pague com Pix - copia e cola ou QR Code.<br><b>Seu numero Pix nao aparece na tela por seguranca.</b></p>
<div class="plano-card" id="cardBasico" onclick="selecionarPlano('basico')">
<h3>📦 BÁSICO - R$ 49,90/mês</h3>
<p style="font-size:13px;line-height:1.6">✅ Calculadora do Vendedor<br>✅ Metas Dia / Semana / Mês<br>✅ Ranking da equipe<br>✅ Relatório em PDF<br>❌ Sem Chat, sem Robô, sem Caixa</p>
</div>
<div class="plano-card pro selecionado" id="cardPro" onclick="selecionarPlano('pro')">
<h3>🏆 PRO - R$ 89,90/mês ⭐ MAIS VENDIDO</h3>
<p style="font-size:13px;line-height:1.6">✅ Tudo do Básico<br>✅ 💬 Chat com Cliente<br>✅ 🤖 Robô Inteligente<br>✅ 🧾 Caixa da Loja<br>✅ 📊 Gráfico por Vendedor<br>✅ 🔄 Sincronização<br>✅ Vendedores ilimitados<br>✅ Login por vendedor com senha</p>
</div>
<div class="plano-card" id="cardVitalicio" onclick="selecionarPlano('vitalicio')">
<h3>💎 VITALÍCIO - R$ 497 uma vez</h3>
<p style="font-size:13px;line-height:1.6">✅ Tudo do PRO<br>✅ Paga uma vez, usa pra sempre<br>✅ Sem mensalidade nunca mais<br>✅ Atualizações inclusas</p>
</div>
<div id="areaPagamento" style="display:none">
<div style="background:#F0FDF4;border:2px solid #22c55e;border-radius:12px;padding:12px;text-align:center">
<b id="tituloPagamento">Pagamento - Plano PRO - R$ 89,90</b><br>
<small style="color:#64748b">Pague com Pix - copia e cola ou escaneie o QR Code abaixo.<br>Depois envie o comprovante no WhatsApp e receba seu código de liberação.</small>
<div class="qr-box"><img id="imgQR" src="" alt="QR Code Pix"><br><small>Escaneie com o app do seu banco</small></div>
<button class="btn btn-verde" onclick="copiarPix()">📋 COPIAR CÓDIGO PIX COPIA E COLA</button>
<p style="font-size:11px;color:#94a3b8">Seu código Pix fica oculto por segurança.<br>Não exibimos a chave na tela.</p>
</div>
<label style="margin-top:10px">Já pagou? Digite o código de liberação que você recebeu:</label>
<input id="codigoLiberacao" placeholder="Ex: PRO-30-STILLUS" style="text-transform:uppercase">
<button class="btn btn-escuro" onclick="validarCodigo()">🔓 LIBERAR MEU APP AGORA</button>
<button class="btn btn-whats" onclick="enviarComprovanteWhats()">📱 ENVIAR COMPROVANTE NO WHATSAPP</button>
</div>
<button class="btn btn-verde" style="padding:15px;font-size:16px" id="btnPagarPlano" onclick="mostrarPagamento()">💳 PAGAR COM PIX - PLANO PRO</button>
<p style="font-size:11px;color:#94a3b8;text-align:center">Ao pagar, você concorda com os termos de uso.<br>© 2026 StillusCalc PRO</p>
</div>
</div>

<div id="modalBoasVindas" class="modal">
<div class="modal-box">
<div class="boas-vindas"><div class="logo">💰</div><h2>Bem-vindo ao StillusCalc PRO!</h2><p>Você tem <b>7 dias grátis</b> com tudo liberado! Chat, Caixa, Metas, Ranking, Grafico e Robo. Configure em 30 segundos:</p></div>
<div class="passo"><b>1️⃣ Qual o nome da sua loja?</b><input id="bvLoja" placeholder="Ex: Loja do Joao..." maxlength="60"></div>
<div class="passo"><b>2️⃣ WhatsApp da loja</b><input id="bvWhats" placeholder="Ex: 61999999999" maxlength="13"></div>
<div class="passo"><b>3️⃣ Quem sao seus vendedores? (separe por virgula)</b><input id="bvVends" placeholder="Ex: Maria, Joao, Carlos" maxlength="120"></div>
<div class="passo"><b>4️⃣ Qual sua meta do mes? (R$)</b><input id="bvMetaMes" type="number" placeholder="Ex: 60000"></div>
<button class="btn btn-verde" style="padding:15px;font-size:16px" onclick="concluirBoasVindas()">🚀 COMECAR MEUS 7 DIAS GRATIS!</button>
<button class="btn btn-cinza" onclick="fecharModal('modalBoasVindas')">PULAR - CONFIGURAR DEPOIS</button>
</div>
</div>

<div id="modalChat" class="modal" onclick="if(event.target.id==='modalChat') fecharModal('modalChat')">
<div class="modal-box">
<div class="modal-top"><h3>💬 Sala de Bate-Papo com Cliente</h3><button class="btn-fechar" onclick="fecharModal('modalChat')">X</button></div>
<div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:8px">
<button id="btnRobo" class="btn btn-cinza" style="width:auto;padding:8px 12px" onclick="toggleRobo()">🤖 ROBO: DESLIGADO</button>
<button class="btn btn-azul" style="width:auto;padding:8px 12px" onclick="abrirModal('modalRobo')">⚙️ CONFIGURAR ROBO</button>
<button class="btn btn-verde" style="width:auto;padding:8px 12px" onclick="simularCliente()">👤 SIMULAR CLIENTE</button>
</div>
<label>Nome do cliente</label>
<div class="flex2"><input id="novoClienteNome" placeholder="Ex: Joao da Silva..." maxlength="50"><button class="btn btn-whats" style="width:110px" onclick="addCliente()">+ CLIENTE</button></div>
<label>Conversas:</label>
<div id="listaClientes" style="background:#fff;border:1px solid #e2e8f0;border-radius:12px;max-height:160px;overflow:auto"></div>
<div id="chatAtivoBox" style="margin-top:10px">
<div class="chat-header"><div class="avatar" id="chatAvatar">👤</div><div style="flex:1"><b id="chatClienteNome">Selecione um cliente acima</b><br><small id="chatClienteStatus">--</small></div><span id="chatRoboStatus" style="font-size:11px;background:#25D366;padding:4px 8px;border-radius:20px">Robo OFF</span></div>
<div id="chatBox" class="chat-box"><p style="font-size:13px;color:#888;text-align:center;margin-top:40px">Selecione um cliente para comecar.<br>Comece a venda aqui e termine na loja! 🛍️</p></div>
<div id="emojiPanel" class="emoji-panel" style="display:none"></div>
<div class="flex2" style="margin-top:8px">
<button class="btn btn-cinza" style="width:48px" onclick="toggleEmoji()">😀</button>
<label class="btn btn-cinza" style="width:48px;text-align:center">📎<input type="file" accept="image/*,video/*" style="display:none" onchange="enviarMidiaChat(this)"></label>
<button class="btn btn-amarelo" style="flex:1" onclick="abrirModal('modalEnviarProduto')">🛍️ ENVIAR PRODUTO</button>
</div>
<div class="flex2"><input id="chatInput" placeholder="Digite sua mensagem..." onkeypress="if(event.key==='Enter') enviarMsgChat()"><button class="btn btn-whats" style="width:70px" onclick="enviarMsgChat()">➤</button></div>
<button class="btn btn-verde" onclick="comecarVendaNoChat()">🛒 COMECAR VENDA NO CHAT -> ENVIAR PRO CAIXA</button>
<button class="btn btn-escuro" onclick="enviarChatWhatsApp()">📱 ENVIAR ESSA CONVERSA NO WHATSAPP REAL</button>
</div>
</div>
</div>

<div id="modalEnviarProduto" class="modal">
<div class="modal-box">
<div class="modal-top"><h3>🛍️ Enviar Produto no Chat</h3><button class="btn-fechar" onclick="fecharModal('modalEnviarProduto')">X</button></div>
<div id="listaProdutosChat"></div>
</div>
</div>

<div id="modalRobo" class="modal">
<div class="modal-box">
<div class="modal-top"><h3>🤖 Robo Inteligente - Gatilhos</h3><button class="btn-fechar" onclick="fecharModal('modalRobo')">X</button></div>
<label>Resposta para: OI / BOM DIA</label><textarea id="roboOi" rows="2"></textarea>
<label>Resposta para: PRECO / VALOR</label><textarea id="roboPreco" rows="2"></textarea>
<label>Resposta para: DESCONTO</label><textarea id="roboDesconto" rows="2"></textarea>
<label>Resposta para: ENTREGA / FRETE</label><textarea id="roboEntrega" rows="2"></textarea>
<label>Resposta para: PARCELA / CARTAO</label><textarea id="roboParcela" rows="2"></textarea>
<label>Resposta para: TEM / ESTOQUE</label><textarea id="roboEstoque" rows="2"></textarea>
<button class="btn btn-verde" onclick="salvarRobo()">💾 SALVAR ROBO</button>
</div>
</div>

<div id="modalCaixa" class="modal" onclick="if(event.target.id==='modalCaixa') fecharModal('modalCaixa')">
<div class="modal-box">
<div class="modal-top"><h3>🧾 Caixa da Loja</h3><button class="btn-fechar" onclick="fecharModal('modalCaixa')">X</button></div>
<div style="background:#0f172a;color:#fff;border-radius:12px;padding:12px;text-align:center;font-size:13px;line-height:1.6;margin-bottom:10px" id="resumoCaixa"></div>
<div class="flex2"><button class="btn btn-amarelo" onclick="abrirModal('modalItens')">+ NOVA VENDA PRO CAIXA</button><button class="btn btn-whats" onclick="abrirModal('modalChat')">💬 VENDER PELO CHAT</button></div>
<h3 style="font-size:15px;margin:10px 0 8px">Fila do Caixa - Aguardando</h3>
<div id="listaCaixa"></div>
<h3 style="font-size:15px;margin:10px 0 8px">Ja Finalizados Hoje</h3>
<div id="listaCaixaFinalizados"></div>
</div>
</div>

<div id="modalSync" class="modal" onclick="if(event.target.id==='modalSync') fecharModal('modalSync')">
<div class="modal-box">
<div class="modal-top"><h3>🔄 Sincronizar</h3><button class="btn-fechar" onclick="fecharModal('modalSync')">X</button></div>
<p id="statusSync" style="font-size:12px;color:#64748b;margin-bottom:8px"></p>
<label>Codigo da sua loja - passe para seus vendedores</label><input id="codigoLoja" readonly>
<div style="background:#FFFBEB;border:1px solid #facc15;border-radius:10px;padding:10px;font-size:12px;line-height:1.6;margin-bottom:8px" id="boxCodigoLojaVendedor"></div>
<div class="flex2"><button class="btn btn-verde" onclick="gerarLinkLoja()">🔗 GERAR LINK DA LOJA</button><button class="btn btn-azul" onclick="copiarLinkLoja()">📋 COPIAR LINK</button></div>
<button class="btn btn-escuro" onclick="enviarLinkLojaWhats()">📱 ENVIAR LINK NO WHATSAPP</button>
<hr style="margin:10px 0"><h3 style="font-size:15px;margin-bottom:8px">Vendedor: Enviar minhas vendas pro dono</h3>
<button class="btn btn-verde" onclick="enviarVendasWhats()">📤 ENVIAR MINHAS VENDAS PRO DONO</button>
<hr style="margin:10px 0"><h3 style="font-size:15px;margin-bottom:8px">Dono: Receber vendas</h3>
<textarea id="codigoReceber" rows="4" placeholder="Cole aqui o codigo STILLUS..."></textarea>
<button class="btn btn-escuro" onclick="receberVendas()">⬇️ RECEBER VENDAS</button>
</div>
</div>

<div id="modalGrafico" class="modal" onclick="if(event.target.id==='modalGrafico') fecharModal('modalGrafico')">
<div class="modal-box">
<div class="modal-top"><h3>📊 Grafico de Vendas</h3><button class="btn-fechar" onclick="fecharModal('modalGrafico')">X</button></div>
<div id="resumoGrafico" style="background:#0f172a;color:#fff;border-radius:12px;padding:12px;text-align:center;font-size:13px;line-height:1.6;margin:10px 0"></div>
<div id="graficoBarras" class="graf-bar"></div>
<div id="listaGrafico"></div>
<div class="flex2"><button class="btn btn-verde" onclick="enviarGraficoWhats()">📱 ENVIAR GRAFICO NO WHATS</button><button class="btn btn-azul" onclick="renderGrafico()">🔄 ATUALIZAR</button></div>
</div>
</div>

<div id="modalBackup" class="modal" onclick="if(event.target.id==='modalBackup') fecharModal('modalBackup')">
<div class="modal-box">
<div class="modal-top"><h3>💾 Backup</h3><button class="btn-fechar" onclick="fecharModal('modalBackup')">X</button></div>
<button class="btn btn-verde" style="padding:15px" onclick="exportarBackup()">⬇️ BAIXAR BACKUP AGORA</button>
<label style="margin-top:10px">Restaurar backup:</label>
<label class="btn btn-azul" style="display:block;text-align:center">📂 ESCOLHER ARQUIVO<input type="file" accept=".json" style="display:none" onchange="importarBackup(this)"></label>
<button class="btn btn-vermelho" onclick="apagarTudo()">🗑️ APAGAR TUDO</button>
</div>
</div>

<div id="modalLoja" class="modal" onclick="if(event.target.id==='modalLoja') fecharModal('modalLoja')">
<div class="modal-box">
<div class="modal-top"><h3>🏪 Minha Loja</h3><button class="btn-fechar" onclick="fecharModal('modalLoja')">X</button></div>
<label>Nome da sua loja</label><input id="cfgLoja" maxlength="60">
<label>WhatsApp da loja</label><input id="cfgWhats" maxlength="13">
<label>Slogan</label><input id="cfgSlogan" maxlength="80">
<label>Codigo da Loja (passe para os vendedores)</label><input id="cfgCodigoLoja" readonly>
<label>Tipo de loja</label><select id="cfgTipo"><option>Moveis e Eletrodomesticos</option><option>Celulares e Eletronicos</option><option>Roupas e Calcados</option><option>Motos e Veiculos</option><option>Beleza e Cosmeticos</option><option>Alimentos e Mercado</option><option>Outro tipo de loja</option></select>
<button class="btn btn-verde" onclick="salvarLoja()">SALVAR MINHA LOJA</button>
</div>
</div>
<div id="modalVendEquipe" class="modal" onclick="if(event.target.id==='modalVendEquipe') fecharModal('modalVendEquipe')">
<div class="modal-box">
<div class="modal-top"><h3>👥 Equipe de Vendedores - Só o Dono cadastra</h3><button class="btn-fechar" onclick="fecharModal('modalVendEquipe')">X</button></div>
<div style="background:#FFFBEB;border:1px solid #facc15;border-radius:10px;padding:10px;font-size:12px;line-height:1.6;margin-bottom:10px">
<b>Codigo da sua loja:</b> <span id="codigoLojaEquipe" style="font-size:15px;color:#0f172a">--</span><br>
Passe esse codigo + login + senha para o vendedor entrar.<br>
<button class="btn btn-amarelo" style="margin-top:6px" onclick="copiarDadosVendedores()">📋 COPIAR DADOS PARA ENVIAR NO WHATS</button>
</div>
<label>Nome do vendedor</label><input id="novoVendNome" maxlength="40" placeholder="Ex: Maria Silva">
<label>Login do vendedor (sem espaco, so letras)</label><input id="novoVendLogin" maxlength="30" placeholder="Ex: maria">
<label>Senha do vendedor</label><input id="novoVendSenha" maxlength="30" placeholder="Ex: 1234">
<button class="btn btn-verde" onclick="addVendedor()">+ CADASTRAR VENDEDOR COM LOGIN E SENHA</button>
<div id="listaVendedoresModal" class="vendedores-wrap" style="margin-top:8px"></div>
<div id="listaLoginsVendedores" style="margin-top:10px"></div>
<p style="font-size:11px;color:#94a3b8;margin-top:8px">Se voce e vendedor, voce nao consegue cadastrar ninguem. So o dono cadastra.</p>
</div>
</div>

<div id="modalFoto" class="modal" onclick="if(event.target.id==='modalFoto') fecharModal('modalFoto')">
<div class="modal-box">
<div class="modal-top"><h3>Foto da Loja no Fundo</h3><button class="btn-fechar" onclick="fecharModal('modalFoto')">X</button></div>
<img id="prevFundo" class="foto-fundo">
<label class="btn btn-amarelo" style="display:block;text-align:center">COLOCAR FOTO DA LOJA NO FUNDO<input type="file" accept="image/*" style="display:none" onchange="salvarFundo(this)"></label>
<button class="btn btn-cinza" onclick="removerFundo()">TIRAR FOTO DO FUNDO</button>
</div>
</div>

<div id="modalCad" class="modal" onclick="if(event.target.id==='modalCad') fecharModal('modalCad')">
<div class="modal-box">
<div class="modal-top"><h3>Cadastrar Item</h3><button class="btn-fechar" onclick="fecharModal('modalCad')">X</button></div>
<label>Nome do item</label><input id="nNome" maxlength="80">
<label>Codigo</label><input id="nCodigo" maxlength="20" style="text-transform:uppercase">
<label>Preco de Venda (R$)</label><input id="nPreco" type="number" min="0">
<label>Preco de Custo (R$)</label><input id="nCusto" type="number" min="0">
<label>Categoria</label><select id="nCat"><option>Produto Geral</option><option>Sala de Estar</option><option>Cozinha</option><option>Cama / Colchao</option><option>Celulares</option><option>Roupas</option><option>Outro</option></select>
<label>Foto do item (opcional)</label><input type="file" accept="image/*" onchange="preverFotoItem(this)">
<img id="prevItem" class="foto-fundo" style="height:90px">
<button class="btn btn-verde" onclick="cadastrarItem()">CADASTRAR ITEM</button>
</div>
</div>

<div id="modalItens" class="modal" onclick="if(event.target.id==='modalItens') fecharModal('modalItens')">
<div class="modal-box">
<div class="modal-top"><h3>Meus Itens</h3><button class="btn-fechar" onclick="fecharModal('modalItens')">X</button></div>
<p style="font-size:12px;color:#64748b;margin-bottom:8px">Vendendo como: <b id="vendendoComoItens">--</b></p>
<input id="buscaItem" placeholder="Buscar por nome ou codigo..." oninput="renderItens()">
<div id="listaItens"></div>
<div id="favoritosBox" style="margin-top:8px"></div>
</div>
</div>

<div id="modalVend" class="modal" onclick="if(event.target.id==='modalVend') fecharModal('modalVend')">
<div class="modal-box">
<div class="modal-top"><h3>Calculadora do Vendedor</h3><button class="btn-fechar" onclick="fecharModal('modalVend')">X</button></div>
<div class="modo"><button id="btnModoVend" class="ativo" onclick="setModo('vend')">MODO VENDEDOR</button><button id="btnModoCli" onclick="setModo('cli')">MODO CLIENTE</button></div>
<label>Vendedor da venda</label><select id="vVendedor"></select>
<label>Cliente (opcional)</label><input id="vCliente" placeholder="Nome do cliente..." maxlength="60">
<label>Item selecionado</label><input id="vNome" readonly placeholder="Clique num item em Meus Itens ou digite o codigo">
<label>Codigo</label><div class="flex2"><input id="vCodigo" placeholder="001" style="text-transform:uppercase"><button class="btn btn-escuro" style="width:110px" onclick="puxarItem()">PUXAR</button></div>
<label>Preco de Venda (R$)</label><input id="vPreco" type="number" oninput="calcularVendedor()">
<label>Preco de Custo (R$)</label><input id="vCusto" type="number" oninput="calcularVendedor()">
<label>Desconto (%)</label><input id="vDesc" type="range" min="0" max="50" value="10" class="range" oninput="document.getElementById('vDescLabel').innerText=this.value+'%';calcularVendedor()">
<div style="text-align:center;font-weight:bold">Desconto: <span id="vDescLabel">10%</span></div>
<div style="display:flex;gap:6px;flex-wrap:wrap;margin:8px 0"><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(0)">0%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(5)">5%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(10)">10%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(15)">15%</button><button class="btn btn-cinza" style="width:auto;padding:8px 14px" onclick="setDesc(20)">20%</button></div>
<label>Comissao (%)</label><input id="vComissao" type="number" value="3" oninput="calcularVendedor()">
<label>Entrada (R$)</label><input id="vEntrada" type="number" value="0" oninput="calcularVendedor()">
<label>Frete + Montagem (R$)</label><input id="vFrete" type="number" value="0" oninput="calcularVendedor()">
<div id="resultadoVend" class="resultado">Selecione um item!</div>
<div id="parcelasVend" style="font-size:13px;margin-top:8px;background:#f8fafc;padding:10px;border-radius:10px"></div>
<button class="btn btn-verde" style="padding:15px;font-size:16px;margin-top:10px" onclick="venderItemAtual()">🛒 VENDER AGORA - FINALIZAR DIRETO</button>
<button class="btn btn-roxo" style="padding:15px;font-size:16px" onclick="enviarProCaixa()">🧾 ENVIAR PRO CAIXA - FINALIZAR NA LOJA</button>
<div class="flex2" style="margin-top:6px"><button class="btn btn-azul" onclick="enviarWhats()">ENVIAR NO WHATS</button><button class="btn btn-cinza" onclick="salvarCalculo()">SALVAR CALCULO</button></div>
<button class="btn btn-cinza" onclick="limparVend()">LIMPAR</button>
</div>
</div>

<div id="modalMeta" class="modal" onclick="if(event.target.id==='modalMeta') fecharModal('modalMeta')">
<div class="modal-box">
<div class="modal-top"><h3>Metas - Dia / Semana / Mes</h3><button class="btn-fechar" onclick="fecharModal('modalMeta')">X</button></div>
<div class="meta-card dia"><h3>☀️ Meta do Dia <span class="badge-auto">EDITAVEL</span></h3><label>Meta do dia (R$)</label><input id="metaDia" type="number" oninput="salvarMetas()"><label>Ja vendeu hoje (R$) - automatico</label><input id="vendidoDia" readonly><div id="contaDia" class="meta-conta"></div><div class="barra-meta"><div id="barraDia">0%</div></div><div class="flex2"><button class="btn btn-cinza" onclick="zerarMeta('dia')">ZERAR DIA</button><button class="btn btn-verde" onclick="abrirModal('modalItens')">VENDER AGORA</button></div></div>
<div class="meta-card semana"><h3>📅 Meta da Semana <span class="badge-auto">EDITAVEL</span></h3><label>Meta da semana (R$)</label><input id="metaSemana" type="number" oninput="salvarMetas()"><label>Ja vendeu na semana (R$) - automatico</label><input id="vendidoSemana" readonly><div id="contaSemana" class="meta-conta"></div><div class="barra-meta"><div id="barraSemana">0%</div></div><button class="btn btn-cinza" onclick="zerarMeta('semana')">ZERAR SEMANA</button></div>
<div class="meta-card mes"><h3>🗓️ Meta do Mes <span class="badge-travado">🔒 TRAVADA</span></h3><div class="cadeado">🔒 META DO MES TRAVADA<br><span id="textoTravaMes">Mes atual: --</span></div><label>Meta do mes (R$)</label><input id="metaMes" type="number" class="travado" readonly onclick="tentarEditarMes()"><label>Ja vendeu no mes (R$) - automatico</label><input id="vendidoMes" readonly><div id="contaMes" class="meta-conta"></div><div class="barra-meta"><div id="barraMes">0%</div></div><button class="btn btn-vermelho" onclick="fecharMes()">FECHAR MES E GERAR RELATORIO</button></div>
<h3>Vendas de Hoje</h3><div id="listaVendasHoje"></div><button class="btn btn-vermelho" onclick="limparVendasHoje()">LIMPAR VENDAS DE HOJE</button><button class="btn btn-verde" onclick="abrirModal('modalRel')">VER RELATORIO COMPLETO</button>
</div>
</div>

<div id="modalRank" class="modal" onclick="if(event.target.id==='modalRank') fecharModal('modalRank')">
<div class="modal-box">
<div class="modal-top"><h3>🏆 Ranking da Equipe</h3><button class="btn-fechar" onclick="fecharModal('modalRank')">X</button></div>
<div id="rankingBox"></div>
<div class="flex2"><button class="btn btn-verde" onclick="enviarRankingWhats()">📱 ENVIAR RANKING NO WHATS</button><button class="btn btn-cinza" onclick="abrirModal('modalVendEquipe')">+ VENDEDOR</button></div>
</div>
</div>

<div id="modalHist" class="modal" onclick="if(event.target.id==='modalHist') fecharModal('modalHist')">
<div class="modal-box">
<div class="modal-top"><h3>Historico de Calculos</h3><button class="btn-fechar" onclick="fecharModal('modalHist')">X</button></div>
<div id="listaHist"></div><button class="btn btn-vermelho" onclick="limparHist()">LIMPAR HISTORICO</button>
</div>
</div>

<div id="modalRel" class="modal" onclick="if(event.target.id==='modalRel') fecharModal('modalRel')">
<div class="modal-box">
<div class="modal-top"><h3>📊 Relatorio</h3><button class="btn-fechar" onclick="fecharModal('modalRel')">X</button></div>
<label>Enviar relatorio pra qual WhatsApp?</label><input id="whatsDestino" placeholder="Ex: 61999999999" maxlength="13">
<div id="relatorioBox"></div>
<div class="flex2" style="margin-top:10px"><button class="btn btn-verde" onclick="enviarRelatorioWhats()">📱 ENVIAR NO WHATSAPP</button><button class="btn btn-escuro" onclick="baixarRelatorioPDF()">📄 BAIXAR EM PDF</button></div>
<button class="btn btn-amarelo" onclick="baixarArquivoRelatorio()">⬇️ BAIXAR ARQUIVO DO RELATORIO</button>
<button class="btn btn-azul" onclick="copiarRelatorio()">📋 COPIAR RELATORIO</button>
<button class="btn btn-cinza" onclick="fecharModal('modalRel')">VOLTAR</button>
</div>
</div>

<script>
// ===== PIX - CHAVE OCULTA =====
var PIX_KEY = "+5561995873892";
var PIX_NOME = "STILLUSCALC PRO";
var PIX_CIDADE = "BRASILIA";
var WHATS_DONO = "5561995873892";
var planoSelecionado = "pro";
var planosInfo = {basico:{nome:"BÁSICO", valor:"49.90", valorNum:49.90, label:"R$ 49,90/mês"}, pro:{nome:"PRO", valor:"89.90", valorNum:89.90, label:"R$ 89,90/mês"}, vitalicio:{nome:"VITALÍCIO", valor:"497.00", valorNum:497.00, label:"R$ 497 uma vez"}};
function crc16(str){var crc=0xFFFF; for(var i=0;i<str.length;i++){crc ^= str.charCodeAt(i)<<8; for(var j=0;j<8;j++){if(crc & 0x8000) crc = ((crc<<1) ^ 0x1021) & 0xFFFF; else crc = (crc<<1) & 0xFFFF;}} return crc.toString(16).toUpperCase().padStart(4,'0');}
function campo(id, val){var s=String(val); return id + String(s.length).padStart(2,'0') + s;}
function gerarPixCopiaECola(valor, txid){var gui = campo("00","BR.GOV.BCB.PIX") + campo("01", PIX_KEY); var merchant = campo("26", gui); var payloadSemCRC = "000201" + merchant + "52040000" + "5303986" + campo("54", valor) + "5802BR" + campo("59", PIX_NOME.substring(0,25)) + campo("60", PIX_CIDADE.substring(0,15)) + campo("62", campo("05", txid)) + "6304"; return payloadSemCRC + crc16(payloadSemCRC);}
function pixAtual(){var info=planosInfo[planoSelecionado]; var txid="STILLUS"+Date.now().toString().slice(-8); return gerarPixCopiaECola(info.valor, txid);}
var pixAtualCodigo = "";
function selecionarPlano(p){planoSelecionado=p; document.getElementById('cardBasico').classList.remove('selecionado'); document.getElementById('cardPro').classList.remove('selecionado'); document.getElementById('cardVitalicio').classList.remove('selecionado'); if(p==='basico') document.getElementById('cardBasico').classList.add('selecionado'); if(p==='pro') document.getElementById('cardPro').classList.add('selecionado'); if(p==='vitalicio') document.getElementById('cardVitalicio').classList.add('selecionado'); var info=planosInfo[p]; document.getElementById('btnPagarPlano').innerText="💳 PAGAR COM PIX - PLANO "+info.nome+" - "+info.label; document.getElementById('areaPagamento').style.display='none';}
function mostrarPagamento(){var info=planosInfo[planoSelecionado]; pixAtualCodigo = pixAtual(); document.getElementById('tituloPagamento').innerText="Pagamento - Plano "+info.nome+" - "+info.label; document.getElementById('imgQR').src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data="+encodeURIComponent(pixAtualCodigo); document.getElementById('areaPagamento').style.display='block'; document.getElementById('areaPagamento').scrollIntoView({behavior:'smooth'});}
function copiarPix(){if(!pixAtualCodigo) pixAtualCodigo=pixAtual(); navigator.clipboard.writeText(pixAtualCodigo).then(function(){alert('Código Pix copiado! ✅\n\nAgora abra o app do seu banco, escolha Pix Copia e Cola e cole o código.');});}
function enviarComprovanteWhats(){var info=planosInfo[planoSelecionado]; var msg="Olá! Acabei de pagar o StillusCalc PRO - Plano "+info.nome+" - "+info.label+" - Loja: "+(loja?loja.nome:"")+". Segue meu comprovante! Quero meu código de liberação."; var url="https://wa.me/"+WHATS_DONO+"?text="+encodeURIComponent(msg); window.open(url,'_blank');}
function getLicenca(){try{return JSON.parse(localStorage.getItem('stilluscalc_licenca')||'null');}catch(e){return null;}}
function salvarLicenca(l){try{localStorage.setItem('stilluscalc_licenca', JSON.stringify(l));}catch(e){}}
function getDataInstalacao(){var d=localStorage.getItem('stilluscalc_instalacao'); if(!d){d=new Date().toISOString(); try{localStorage.setItem('stilluscalc_instalacao', d);}catch(e){}} return new Date(d);}
function diasRestantesTeste(){var inst=getDataInstalacao(); var agora=new Date(); var diff=Math.floor((agora-inst)/(1000*60*60*24)); return Math.max(0, 7-diff);}
function estaLiberado(){var lic=getLicenca(); if(lic && lic.tipo==='vitalicio') return true; if(lic && lic.expira){var exp=new Date(lic.expira); if(new Date() < exp) return true;} if(diasRestantesTeste()>0) return true; return false;}
function atualizarStatusPlano(){var lic=getLicenca(); var box=document.getElementById('statusPlanoBox'); if(!box) return; var pill=document.getElementById('pillTeste'); if(lic && lic.tipo==='vitalicio'){box.innerHTML="💎 <b>PLANO VITALÍCIO ATIVO</b><br>Você tem acesso pra sempre! Obrigado! 🎉"; if(pill){pill.innerText="💎 VITALÍCIO"; pill.style.background="#7c3aed"; pill.style.color="#fff";} return;} if(lic && lic.expira && new Date() < new Date(lic.expira)){var dias=Math.ceil((new Date(lic.expira)-new Date())/(1000*60*60*24)); box.innerHTML="✅ <b>PLANO "+lic.plano.toUpperCase()+" ATIVO</b><br>Faltam "+dias+" dias. Vence em "+new Date(lic.expira).toLocaleDateString('pt-BR'); if(pill){pill.innerText="✅ "+lic.plano.toUpperCase()+" - "+dias+" dias"; pill.style.background="#22c55e"; pill.style.color="#fff";} return;} var rest=diasRestantesTeste(); if(rest>0){box.innerHTML="🎁 <b>TESTE GRÁTIS - Faltam "+rest+" dias</b><br>Você está usando tudo liberado! Depois escolha um plano para continuar."; if(pill){pill.innerText="🎁 TESTE GRÁTIS: "+rest+" dias"; pill.style.background="#22c55e"; pill.style.color="#fff";}} else {box.innerHTML="🔒 <b>SEU TESTE ACABOU!</b><br>Escolha um plano abaixo para continuar usando o StillusCalc PRO."; if(pill){pill.innerText="🔒 TESTE ACABOU - ASSINAR"; pill.style.background="#ef4444"; pill.style.color="#fff";}}}
function verificarTravaEAbrir(id, btn){if(!usuarioLogado){abrirModal('modalLogin'); return;} if(!estaLiberado()){abrirModal('modalPlanos'); return;} if(id==='modalVendEquipe' && usuarioLogado.tipo!=='dono'){alert('Só o DONO pode cadastrar vendedores!'); return;} if(id==='modalLoja' && usuarioLogado.tipo!=='dono'){alert('Só o DONO pode mudar dados da loja!'); return;} abrirModal(id, btn);}
function validarCodigo(){var cod=document.getElementById('codigoLiberacao').value.trim().toUpperCase(); var mapa={"BASICO-30-STILLUS":{plano:"basico", tipo:"mensal", dias:30}, "PRO-30-STILLUS":{plano:"pro", tipo:"mensal", dias:30}, "VITALICIO-STILLUS-PRO":{plano:"vitalicio", tipo:"vitalicio", dias:0}}; if(!mapa[cod]){alert('Código inválido! Confira com o dono e tente de novo.'); return;} var info=mapa[cod]; var lic={plano:info.plano, tipo:info.tipo, expira:""}; if(info.tipo==='mensal'){var exp=new Date(); exp.setDate(exp.getDate()+info.dias); lic.expira=exp.toISOString();} salvarLicenca(lic); atualizarStatusPlano(); alert('LIBERADO! ✅\n\nPlano '+info.plano.toUpperCase()+' ativado!'); fecharModal('modalPlanos');}
var deferredPrompt=null;
window.addEventListener('beforeinstallprompt',function(e){e.preventDefault(); deferredPrompt=e; var b=document.getElementById('btnInstalar'); if(b) b.style.display='inline-block';});
function instalarApp(){if(deferredPrompt){deferredPrompt.prompt(); deferredPrompt.userChoice.then(function(){deferredPrompt=null; document.getElementById('btnInstalar').style.display='none';});} else {alert('Para instalar: No Chrome, 3 pontinhos > Adicionar a tela inicial / Instalar app. No iPhone: Compartilhar > Adicionar a Tela de Inicio');}}
function esc(s){return String(s==null?'':s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');}
function fmt(v){return (Number(v)||0).toLocaleString('pt-BR',{style:'currency',currency:'BRL'});}
function limparTexto(s,max){return String(s||'').replace(/<[^>]*>/g,'').trim().slice(0,max||200);}
function abrirModal(id,btn){var m=document.getElementById(id); if(!m) return; m.classList.add('aberto'); if(id==='modalRel') renderRelatorio(); if(id==='modalRank') renderRanking(); if(id==='modalGrafico') renderGrafico(); if(id==='modalSync') atualizarStatusSync(); if(id==='modalCaixa') renderCaixa(); if(id==='modalChat'){renderClientes(); renderChat();} if(id==='modalRobo') renderRobo(); if(id==='modalEnviarProduto') renderProdutosChat(); if(id==='modalPlanos'){atualizarStatusPlano();} if(id==='modalVendEquipe'){renderVendedores(); renderListaLogins();} if(id==='modalLoja'){var c=document.getElementById('cfgCodigoLoja'); if(c) c.value=loja.codigoLoja;} if(btn){var tabs=document.querySelectorAll('.tab'); tabs.forEach(function(t){t.classList.remove('ativo')}); btn.classList.add('ativo'); btn.scrollIntoView({behavior:'smooth',inline:'center',block:'nearest'});}}
function fecharModal(id){var m=document.getElementById(id); if(m) m.classList.remove('aberto'); if(id==='modalLogin') return; var tabs=document.querySelectorAll('.tab'); tabs.forEach(function(t){t.classList.remove('ativo')});}
function mesAtualStr(){var d=new Date(); return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0');}
function nomeMesAtual(){var d=new Date(); return d.toLocaleDateString('pt-BR',{month:'long',year:'numeric'});}
function limparNumeroWhats(s){return String(s||'').replace(/\D/g,'');}
function abrirWhatsComTexto(texto, numeroDestino){var num=limparNumeroWhats(numeroDestino||''); var url=''; if(num && num.length>=10){var n=num; if(n.length===11||n.length===10) n='55'+n; url='https://wa.me/'+n+'?text='+encodeURIComponent(texto);} else {url='https://wa.me/?text='+encodeURIComponent(texto);} if(navigator.share){navigator.share({text:texto}).then(function(){}).catch(function(){window.open(url,'_blank');});} else {window.open(url,'_blank');}}
// ===== DADOS =====
var loja=null; try{loja=JSON.parse(localStorage.getItem('stilluscalc_loja')||'null');}catch(e){loja=null;}
if(!loja){loja={nome:'Minha Loja', whats:'', slogan:'O barato e aqui!', tipo:'Moveis e Eletrodomesticos', codigoLoja:'LOJA-'+Math.random().toString(36).slice(2,7).toUpperCase()};}
if(!loja.codigoLoja) loja.codigoLoja='LOJA-'+Math.random().toString(36).slice(2,7).toUpperCase();
var vendedores=[]; try{vendedores=JSON.parse(localStorage.getItem('stilluscalc_vendedores')||'[]');}catch(e){vendedores=[];}
if(!vendedores.length){vendedores=['Vendedor 1','Vendedor 2'];}
var loginsVendedores=[]; try{loginsVendedores=JSON.parse(localStorage.getItem('stilluscalc_logins')||'[]');}catch(e){loginsVendedores=[];}
if(!loginsVendedores.length){loginsVendedores=[{nome:'Maria Teste', login:'maria', senha:'1234', codigoLoja:'LOJA-TESTE'}];}
var vendedorAtual=''; try{vendedorAtual=localStorage.getItem('stilluscalc_vendedorAtual')||vendedores[0];}catch(e){vendedorAtual=vendedores[0];}
var usuarioLogado=null; try{usuarioLogado=JSON.parse(localStorage.getItem('stilluscalc_usuario')||'null');}catch(e){usuarioLogado=null;}
var itens=[]; try{itens=JSON.parse(localStorage.getItem('stilluscalc_itens')||'[]');}catch(e){itens=[];}
if(!itens.length){var a={}; a.nome='Produto Exemplo - Sofa'; a.codigo='001'; a.preco=1789; a.custo=1200; a.cat='Produto Geral'; a.foto=''; itens.push(a);}
var historico=[]; try{historico=JSON.parse(localStorage.getItem('stilluscalc_hist')||'[]');}catch(e){historico=[];}
var metas=null; try{metas=JSON.parse(localStorage.getItem('stilluscalc_metas')||'null');}catch(e){metas=null;}
if(!metas){metas={dia:3000, vendidoDia:0, semana:15000, vendidoSemana:0, mes:60000, vendidoMes:0, mesRef:mesAtualStr()};}
if(!metas.mesRef) metas.mesRef=mesAtualStr();
var vendasHoje=[]; try{vendasHoje=JSON.parse(localStorage.getItem('stilluscalc_vendas')||'[]');}catch(e){vendasHoje=[];}
var relatorios=[]; try{relatorios=JSON.parse(localStorage.getItem('stilluscalc_relatorios')||'[]');}catch(e){relatorios=[];}
var clientes=[]; try{clientes=JSON.parse(localStorage.getItem('stilluscalc_clientes')||'[]');}catch(e){clientes=[];}
if(!clientes.length){clientes=[{nome:'Cliente Exemplo - Joao', msgs:[{tipo:'cliente', texto:'Oi, tem sofa em promocao?', hora:'08:00'}, {tipo:'eu', texto:'Tem sim! Olha esse aqui 👇', hora:'08:01'}]}];}
var clienteAtivo=0;
var caixa=[]; try{caixa=JSON.parse(localStorage.getItem('stilluscalc_caixa')||'[]');}catch(e){caixa=[];}
var roboLigado=false; try{roboLigado=localStorage.getItem('stilluscalc_robo')==='1';}catch(e){}
var roboRespostas=null; try{roboRespostas=JSON.parse(localStorage.getItem('stilluscalc_roboRespostas')||'null');}catch(e){roboRespostas=null;}
if(!roboRespostas){roboRespostas={oi:'Ola! Bem-vindo(a) a {LOJA}! 😊 Sou o assistente virtual. Como posso te ajudar hoje?', preco:'Esse produto esta por {PRECO}! E hoje consigo um desconto especial so pra voce! Quer que eu reserve?', desconto:'Consigo 10% de desconto so pra voce hoje! 🔥 De {PRECO} por {PRECO_DESC} - quer que eu reserve?', entrega:'Sim! Fazemos entrega e montagem! 🚚 Me passa seu endereco que eu calculo na hora.', parcela:'Parcela sim! Em ate 12x no cartao! 💳 Quer que eu simule?', estoque:'Tem sim em estoque! ✅ Quer que eu reserve pra voce?'};}
var fotoTemp=''; var modoAtual='vend'; var expr='';
function salvar(){try{localStorage.setItem('stilluscalc_loja',JSON.stringify(loja)); localStorage.setItem('stilluscalc_vendedores',JSON.stringify(vendedores)); localStorage.setItem('stilluscalc_vendedorAtual',vendedorAtual); localStorage.setItem('stilluscalc_itens',JSON.stringify(itens)); localStorage.setItem('stilluscalc_hist',JSON.stringify(historico)); localStorage.setItem('stilluscalc_metas',JSON.stringify(metas)); localStorage.setItem('stilluscalc_vendas',JSON.stringify(vendasHoje)); localStorage.setItem('stilluscalc_relatorios',JSON.stringify(relatorios)); localStorage.setItem('stilluscalc_clientes',JSON.stringify(clientes)); localStorage.setItem('stilluscalc_caixa',JSON.stringify(caixa)); localStorage.setItem('stilluscalc_robo', roboLigado?'1':'0'); localStorage.setItem('stilluscalc_roboRespostas', JSON.stringify(roboRespostas)); localStorage.setItem('stilluscalc_logins', JSON.stringify(loginsVendedores)); if(usuarioLogado) localStorage.setItem('stilluscalc_usuario', JSON.stringify(usuarioLogado)); else localStorage.removeItem('stilluscalc_usuario');}catch(e){}}
// ===== LOGIN =====
function setAbaLogin(tipo){document.getElementById('abaDono').classList.toggle('ativo', tipo==='dono'); document.getElementById('abaVend').classList.toggle('ativo', tipo==='vend'); document.getElementById('boxLoginDono').style.display=tipo==='dono'?'block':'none'; document.getElementById('boxLoginVend').style.display=tipo==='vend'?'block':'none';}
function atualizarPillUsuario(){var pill=document.getElementById('pillUsuario'); if(!pill) return; if(!usuarioLogado){pill.innerText='👤 Nao logado'; return;} if(usuarioLogado.tipo==='dono'){pill.innerText='👑 DONO: '+usuarioLogado.nome+' | '+loja.codigoLoja;} else {pill.innerText='👤 VENDEDOR: '+usuarioLogado.nome+' | '+usuarioLogado.codigoLoja;}}
function entrarComoDono(){var nome=limparTexto(document.getElementById('loginLojaNome').value,60); var whats=limparNumeroWhats(document.getElementById('loginDonoWhats').value); var codigo=document.getElementById('loginCodigoDono').value.trim().toUpperCase(); if(!nome){alert('Coloca o nome da sua loja, dono!'); return;} loja.nome=nome; if(whats) loja.whats=whats; if(codigo){var mapa={"BASICO-30-STILLUS":{plano:"basico", tipo:"mensal", dias:30}, "PRO-30-STILLUS":{plano:"pro", tipo:"mensal", dias:30}, "VITALICIO-STILLUS-PRO":{plano:"vitalicio", tipo:"vitalicio", dias:0}}; if(!mapa[codigo]){alert('Codigo invalido! Tenta de novo ou deixa em branco para usar o teste gratis.'); return;} var info=mapa[codigo]; var lic={plano:info.plano, tipo:info.tipo, expira:""}; if(info.tipo==='mensal'){var exp=new Date(); exp.setDate(exp.getDate()+info.dias); lic.expira=exp.toISOString();} salvarLicenca(lic);} usuarioLogado={tipo:'dono', nome:nome, codigoLoja:loja.codigoLoja}; vendedorAtual=nome; salvar(); atualizarPillUsuario(); renderLoja(); renderVendedores(); fecharModal('modalLogin'); alert('Bem-vindo, DONO! 👑\nLoja: '+loja.nome+'\nCodigo da loja: '+loja.codigoLoja+'\n\nPasse esse codigo + login + senha para seus vendedores entrarem.');}
function entrarComoVendedor(){var codigo=document.getElementById('loginCodigoLoja').value.trim().toUpperCase(); var login=limparTexto(document.getElementById('loginVendLogin').value,30).toLowerCase(); var senha=document.getElementById('loginVendSenha').value.trim(); if(!codigo||!login||!senha){alert('Preenche Codigo da Loja, Login e Senha!'); return;} var ach=null; for(var i=0;i<loginsVendedores.length;i++){if(loginsVendedores[i].login.toLowerCase()===login && loginsVendedores[i].senha===senha){if(loginsVendedores[i].codigoLoja.toUpperCase()===codigo || codigo==='LOJA-TESTE'){ach=loginsVendedores[i]; break;}}} if(!ach){alert('Login ou senha errados, ou codigo da loja errado!\n\nConfere com o dono: Codigo da Loja + Login + Senha.'); return;} usuarioLogado={tipo:'vend', nome:ach.nome, login:ach.login, codigoLoja:codigo}; vendedorAtual=ach.nome; if(!vendedores.includes(ach.nome)) vendedores.push(ach.nome); salvar(); atualizarPillUsuario(); renderLoja(); renderVendedores(); fecharModal('modalLogin'); alert('Bem-vindo, '+ach.nome+'! 👤\n\nVoce entrou direto na calculadora.\nBoas vendas! 🛒');}
function entrarTesteVendedor(){document.getElementById('loginCodigoLoja').value='LOJA-TESTE'; document.getElementById('loginVendLogin').value='maria'; document.getElementById('loginVendSenha').value='1234'; entrarComoVendedor();}
function sairLogin(){if(!confirm('Sair e trocar de usuario?')) return; usuarioLogado=null; salvar(); atualizarPillUsuario(); abrirModal('modalLogin');}
function concluirBoasVindas(){var nomeLoja=limparTexto(document.getElementById('bvLoja').value,60); var whats=limparNumeroWhats(document.getElementById('bvWhats').value); var vendsStr=limparTexto(document.getElementById('bvVends').value,120); var metaMes=parseFloat(document.getElementById('bvMetaMes').value)||0; if(!nomeLoja){alert('Coloca o nome da sua loja!'); return;} loja.nome=nomeLoja; loja.whats=whats; if(metaMes>0) metas.mes=metaMes; if(vendsStr){var arr=vendsStr.split(','); var novos=[]; for(var i=0;i<arr.length;i++){var n=arr[i].trim(); if(n) novos.push(n);} if(novos.length){vendedores=novos; vendedorAtual=novos[0];}} try{localStorage.setItem('stilluscalc_jaViuBoasVindas','1');}catch(e){} usuarioLogado={tipo:'dono', nome:nomeLoja, codigoLoja:loja.codigoLoja}; salvar(); atualizarPillUsuario(); renderLoja(); renderVendedores(); renderMetas(); fecharModal('modalBoasVindas'); alert('Pronto! Seus 7 dias grátis começaram! 🎉');}
function addCliente(){var n=limparTexto(document.getElementById('novoClienteNome').value,50); if(!n){alert('Digite o nome do cliente!'); return;} clientes.push({nome:n, msgs:[{tipo:'eu', texto:'Ola '+n+'! Bem-vindo(a) a '+loja.nome+'! 😊 Como posso te ajudar?', hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}]}); document.getElementById('novoClienteNome').value=''; clienteAtivo=clientes.length-1; salvar(); renderClientes(); renderChat();}
function renderClientes(){var div=document.getElementById('listaClientes'); if(!div) return; div.innerHTML=''; if(!clientes.length) div.innerHTML='<p style="font-size:13px;padding:8px">Nenhum cliente ainda.</p>'; for(var i=0;i<clientes.length;i++){var c=clientes[i]; var last=c.msgs.length? c.msgs[c.msgs.length-1].texto:'...'; var letra=c.nome.charAt(0).toUpperCase(); div.innerHTML+='<div class="cliente-item" onclick="selecionarCliente('+i+')"><div class="av">'+esc(letra)+'</div><div style="flex:1;min-width:0"><b>'+esc(c.nome)+'</b><br><small style="color:#888">'+esc(last.slice(0,50))+'</small></div><span style="font-size:16px">💬</span></div>';}}
function selecionarCliente(i){clienteAtivo=i; renderChat(); renderClientes();}
function renderChat(){var c=clientes[clienteAtivo]; if(!c) return; document.getElementById('chatClienteNome').innerText=c.nome; document.getElementById('chatAvatar').innerText=c.nome.charAt(0).toUpperCase(); document.getElementById('chatClienteStatus').innerText='Vendedor: '+vendedorAtual+' | '+loja.nome; document.getElementById('chatRoboStatus').innerText=roboLigado?'Robo ON 🤖':'Robo OFF'; document.getElementById('btnRobo').innerText=roboLigado?'🤖 ROBO: LIGADO ✅':'🤖 ROBO: DESLIGADO'; var box=document.getElementById('chatBox'); box.innerHTML=''; for(var i=0;i<c.msgs.length;i++){var m=c.msgs[i]; var cls=m.tipo==='eu'?'eu':m.tipo==='robo'?'robo':'cliente'; var nome=m.tipo==='robo'?'🤖 Robo':m.tipo==='eu'?'Voce':esc(c.nome); var midia=''; if(m.foto) midia+='<img src="'+esc(m.foto)+'">'; if(m.video) midia+='<video src="'+esc(m.video)+'" controls></video>'; var prod=''; if(m.produto){prod='<div class="prod-card">'+(m.produto.foto?'<img src="'+esc(m.produto.foto)+'">':'')+'<b>'+esc(m.produto.nome)+'</b><br>De <s>'+fmt(m.produto.preco)+'</s> por <b style="color:#22c55e">'+fmt(m.produto.preco*0.9)+'</b></div>';} box.innerHTML+='<div class="msg '+cls+'"><b style="font-size:11px">'+nome+'</b><br>'+esc(m.texto)+midia+prod+'<small>'+esc(m.hora||'')+'</small></div>';} box.scrollTop=box.scrollHeight;}
function toggleEmoji(){var p=document.getElementById('emojiPanel'); if(p.style.display==='none'){var emojis=['😀','😂','😍','👍','👏','🔥','💰','🛍️','🛋️','📱','🚚','💳','✅','❤️','😊','🎉','👋','🙏','💪','⭐','🏆','📦','🤑','😉']; p.innerHTML=''; for(var i=0;i<emojis.length;i++){p.innerHTML+='<span onclick="addEmoji(\''+emojis[i]+'\')">'+emojis[i]+'</span>';} p.style.display='flex';} else {p.style.display='none';}}
function addEmoji(e){document.getElementById('chatInput').value+=e; document.getElementById('chatInput').focus();}
function enviarMsgChat(){var inp=document.getElementById('chatInput'); var txt=limparTexto(inp.value,500); if(!txt) return; var c=clientes[clienteAtivo]; if(!c) return; c.msgs.push({tipo:'eu', texto:txt, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); inp.value=''; document.getElementById('emojiPanel').style.display='none'; salvar(); renderChat(); renderClientes();}
function enviarMidiaChat(input){var f=input.files[0]; if(!f) return; var c=clientes[clienteAtivo]; if(!c) return; var r=new FileReader(); r.onload=function(e){var isVideo=f.type.indexOf('video')>-1; var m={tipo:'eu', texto:isVideo?'🎥 Video do produto!':'📸 Foto do produto!', hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}; if(isVideo) m.video=e.target.result; else m.foto=e.target.result; c.msgs.push(m); salvar(); renderChat();}; r.readAsDataURL(f);}
function renderProdutosChat(){var div=document.getElementById('listaProdutosChat'); div.innerHTML=''; for(var i=0;i<itens.length;i++){var it=itens[i]; div.innerHTML+='<div class="item-cad"><div class="ft">'+(it.foto?'<img src="'+esc(it.foto)+'">':'🛍️')+'</div><div class="info"><b>'+esc(it.nome)+'</b><br><b>'+fmt(it.preco)+'</b></div><button class="btn btn-verde" style="width:auto;padding:8px 12px" onclick="enviarProdutoChat('+i+')">ENVIAR NO CHAT</button></div>';}}
function enviarProdutoChat(idx){var it=itens[idx]; var c=clientes[clienteAtivo]; if(!c) return; c.msgs.push({tipo:'eu', texto:'Olha esse produto! 👇', produto:it, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat(); fecharModal('modalEnviarProduto'); abrirModal('modalChat');}
function simularCliente(){var c=clientes[clienteAtivo]; if(!c) return; var frases=['Oi, qual o preco desse sofa?','Tem desconto?','Voce faz entrega?','Parcela no cartao?','Tem em estoque?']; var f=frases[Math.floor(Math.random()*frases.length)]; c.msgs.push({tipo:'cliente', texto:f, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat(); if(roboLigado){setTimeout(function(){respostaRobo(f);},800);}}
function respostaRobo(textoCliente){var c=clientes[clienteAtivo]; if(!c) return; var t=textoCliente.toLowerCase(); var resp=''; var ultimoPreco=itens.length? itens[0].preco:1789; if(t.indexOf('preco')>-1||t.indexOf('valor')>-1||t.indexOf('quanto')>-1){resp=roboRespostas.preco.replace('{PRECO}', fmt(ultimoPreco));} else if(t.indexOf('desconto')>-1){resp=roboRespostas.desconto.replace('{PRECO}', fmt(ultimoPreco)).replace('{PRECO_DESC}', fmt(ultimoPreco*0.9));} else if(t.indexOf('entrega')>-1||t.indexOf('frete')>-1){resp=roboRespostas.entrega;} else if(t.indexOf('parcela')>-1||t.indexOf('cartao')>-1){resp=roboRespostas.parcela;} else if(t.indexOf('tem')>-1||t.indexOf('estoque')>-1){resp=roboRespostas.estoque;} else if(t.indexOf('oi')>-1||t.indexOf('ola')>-1||t.indexOf('bom dia')>-1){resp=roboRespostas.oi.replace('{LOJA}', loja.nome);} else {resp='Entendi! Um vendedor vai te atender agora! 😊';} c.msgs.push({tipo:'robo', texto:resp, hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat();}
function toggleRobo(){roboLigado=!roboLigado; salvar(); renderChat(); alert(roboLigado?'Robo LIGADO! 🤖':'Robo DESLIGADO.');}
function renderRobo(){document.getElementById('roboOi').value=roboRespostas.oi; document.getElementById('roboPreco').value=roboRespostas.preco; document.getElementById('roboDesconto').value=roboRespostas.desconto; document.getElementById('roboEntrega').value=roboRespostas.entrega; document.getElementById('roboParcela').value=roboRespostas.parcela; document.getElementById('roboEstoque').value=roboRespostas.estoque;}
function salvarRobo(){roboRespostas.oi=document.getElementById('roboOi').value; roboRespostas.preco=document.getElementById('roboPreco').value; roboRespostas.desconto=document.getElementById('roboDesconto').value; roboRespostas.entrega=document.getElementById('roboEntrega').value; roboRespostas.parcela=document.getElementById('roboParcela').value; roboRespostas.estoque=document.getElementById('roboEstoque').value; salvar(); fecharModal('modalRobo'); alert('Robo salvo!');}
function comecarVendaNoChat(){var c=clientes[clienteAtivo]; if(!c) return; document.getElementById('vCliente').value=c.nome; var nomeProd=itens.length? itens[0].nome+' ('+itens[0].codigo+')':''; document.getElementById('vNome').value=nomeProd; if(itens.length){document.getElementById('vCodigo').value=itens[0].codigo; document.getElementById('vPreco').value=itens[0].preco; document.getElementById('vCusto').value=itens[0].custo;} calcularVendedor(); c.msgs.push({tipo:'eu', texto:'Perfeito! Ja estou preparando sua venda! 🛒 Vou mandar pro caixa!', hora:new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})}); salvar(); renderChat(); fecharModal('modalChat'); abrirModal('modalVend');}
function enviarChatWhatsApp(){var c=clientes[clienteAtivo]; if(!c) return; var msg='Conversa '+loja.nome+' - Cliente: '+c.nome+'\n\n'; for(var i=0;i<c.msgs.length;i++){var m=c.msgs[i]; var quem=m.tipo==='eu'?'Vendedor':m.tipo==='robo'?'Robo':c.nome; msg+=quem+': '+m.texto+'\n';} abrirWhatsComTexto(msg, loja.whats);}
function enviarProCaixa(){var nome=document.getElementById('vNome').value||'Produto'; var preco=parseFloat(document.getElementById('vPreco').value); var desc=parseFloat(document.getElementById('vDesc').value)||0; var frete=parseFloat(document.getElementById('vFrete').value)||0; var vend=document.getElementById('vVendedor').value||vendedorAtual; var cliente=document.getElementById('vCliente').value||'Cliente Balcao'; if(!preco){alert('Selecione um item!'); return;} var final=preco*(1-desc/100)+frete; var item={id:Date.now(), nome:nome, valor:final, vendedor:vend, cliente:cliente, data:new Date().toLocaleString('pt-BR'), status:'aguardando', formaPagamento:''}; caixa.push(item); salvar(); renderCaixa(); fecharModal('modalVend'); abrirModal('modalCaixa'); alert('Enviado pro CAIXA! 🧾\n'+nome+' - '+fmt(final)+'\nCliente: '+cliente); }
function renderCaixa(){var pend=caixa.filter(function(x){return x.status==='aguardando';}); var fin=caixa.filter(function(x){return x.status==='finalizado';}); var totalPend=pend.reduce(function(s,x){return s+x.valor;},0); var totalFin=fin.reduce(function(s,x){return s+x.valor;},0); document.getElementById('resumoCaixa').innerHTML='🧾 CAIXA - '+esc(loja.nome)+'<br>Aguardando: <b>'+pend.length+' - '+fmt(totalPend)+'</b> | Finalizados: <b>'+fin.length+' - '+fmt(totalFin)+'</b>'; var div=document.getElementById('listaCaixa'); div.innerHTML=''; if(!pend.length) div.innerHTML='<p style="font-size:13px">Nenhuma venda aguardando.</p>'; for(var i=0;i<pend.length;i++){var it=pend[i]; div.innerHTML+='<div class="caixa-item aguardando"><b>🛒 '+esc(it.nome)+'</b><br>Cliente: <b>'+esc(it.cliente)+'</b> | Vendedor: <b>'+esc(it.vendedor)+'</b><br>Valor: <b style="font-size:18px">'+fmt(it.valor)+'</b><br><label style="margin-top:6px">Forma de pagamento:</label><select id="pag-'+it.id+'"><option>Pix</option><option>Dinheiro</option><option>Cartao Credito</option><option>Cartao Debito</option><option>Boleto</option></select><div class="flex2"><button class="btn btn-verde" onclick="finalizarCaixa('+it.id+')">✅ FINALIZAR / RECEBER</button><button class="btn btn-vermelho" onclick="cancelarCaixa('+it.id+')">❌ CANCELAR</button></div></div>';} var div2=document.getElementById('listaCaixaFinalizados'); div2.innerHTML=''; for(var j=0;j<fin.slice().reverse().length;j++){var f=fin.slice().reverse()[j]; div2.innerHTML+='<div class="caixa-item finalizado">✅ <b>'+esc(f.nome)+'</b> - '+fmt(f.valor)+'<br><small>'+esc(f.cliente)+' | '+esc(f.vendedor)+' | '+esc(f.formaPagamento)+'</small></div>';} if(!fin.length) div2.innerHTML='<p style="font-size:13px">Nenhuma venda finalizada ainda.</p>';}
function finalizarCaixa(id){var idx=-1; for(var i=0;i<caixa.length;i++){if(caixa[i].id===id){idx=i;break;}} if(idx<0) return; var it=caixa[idx]; var forma=document.getElementById('pag-'+id).value; if(!confirm('Finalizar venda de '+it.nome+' por '+fmt(it.valor)+'?\nCliente: '+it.cliente+'\nPagamento: '+forma)) return; it.status='finalizado'; it.formaPagamento=forma; registrarVendaAutomatica(it.nome, it.valor, it.vendedor); salvar(); renderCaixa(); alert('Venda FINALIZADA! ✅\n'+fmt(it.valor)+' via '+forma); }
function cancelarCaixa(id){if(!confirm('Cancelar essa venda?')) return; for(var i=0;i<caixa.length;i++){if(caixa[i].id===id){caixa[i].status='cancelado'; break;}} salvar(); renderCaixa();}
function atualizarStatusSync(){document.getElementById('codigoLoja').value=loja.codigoLoja+' - '+loja.nome; var el=document.getElementById('boxCodigoLojaVendedor'); if(el){el.innerHTML='<b>Passe para seus vendedores:</b><br>Codigo da Loja: <b>'+esc(loja.codigoLoja)+'</b><br>Link: <b>https://stilluscalc-pro.netlify.app</b><br>Cada vendedor entra com o login e senha que voce cadastrou.';} var total=vendasHoje.length; var val=vendasHoje.reduce(function(s,v){return s+(v.valor||0);},0); document.getElementById('statusSync').innerText='Loja: '+loja.nome+' | Vendas: '+total+' - '+fmt(val);}
function gerarLinkLoja(){var dados={loja:loja, vendedores:vendedores, itens:itens, metas:metas, logins:loginsVendedores}; var codigo=btoa(unescape(encodeURIComponent(JSON.stringify(dados)))); var base=location.href.split('?')[0].split('#')[0]; var link=base+'?loja='+encodeURIComponent(codigo); document.getElementById('codigoLoja').value=link; navigator.clipboard.writeText(link).then(function(){alert('Link copiado!');}); return link;}
function copiarLinkLoja(){var l=gerarLinkLoja(); navigator.clipboard.writeText(l);}
function enviarLinkLojaWhats(){var l=gerarLinkLoja(); var msg='Ola! Entra na nossa loja no StillusCalc PRO 🏪 '+loja.nome+'\n\nCodigo da Loja: '+loja.codigoLoja+'\nClica no link:\n'+l; abrirWhatsComTexto(msg, loja.whats);}
function tentarEntrarViaLink(){var params=new URLSearchParams(location.search); var cod=params.get('loja'); if(!cod) return; try{var dados=JSON.parse(decodeURIComponent(escape(atob(cod)))); if(dados.loja && confirm('Entrar na loja '+dados.loja.nome+'?')){loja=dados.loja; vendedores=dados.vendedores||vendedores; itens=dados.itens||itens; if(dados.metas) metas=dados.metas; if(dados.logins) loginsVendedores=dados.logins; vendedorAtual=vendedores[0]; try{localStorage.setItem('stilluscalc_jaViuBoasVindas','1');}catch(e){} salvar(); renderLoja(); renderVendedores(); renderItens(); renderMetas(); alert('Voce entrou na loja '+loja.nome+'! Agora faca login com seu login e senha.');}}catch(e){}}
function gerarCodigoVendas(){var minhas=vendasHoje.filter(function(v){return v.vendedor===vendedorAtual;}); var payload={tipo:'STILLUS_VENDAS', loja:loja.codigoLoja, lojaNome:loja.nome, vendedor:vendedorAtual, vendas:minhas, data:new Date().toLocaleString('pt-BR')}; return 'STILLUS-'+btoa(unescape(encodeURIComponent(JSON.stringify(payload))));}
function enviarVendasWhats(){var codigo=gerarCodigoVendas(); var minhas=vendasHoje.filter(function(v){return v.vendedor===vendedorAtual;}); var total=minhas.reduce(function(s,v){return s+(v.valor||0);},0); var msg='🔄 SINCRONIZACAO StillusCalc PRO - '+loja.nome+'\nVendedor: '+vendedorAtual+'\nVendas: '+minhas.length+' - Total: '+fmt(total)+'\n\nCole esse codigo no app do dono:\n\n'+codigo; abrirWhatsComTexto(msg, loja.whats);}
function receberVendas(){var txt=document.getElementById('codigoReceber').value.trim(); if(!txt){alert('Cole o codigo!'); return;} try{var codigo=txt.replace('STILLUS-','').trim(); var payload=JSON.parse(decodeURIComponent(escape(atob(codigo)))); if(payload.tipo!=='STILLUS_VENDAS'){alert('Codigo invalido!'); return;} var novas=0; for(var i=0;i<payload.vendas.length;i++){var v=payload.vendas[i]; var ja=false; for(var j=0;j<vendasHoje.length;j++){if(vendasHoje[j].nome===v.nome && vendasHoje[j].valor===v.valor && vendasHoje[j].data===v.data && vendasHoje[j].vendedor===v.vendedor){ja=true;break;}} if(!ja){vendasHoje.push(v); metas.vendidoDia+=v.valor; metas.vendidoSemana+=v.valor; metas.vendidoMes+=v.valor; novas++;}} if(!vendedores.includes(payload.vendedor)) vendedores.push(payload.vendedor); salvar(); renderMetas(); renderRanking(); renderGrafico(); document.getElementById('codigoReceber').value=''; alert('Recebido! '+novas+' vendas novas'); abrirModal('modalGrafico'); }catch(e){alert('Nao consegui ler esse codigo!');}}
function calcRanking(){var map={}; for(var i=0;i<vendedores.length;i++){map[vendedores[i]]={nome:vendedores[i], total:0, qtd:0};} for(var j=0;j<vendasHoje.length;j++){var v=vendasHoje[j]; if(!map[v.vendedor]) map[v.vendedor]={nome:v.vendedor,total:0,qtd:0}; map[v.vendedor].total+=v.valor; map[v.vendedor].qtd+=1;} var arr=[]; for(var k in map) arr.push(map[k]); arr.sort(function(a,b){return b.total-a.total;}); return arr;}
function renderGrafico(){var arr=calcRanking(); var total=arr.reduce(function(s,r){return s+r.total;},0); var media=arr.length? total/arr.length:0; var top=arr.length? arr[0].nome:'--'; document.getElementById('resumoGrafico').innerHTML='🏪 <b>'+esc(loja.nome)+'</b><br>Total: <b>'+fmt(total)+'</b> | Media: <b>'+fmt(media)+'</b><br>Top: <b>🏆 '+esc(top)+'</b>'; var max=arr.length? arr[0].total:1; var cores=['#facc15','#22c55e','#007bff','#7c3aed','#f97316','#ef4444']; var div=document.getElementById('graficoBarras'); div.innerHTML=''; for(var i=0;i<arr.length;i++){var r=arr[i]; var h=max? Math.max(18, Math.round(r.total/max*150)):18; div.innerHTML+='<div class="graf-col"><div class="barra" style="height:'+h+'px;background:'+cores[i%cores.length]+'">'+Math.round(r.total/max*100)+'%</div><b>'+fmt(r.total)+'</b><span>'+esc(r.nome)+'</span><small>'+r.qtd+' vendas</small></div>';} if(!vendasHoje.length) div.innerHTML='<p style="font-size:13px">Nenhuma venda ainda.</p>'; var lista=document.getElementById('listaGrafico'); lista.innerHTML=''; for(var j=0;j<arr.length;j++){var rr=arr[j]; var perc=total? Math.round(rr.total/total*100):0; lista.innerHTML+='<div class="rank-item'+(j===0?' top1':'')+'"><div class="podio">'+(j===0?'🥇':j===1?'🥈':j===2?'🥉':'🏅')+'</div><div style="flex:1;min-width:0"><b>'+esc(rr.nome)+'</b><br><small>'+rr.qtd+' vendas - '+perc+'%</small><div class="barra-meta"><div style="width:'+perc+'%">'+perc+'%</div></div></div><b>'+fmt(rr.total)+'</b></div>';}}
function enviarGraficoWhats(){var arr=calcRanking(); var total=arr.reduce(function(s,r){return s+r.total;},0); var msg='📊 GRAFICO - '+loja.nome+'\nTotal: '+fmt(total)+'\n\n'; for(var i=0;i<arr.length;i++){msg+=(i+1)+'o '+arr[i].nome+' - '+fmt(arr[i].total)+' ('+arr[i].qtd+' vendas)\n';} abrirWhatsComTexto(msg, loja.whats);}
function exportarBackup(){var dados={}; dados.app='StillusCalc PRO'; dados.loja=loja; dados.vendedores=vendedores; dados.logins=loginsVendedores; dados.itens=itens; dados.metas=metas; dados.vendasHoje=vendasHoje; dados.clientes=clientes; dados.caixa=caixa; var blob=new Blob([JSON.stringify(dados,null,2)],{type:'application/json'}); var a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='backup-stilluscalc-'+mesAtualStr()+'.json'; a.click(); alert('Backup baixado!');}
function importarBackup(input){var f=input.files[0]; if(!f) return; var r=new FileReader(); r.onload=function(e){try{var d=JSON.parse(e.target.result); if(!d.loja){alert('Backup invalido!'); return;} loja=d.loja; vendedores=d.vendedores||vendedores; itens=d.itens||[]; metas=d.metas||metas; vendasHoje=d.vendasHoje||[]; clientes=d.clientes||clientes; caixa=d.caixa||caixa; if(d.logins) loginsVendedores=d.logins; salvar(); renderLoja(); renderVendedores(); renderItens(); renderMetas(); alert('Backup restaurado!'); }catch(err){alert('Nao consegui ler!');}}; r.readAsText(f);}
function apagarTudo(){if(!confirm('APAGAR TUDO?')) return; if(!confirm('Ultima chance!')) return; localStorage.clear(); location.reload();}
function renderLoja(){document.getElementById('nomeLojaTopo').innerText=loja.nome+' - '+loja.slogan; document.getElementById('cfgLoja').value=loja.nome; document.getElementById('cfgWhats').value=loja.whats; document.getElementById('cfgSlogan').value=loja.slogan; document.getElementById('cfgTipo').value=loja.tipo; var cc=document.getElementById('cfgCodigoLoja'); if(cc) cc.value=loja.codigoLoja; var ce=document.getElementById('codigoLojaEquipe'); if(ce) ce.innerText=loja.codigoLoja; document.getElementById('vendedorAtualTopo').innerText='Vendedor: '+vendedorAtual; document.getElementById('vendendoComoItens').innerText=vendedorAtual; var sel=document.getElementById('vVendedor'); sel.innerHTML=''; for(var i=0;i<vendedores.length;i++){sel.innerHTML+='<option>'+esc(vendedores[i])+'</option>';} sel.value=vendedorAtual; atualizarPillUsuario();}
function salvarLoja(){if(usuarioLogado && usuarioLogado.tipo!=='dono'){alert('So o DONO pode mudar dados da loja!'); return;} var nome=limparTexto(document.getElementById('cfgLoja').value,60); if(!nome){alert('Coloque o nome da loja!'); return;} loja.nome=nome; loja.whats=limparNumeroWhats(document.getElementById('cfgWhats').value); loja.slogan=limparTexto(document.getElementById('cfgSlogan').value,80)||'O barato e aqui!'; loja.tipo=document.getElementById('cfgTipo').value; salvar(); renderLoja(); fecharModal('modalLoja');}
function addVendedor(){if(usuarioLogado && usuarioLogado.tipo!=='dono'){alert('So o DONO pode cadastrar vendedores!'); return;} var n=limparTexto(document.getElementById('novoVendNome').value,40); var login=limparTexto(document.getElementById('novoVendLogin').value,30).toLowerCase().replace(/\s/g,''); var senha=document.getElementById('novoVendSenha').value.trim(); if(!n||!login||!senha){alert('Preenche Nome, Login e Senha!'); return;} for(var i=0;i<loginsVendedores.length;i++){if(loginsVendedores[i].login.toLowerCase()===login){alert('Esse login ja existe! Usa outro.'); return;}} vendedores.push(n); loginsVendedores.push({nome:n, login:login, senha:senha, codigoLoja:loja.codigoLoja}); vendedorAtual=n; document.getElementById('novoVendNome').value=''; document.getElementById('novoVendLogin').value=''; document.getElementById('novoVendSenha').value=''; salvar(); renderVendedores(); renderListaLogins(); renderLoja(); alert('Vendedor cadastrado! ✅\n\nNome: '+n+'\nCodigo da Loja: '+loja.codigoLoja+'\nLogin: '+login+'\nSenha: '+senha+'\n\nManda esses dados pra ele!');}
function renderListaLogins(){var div=document.getElementById('listaLoginsVendedores'); if(!div) return; div.innerHTML='<b>Logins cadastrados:</b>'; for(var i=0;i<loginsVendedores.length;i++){var l=loginsVendedores[i]; div.innerHTML+='<div style="background:#f8fafc;border:1px solid #e2e8f0;border-radius:10px;padding:8px;margin-top:6px;font-size:12px;line-height:1.6"><b>'+esc(l.nome)+'</b><br>Codigo: <b>'+esc(l.codigoLoja)+'</b> | Login: <b>'+esc(l.login)+'</b> | Senha: <b>'+esc(l.senha)+'</b> <button class="btn btn-vermelho" style="width:auto;padding:4px 10px;margin-top:4px" onclick="removerVendedor('+i+')">REMOVER</button></div>';}}
function removerVendedor(idx){if(!confirm('Remover esse vendedor?')) return; var nome=loginsVendedores[idx].nome; loginsVendedores.splice(idx,1); var vi=vendedores.indexOf(nome); if(vi>-1) vendedores.splice(vi,1); salvar(); renderVendedores(); renderListaLogins();}
function copiarDadosVendedores(){var txt='🏪 '+loja.nome+' - StillusCalc PRO\n\nPara entrar, usa:\nCodigo da Loja: '+loja.codigoLoja+'\nLink: https://stilluscalc-pro.netlify.app\n\nSeus logins:\n'; for(var i=0;i<loginsVendedores.length;i++){txt+=loginsVendedores[i].nome+' - Login: '+loginsVendedores[i].login+' - Senha: '+loginsVendedores[i].senha+'\n';} navigator.clipboard.writeText(txt).then(function(){alert('Dados copiados! Cola no WhatsApp e manda pros vendedores.');});}
function renderVendedores(){var div=document.getElementById('listaVendedoresModal'); if(div){div.innerHTML=''; for(var i=0;i<vendedores.length;i++){var at=vendedores[i]===vendedorAtual?' ativo':''; div.innerHTML+='<span class="chip-vend'+at+'" onclick="trocarVendedor(\''+esc(vendedores[i])+'\')">'+esc(vendedores[i])+'</span>';}} var topo=document.getElementById('listaVendedoresTopo'); if(topo){topo.innerHTML=''; for(var j=0;j<vendedores.length;j++){var at2=vendedores[j]===vendedorAtual?' ativo':''; topo.innerHTML+='<span class="chip-vend'+at2+'" onclick="trocarVendedor(\''+esc(vendedores[j])+'\')">'+esc(vendedores[j])+'</span>';}} var ce=document.getElementById('codigoLojaEquipe'); if(ce) ce.innerText=loja.codigoLoja; renderListaLogins();}
function trocarVendedor(nome){if(usuarioLogado && usuarioLogado.tipo==='vend' && usuarioLogado.nome!==nome){alert('Voce esta logado como '+usuarioLogado.nome+' e nao pode trocar de vendedor!'); return;} vendedorAtual=nome; salvar(); renderVendedores(); renderLoja(); renderRanking();}
function aplicarFundo(){var f=localStorage.getItem('stilluscalc_fundo')||''; if(f){document.body.style.backgroundImage='url('+f+')'; var img=document.getElementById('prevFundo'); if(img){img.src=f; img.style.display='block';}}}
aplicarFundo();
function salvarFundo(input){var f=input.files[0]; if(!f) return; var r=new FileReader(); r.onload=function(e){try{localStorage.setItem('stilluscalc_fundo',e.target.result);}catch(err){alert('Foto muito grande!'); return;} aplicarFundo();}; r.readAsDataURL(f);}
function removerFundo(){localStorage.removeItem('stilluscalc_fundo'); document.body.style.backgroundImage=''; document.getElementById('prevFundo').style.display='none';}
function preverFotoItem(input){var f=input.files[0]; if(!f) return; var r=new FileReader(); r.onload=function(e){fotoTemp=e.target.result; document.getElementById('prevItem').src=e.target.result; document.getElementById('prevItem').style.display='block';}; r.readAsDataURL(f);}
function cadastrarItem(){var nome=limparTexto(document.getElementById('nNome').value,80); var codigo=limparTexto(document.getElementById('nCodigo').value,20).toUpperCase(); var preco=parseFloat(document.getElementById('nPreco').value); var custo=parseFloat(document.getElementById('nCusto').value)||0; if(!nome||!codigo||!preco){alert('Preencha Nome, Codigo e Preco!'); return;} for(var i=0;i<itens.length;i++){if(itens[i].codigo===codigo){alert('Codigo ja existe!'); return;}} var item={}; item.nome=nome; item.codigo=codigo; item.preco=preco; item.custo=custo; item.cat=document.getElementById('nCat').value; item.foto=fotoTemp; itens.push(item); fotoTemp=''; document.getElementById('nNome').value=''; document.getElementById('nCodigo').value=''; document.getElementById('nPreco').value=''; document.getElementById('nCusto').value=''; document.getElementById('prevItem').style.display='none'; salvar(); renderItens(); fecharModal('modalCad'); abrirModal('modalItens');}
function renderItens(){var busca=limparTexto(document.getElementById('buscaItem').value,80).toLowerCase(); var div=document.getElementById('listaItens'); div.innerHTML=''; var lista=[]; for(var i=0;i<itens.length;i++){if(itens[i].nome.toLowerCase().indexOf(busca)>-1||itens[i].codigo.toLowerCase().indexOf(busca)>-1) lista.push(itens[i]);} for(var j=0;j<lista.length;j++){var it=lista[j]; var idx=itens.indexOf(it); var ft=it.foto? '<img src="'+esc(it.foto)+'">' : '🛍️'; div.innerHTML+='<div class="item-cad"><div class="ft">'+ft+'</div><div class="info"><b>'+esc(it.nome)+'</b><br><small>'+esc(it.codigo)+' - '+esc(it.cat)+'</small><br><b>'+fmt(it.preco)+'</b></div><div style="display:flex;flex-direction:column;gap:4px;flex-shrink:0"><button class="btn btn-verde" style="width:auto;padding:8px 12px;margin:0" onclick="venderPorItem('+idx+')">VENDER</button><button class="btn btn-azul" style="width:auto;padding:6px 10px;margin:0" onclick="selecionarItem('+idx+')">CALCULAR</button><button class="btn btn-vermelho" style="width:auto;padding:6px 10px;margin:0" onclick="excluirItem('+idx+')">X</button></div></div>';} if(!lista.length) div.innerHTML='<p style="font-size:13px">Nenhum item.</p>'; var fav=document.getElementById('favoritosBox'); fav.innerHTML='<b>Rapido:</b><br>'; for(var k=0;k<Math.min(itens.length,5);k++){fav.innerHTML+='<span class="chip" onclick="venderPorItem('+k+')">🛒 '+esc(itens[k].nome)+' - '+fmt(itens[k].preco)+'</span>';} renderHist(); renderMetas();}
function excluirItem(idx){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('So o DONO pode apagar itens!'); return;} if(confirm('Apagar esse item?')){itens.splice(idx,1); salvar(); renderItens();}}
function selecionarItem(idx){var it=itens[idx]; document.getElementById('vNome').value=it.nome+' ('+it.codigo+')'; document.getElementById('vCodigo').value=it.codigo; document.getElementById('vPreco').value=it.preco; document.getElementById('vCusto').value=it.custo; calcularVendedor(); fecharModal('modalItens'); abrirModal('modalVend');}
function puxarItem(){var cod=limparTexto(document.getElementById('vCodigo').value,20).toUpperCase(); if(!cod){alert('Digite o codigo!'); return;} var ach=null; for(var i=0;i<itens.length;i++){if(itens[i].codigo===cod){ach=itens[i];break;}} if(!ach){alert('Codigo nao encontrado!'); return;} document.getElementById('vNome').value=ach.nome+' ('+ach.codigo+')'; document.getElementById('vPreco').value=ach.preco; document.getElementById('vCusto').value=ach.custo; calcularVendedor();}
function setModo(m){modoAtual=m; document.getElementById('btnModoVend').classList.toggle('ativo',m==='vend'); document.getElementById('btnModoCli').classList.toggle('ativo',m==='cli'); calcularVendedor();}
function setDesc(v){document.getElementById('vDesc').value=v; document.getElementById('vDescLabel').innerText=v+'%'; calcularVendedor();}
function calcularVendedor(){var preco=parseFloat(document.getElementById('vPreco').value); var custo=parseFloat(document.getElementById('vCusto').value)||0; var desc=parseFloat(document.getElementById('vDesc').value)||0; var comPerc=parseFloat(document.getElementById('vComissao').value)||3; var entrada=parseFloat(document.getElementById('vEntrada').value)||0; var frete=parseFloat(document.getElementById('vFrete').value)||0; var div=document.getElementById('resultadoVend'); if(!preco){div.innerHTML='Selecione um item!'; return;} var comDesc=preco*(1-desc/100); var totalFinal=comDesc+frete; var lucro=totalFinal-custo-frete; var margem=totalFinal?(lucro/totalFinal*100):0; var comissao=totalFinal*comPerc/100; var maxDesc=preco? Math.max(0,(preco-custo)/preco*100):0; var falta=totalFinal-entrada; var status=''; var classe=''; if(lucro<0){status='NAO DE ESSE DESCONTO! PREJUIZO!'; classe='perigo';} else if(margem<10){status='ATENCAO! Margem baixa!'; classe='atencao';} else {status='PODE DAR ESSE DESCONTO!'; classe='';} div.className='resultado '+classe; if(modoAtual==='cli'){div.innerHTML='<b>'+esc(document.getElementById('vNome').value||'Produto')+'</b><br>De <s>'+fmt(preco)+'</s> por <b style="font-size:20px">'+fmt(comDesc)+'</b>';} else {if(usuarioLogado && usuarioLogado.tipo==='vend'){div.innerHTML='<b>'+status+'</b><br>Preco: <b>'+fmt(preco)+'</b> | Com '+desc+'% OFF: <b>'+fmt(comDesc)+'</b><br>Total: <b>'+fmt(totalFinal)+'</b><br><small>Custo e lucro so o dono ve.</small>';} else {div.innerHTML='<b>'+status+'</b><br>Preco: <b>'+fmt(preco)+'</b> | Com '+desc+'% OFF: <b>'+fmt(comDesc)+'</b><br>Lucro: <b>'+fmt(lucro)+'</b> | Margem: <b>'+margem.toFixed(1)+'%</b><br>Comissao: <b>'+fmt(comissao)+'</b> | Desconto MAX: <b>'+maxDesc.toFixed(1)+'%</b><br>Total: <b>'+fmt(totalFinal)+'</b>';}} document.getElementById('parcelasVend').innerHTML='<b>Parcelas:</b> A vista '+fmt(totalFinal)+' | 3x '+fmt(totalFinal/3)+' | 6x '+fmt(totalFinal/6)+'<br>10x '+fmt(totalFinal/10)+' | 12x '+fmt(totalFinal/12);}
function limparVend(){document.getElementById('vNome').value=''; document.getElementById('vCodigo').value=''; document.getElementById('vPreco').value=''; document.getElementById('vCusto').value=''; document.getElementById('vDesc').value=10; document.getElementById('vDescLabel').innerText='10%'; document.getElementById('vEntrada').value=0; document.getElementById('vFrete').value=0;}
function calcAdd(v){expr+=v; document.getElementById('visorCalc').innerText=expr||'0';}
function calcLimpar(){expr=''; document.getElementById('visorCalc').innerText='0'; document.getElementById('histCalc').innerText='StillusCalc PRO';}
function calcBack(){expr=expr.slice(0,-1); document.getElementById('visorCalc').innerText=expr||'0';}
function calcSqrt(){var n=parseFloat(expr)||0; var r=Math.sqrt(n); expr=String(r); document.getElementById('visorCalc').innerText=r.toFixed(2);}
function calcQuad(){var n=parseFloat(expr)||0; var r=n*n; expr=String(r); document.getElementById('visorCalc').innerText=r.toFixed(2);}
function calcIgual(){try{var e2=expr.replace(/%/g,'/100'); var res=Function('return ('+e2+')')(); document.getElementById('histCalc').innerText=expr+' ='; document.getElementById('visorCalc').innerText=Number(res).toLocaleString('pt-BR',{maximumFractionDigits:2}); var h={}; h.texto=expr+' = '+res; h.data=new Date().toLocaleString('pt-BR'); historico.unshift(h); if(historico.length>20) historico.pop(); salvar(); renderHist(); expr=String(res);}catch(e){document.getElementById('visorCalc').innerText='Erro';}}
function copiarVisor(){var t=document.getElementById('visorCalc').innerText; navigator.clipboard.writeText(t); alert('Copiado: '+t);}
function usarComoPreco(){var t=document.getElementById('visorCalc').innerText.replace(/\./g,'').replace(',','.'); var n=parseFloat(t); if(!isNaN(n)){document.getElementById('vPreco').value=n; calcularVendedor(); abrirModal('modalVend');}}
function salvarCalculo(){var nome=document.getElementById('vNome').value||'Produto'; var preco=document.getElementById('vPreco').value||'0'; var h={}; h.texto=nome+' - '+fmt(preco); h.data=new Date().toLocaleString('pt-BR'); historico.unshift(h); salvar(); renderHist(); alert('Calculo salvo!');}
function renderHist(){var div=document.getElementById('listaHist'); if(!div) return; div.innerHTML=''; if(!historico.length) div.innerHTML='<p style="font-size:13px">Nenhum calculo ainda.</p>'; for(var i=0;i<Math.min(historico.length,20);i++){div.innerHTML+='<div class="hist"><b>'+esc(historico[i].texto)+'</b><br><small>'+esc(historico[i].data)+'</small></div>';}}
function limparHist(){if(confirm('Limpar historico?')){historico=[]; salvar(); renderHist();}}
function enviarWhats(){var nome=document.getElementById('vNome').value||'Produto'; var preco=document.getElementById('vPreco').value||0; var desc=document.getElementById('vDesc').value||0; var comDesc=preco*(1-desc/100); var msg='Ola! Orcamento '+loja.nome+' - '+nome+' - De '+fmt(preco)+' por '+fmt(comDesc)+' com '+desc+'% OFF!'; var dest=document.getElementById('whatsDestino')? document.getElementById('whatsDestino').value : loja.whats; abrirWhatsComTexto(msg,dest||loja.whats);}
function salvarMetas(){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('So o DONO pode mudar metas!'); renderMetas(); return;} metas.dia=parseFloat(document.getElementById('metaDia').value)||0; metas.semana=parseFloat(document.getElementById('metaSemana').value)||0; salvar(); renderMetas();}
function tentarEditarMes(){alert('🔒 META DO MES TRAVADA!');}
function renderMetas(){document.getElementById('metaDia').value=metas.dia; document.getElementById('vendidoDia').value=fmt(metas.vendidoDia); document.getElementById('metaSemana').value=metas.semana; document.getElementById('vendidoSemana').value=fmt(metas.vendidoSemana); document.getElementById('metaMes').value=metas.mes; document.getElementById('vendidoMes').value=fmt(metas.vendidoMes); document.getElementById('textoTravaMes').innerText='Mes atual: '+nomeMesAtual(); function conta(meta,vendido,el,barra){var falta=meta-vendido; var perc=meta? Math.min(100,Math.round(vendido/meta*100)):0; var html=''; if(meta===0){html='Coloque sua meta!';} else if(falta<=0){html='<b>'+fmt(meta)+'</b> - <b>'+fmt(vendido)+'</b> = <span class="bateu">META BATIDA! 🎉</span>';} else {html='<b>'+fmt(meta)+'</b> - <b>'+fmt(vendido)+'</b> = <span class="falta">Falta '+fmt(falta)+'</span>';} document.getElementById(el).innerHTML=html; var b=document.getElementById(barra); b.style.width=perc+'%'; b.innerText=perc+'%';} conta(metas.dia,metas.vendidoDia,'contaDia','barraDia'); conta(metas.semana,metas.vendidoSemana,'contaSemana','barraSemana'); conta(metas.mes,metas.vendidoMes,'contaMes','barraMes'); var faltaDia=Math.max(0,metas.dia-metas.vendidoDia); var faltaMes=Math.max(0,metas.mes-metas.vendidoMes); document.getElementById('resumoDiaTopo').innerText='Dia Falta '+fmt(faltaDia); document.getElementById('resumoMesTopo').innerText='Mes Falta '+fmt(faltaMes)+' 🔒'; var div=document.getElementById('listaVendasHoje'); if(div){div.innerHTML=''; var listaMostrar=vendasHoje; if(usuarioLogado && usuarioLogado.tipo==='vend'){listaMostrar=vendasHoje.filter(function(v){return v.vendedor===usuarioLogado.nome;});} if(!listaMostrar.length) div.innerHTML='<p style="font-size:13px">Nenhuma venda ainda hoje.</p>'; var rev=listaMostrar.slice().reverse(); for(var i=0;i<rev.length;i++){div.innerHTML+='<div class="venda-item"><span>🛒 '+esc(rev[i].nome)+'<br><small>'+esc(rev[i].vendedor)+' - '+esc(rev[i].data)+'</small></span><b>'+fmt(rev[i].valor)+'</b></div>';}}}
function registrarVendaAutomatica(nome,valor,vend){var v={}; v.nome=nome; v.valor=valor; v.vendedor=vend||vendedorAtual; v.data=new Date().toLocaleString('pt-BR'); vendasHoje.push(v); metas.vendidoDia+=valor; metas.vendidoSemana+=valor; metas.vendidoMes+=valor; salvar(); renderMetas(); renderItens(); renderRanking(); renderGrafico(); return v;}
function venderPorItem(idx){var it=itens[idx]; if(!confirm('Confirmar venda de '+it.nome+' por '+fmt(it.preco)+'?\nVendedor: '+vendedorAtual)) return; registrarVendaAutomatica(it.nome+' ('+it.codigo+')',it.preco,vendedorAtual); alert('VENDA FEITA! ✅\n'+it.nome+' - '+fmt(it.preco)); fecharModal('modalItens'); abrirModal('modalGrafico');}
function venderItemAtual(){var nome=document.getElementById('vNome').value||'Produto'; var preco=parseFloat(document.getElementById('vPreco').value); var desc=parseFloat(document.getElementById('vDesc').value)||0; var frete=parseFloat(document.getElementById('vFrete').value)||0; var vend=document.getElementById('vVendedor').value||vendedorAtual; if(!preco){alert('Selecione um item!'); return;} var final=preco*(1-desc/100)+frete; if(!confirm('Confirmar venda de '+nome+' por '+fmt(final)+'?\nVendedor: '+vend)) return; registrarVendaAutomatica(nome,final,vend); alert('VENDA FEITA! ✅\n'+nome+' - '+fmt(final)); fecharModal('modalVend'); abrirModal('modalGrafico');}
function zerarMeta(tipo){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('So o DONO pode zerar metas!'); return;} if(!confirm('Zerar?')) return; if(tipo==='dia') metas.vendidoDia=0; if(tipo==='semana') metas.vendidoSemana=0; salvar(); renderMetas();}
function limparVendasHoje(){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('So o DONO pode limpar vendas!'); return;} if(!confirm('Limpar todas as vendas?')) return; vendasHoje=[]; metas.vendidoDia=0; metas.vendidoSemana=0; metas.vendidoMes=0; salvar(); renderMetas(); renderRanking();}
function fecharMes(){if(usuarioLogado && usuarioLogado.tipo==='vend'){alert('So o DONO pode fechar o mes!'); return;} if(!confirm('Fechar o mes?')) return; var arc={}; arc.mes=metas.mesRef; arc.nomeMes=nomeMesAtual(); arc.metaMes=metas.mes; arc.vendidoMes=metas.vendidoMes; arc.vendas=vendasHoje.slice(); arc.dataFechamento=new Date().toLocaleString('pt-BR'); relatorios.push(arc); var novaMeta=prompt('Mes fechado! Qual a META DO MES NOVO? (R$)', '60000'); var nm=parseFloat(novaMeta); if(!isNaN(nm)&&nm>0) metas.mes=nm; metas.vendidoMes=0; metas.vendidoSemana=0; metas.vendidoDia=0; metas.mesRef=mesAtualStr(); vendasHoje=[]; salvar(); renderMetas(); renderRelatorio(); abrirModal('modalRel');}
function renderRanking(){var arr=calcRanking(); var div=document.getElementById('rankingBox'); div.innerHTML=''; var max=arr.length? arr[0].total:1; var emojis=['🥇','🥈','🥉']; for(var i=0;i<arr.length;i++){var r=arr[i]; var cls=i===0?' top1':i===1?' top2':i===2?' top3':''; var perc=max? Math.round(r.total/max*100):0; div.innerHTML+='<div class="rank-item'+cls+'"><div class="podio">'+(emojis[i]||'🏅')+'</div><div style="flex:1;min-width:0"><b>'+esc(r.nome)+(r.nome===vendedorAtual?' (Voce)':'')+'</b><br><small>'+r.qtd+' vendas - '+fmt(r.total)+'</small><div class="barra-meta"><div style="width:'+perc+'%">'+perc+'%</div></div></div><b style="flex-shrink:0">'+fmt(r.total)+'</b></div>';} if(!vendasHoje.length) div.innerHTML+='<p style="font-size:13px">Nenhuma venda ainda.</p>';}
function textoRelatorio(){var t=''; t+='RELATORIO '+loja.nome.toUpperCase()+' - StillusCalc PRO\n'; t+='Data: '+new Date().toLocaleString('pt-BR')+'\n'; t+='Meta Dia: '+fmt(metas.dia)+' - Vendido: '+fmt(metas.vendidoDia)+'\n'; t+='Meta Mes: '+fmt(metas.mes)+' - Vendido: '+fmt(metas.vendidoMes)+'\n'; var arr=calcRanking(); for(var i=0;i<arr.length;i++){t+=(i+1)+'o '+arr[i].nome+' - '+fmt(arr[i].total)+' ('+arr[i].qtd+' vendas)\n';} return t;}
function renderRelatorio(){var div=document.getElementById('relatorioBox'); var html=''; html+='<div class="rel-box"><b>🏪 '+esc(loja.nome)+' - '+esc(nomeMesAtual())+'</b><br>Dia: <b>'+fmt(metas.dia)+'</b> - Vendido <b>'+fmt(metas.vendidoDia)+'</b><br>Mes 🔒: <b>'+fmt(metas.mes)+'</b> - Vendido <b>'+fmt(metas.vendidoMes)+'</b></div>'; var arr=calcRanking(); html+='<div class="rel-box"><b>🏆 RANKING</b><br>'; for(var i=0;i<arr.length;i++){html+=(i+1)+'o '+esc(arr[i].nome)+' - <b>'+fmt(arr[i].total)+'</b><br>';} html+='</div>'; div.innerHTML=html;}
function enviarRelatorioWhats(){var msg=textoRelatorio(); var dest=document.getElementById('whatsDestino')? document.getElementById('whatsDestino').value : loja.whats; abrirWhatsComTexto(msg,dest||loja.whats);}
function enviarRankingWhats(){var arr=calcRanking(); var msg='🏆 RANKING '+loja.nome+' - Hoje\n'; for(var i=0;i<arr.length;i++){msg+=(i+1)+'o '+arr[i].nome+' - '+fmt(arr[i].total)+'\n';} var dest=document.getElementById('whatsDestino')? document.getElementById('whatsDestino').value : loja.whats; abrirWhatsComTexto(msg,dest||loja.whats);}
function copiarRelatorio(){var t=textoRelatorio(); navigator.clipboard.writeText(t).then(function(){alert('Relatorio copiado!');});}
function gerarHTMLRelatorio(){var h=''; h+='<!DOCTYPE html><html lang="pt-BR"><head><meta charset="UTF-8"><title>Relatorio</title><style>body{font-family:Arial;padding:20px} table{width:100%;border-collapse:collapse} th,td{border:1px solid #ddd;padding:8px} th{background:#111827;color:#fff}</style></head><body>'; h+='<h1>'+esc(loja.nome)+' - Relatorio</h1><p>'+new Date().toLocaleString('pt-BR')+'</p><table><tr><th>Meta</th><th>Meta</th><th>Vendido</th></tr><tr><td>Dia</td><td>'+fmt(metas.dia)+'</td><td>'+fmt(metas.vendidoDia)+'</td></tr><tr><td>Mes</td><td>'+fmt(metas.mes)+'</td><td>'+fmt(metas.vendidoMes)+'</td></tr></table>'; h+='<p>© StillusCalc PRO</p><button onclick="window.print()">IMPRIMIR</button></body></html>'; return h;}
function baixarArquivoRelatorio(){var html=gerarHTMLRelatorio(); var blob=new Blob([html],{type:'text/html'}); var a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='relatorio-'+mesAtualStr()+'.html'; a.click();}
function baixarRelatorioPDF(){var html=gerarHTMLRelatorio(); var w=window.open('','_blank'); if(!w){baixarArquivoRelatorio(); return;} w.document.write(html); w.document.close(); setTimeout(function(){w.print();},400);}
tentarEntrarViaLink();
renderLoja(); renderVendedores(); renderItens(); calcularVendedor(); renderMetas(); renderRanking(); renderGrafico(); renderRelatorio(); atualizarStatusPlano(); atualizarPillUsuario();
var jaViu=''; try{jaViu=localStorage.getItem('stilluscalc_jaViuBoasVindas')||'';}catch(e){} 
if(!usuarioLogado){setTimeout(function(){abrirModal('modalLogin');},600);}
else if(!estaLiberado()){setTimeout(function(){abrirModal('modalPlanos');},1200);}
</script>
</body>
</html>
