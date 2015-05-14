---
layout: post
categories : [tutoriais]
data: 13 de maio de 2015
autor: Yuri C. Fontella
comments: true
titulo: Criando VirtualHosts no Apache
---

<h1>Criando VirtualHosts no Apache</h1>
<p>Todos desenvolvedores web iniciantes gostariam de fazer o apache rodar localmente como fosse um site normal, evitando aquela famosa url “localhost/pasta/projeto”, com seus próprios domínios locais. Nesse tutorial pretendo ajudar a você, que tem dificuldades de montar seu próprio site em seu computador, a configurar corretamente seus Virtual Hosts no Apache. Sendo assim, podendo acessar o seu site por um caminho bem mais acessível no navegador, tornando sua produtividade ainda maior criando virtualhosts.</p>
<p>Após instalado o Apache na sua distribuição Linux, vamos as configurações necessárias:</p>
<p>Crie um novo arquivo vazio dentro de <b>/etc/apache2/sites-available</b> com o nome da sua virtualhost:</p>

<blockquote>
	<p><b>$</b> sudo touch /etc/apache2/sites-available/meuprojeto.local.conf</p>
</blockquote>

<p>Abra o arquivo de configurações com o seguinte comando:</p>

<blockquote>
	<p><b>$</b> sudo nano /etc/apache2/sites-available/meuprojeto.local.conf</p>
</blockquote>

<p>Para sua virtualhost funcionar, edite o arquivo com o seguinte conteúdo:</p>

<img class="image-show img-responsive" src="{{ site.baseurl }}/img/nano.jpg" style="width:700px; height:400px">
<p><i>Para salvar aperte Ctrl+O e para sair Ctrl+X</i></p>

<p><b>ServerName</b>: É o nome que você vai acessar o seu projeto pela url</p>
<p><b>DocumentRoot</b>: É o caminho onde os arquivos do seu projeto estão</p>

<br>

<p>Agora você precisa ativar a sua virtuahost, basicamente ele irá criar um atalho do seu arquivo para a pasta <b>sites-enabled</b></p>

<blockquote>
	<p><b>$</b> sudo a2ensite meuprojeto.local</p>
</blockquote>

<p>Aparecerá a seguinte mensagem: </p>
<p style="margin:0"><i>Enabling site meuprojeto.local.</i></p>
<p style="margin:0"><i>To activate the new configuration, you need to run:</i></p>
<p style="margin:0 15px 0"><i>service apache2 restart</i></p>

<blockquote>
	<p><b>$</b> sudo service apache2 restart</p>
</blockquote>

<p>Pronto, seu site está ativo no Apache, porém ainda não pode ser acessado pela url sem o "localhost".</p>
<p>Agora no terminal digite:</p>

<blockquote>
	<p><b>$</b> sudo nano /etc/hosts</p>
</blockquote>

<p>Edite o arquivo "hosts" para que o <i>ServerName</i> que você definiu seja interpretado como um endereço <i>localhost</i></p>

<img class="image-show img-responsive" src="{{ site.baseurl }}/img/nano-2.jpg" style="width:700px; height:100px">
<p><i>Para salvar aperte Ctrl+O e para sair Ctrl+X</i></p>

<p>Pronto, sua virtualhost deve estar funcionado... abra o navegador e digite o <i>ServerName</i> criado por você, ele irá direcionar para o <i>DocumentRoot</i> que você definiu.</p>

<img class="image-show img-responsive" src="{{ site.baseurl }}/img/web.png" style="width:745px; height:510px; margin-left: -20px">

<h4>Outras opções</h4>
<p><b>Ainda é possível adicionar outras opções no arquivo de configuração:</b></p>
<p>ServerAdmin webmaster@localhost</p>
<p><b>E o caminho dos logs:</b></p>
<p>ErrorLog ${APACHE_LOG_DIR}/error.log</p>
<p>CustomLog ${APACHE_LOG_DIR}/access.log combined</p>

<br>

<h4>Considerações finais</h4>
<p style="margin:0">Para cada site ou projeto é preciso configurar uma nova virtualhost, esse tutorial foi escrito e testado especificamente voltado para a distribuição <i>Debian GNU/Linux</i> e seus derivados (Ubuntu, Mint, Elementary, etc).
O processo tem que ser exatamente esse, mas vocês podem achar outros métodos de se fazer, por exemplo, para abrir um arquivo não necessariamente deverá ser aberto dentro do terminal com o comando <i>nano</i>. O mesmo pode ser aberto com um editor de arquivos.
Cabe a cada um fazer do jeito que mais se sente a vontade, espero que consigam criar e configurar... qualquer dúvida comentem aí!</p>

<hr style="margin: 40px 0 40px">

<div class="info-post">
<b>em 13/05/2015 <br/>
por:  Yuri C. Fontella </b><br/>
<div class="image-author-yuri"></div>
<div class="author-description-yuri">
	Gaúcho colorado de Porto Alegre. 
	<p style="margin:0">Sempre tomando uma Polar e desenvolvendo alguma coisa.</p>
</div>
</div>

