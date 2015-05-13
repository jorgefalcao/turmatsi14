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
<p style="margin:0 15px 0"><i>service apache2 reload</i></p>

<blockquote>
	<p><b>$</b> sudo service apache2 reload</p>
</blockquote>

<hr>

<div class="info-post">
<b>em 13/05/2015 <br/>
por:  Yuri C. Fontella </b><br/>
<div class="image-author-yuri"></div>
<div class="author-description-yuri">
	Gaúcho colorado de Porto Alegre, tomando uma Polar e desenvolvendo alguma coisa.
</div>
</div>

