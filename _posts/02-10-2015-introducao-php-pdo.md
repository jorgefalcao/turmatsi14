---
layout: post
categories : [tutoriais]
data: 10 de Fevereiro de 2015
autor: Luis Felipe Oliveira
comments: true
titulo: Introdução ao PHP PDO
---
<style>
li.L0,
li.L1,
li.L2,
li.L3,
li.L5,
li.L6,
li.L7,
li.L8 { list-style-type: decimal !important }
</style>

<h1>Introdução ao PHP PDO</h1>
<h5 style="margin-top:-1px;">Autor original: Rodrigo Marques(DevMedia)</h5>
<hr>

<img class="image-show img-responsive" src="{{ site.baseurl }}/img/pdo-em-php.jpg"><img>

<div class="post-content">
<h2>Habilitar o PDO</h2>
<p>Antes de começarmos a trabalhar com o PDO, é necessário habilitar o driver do PDO e o driver referente ao banco que será utilizado. Para habilitar o PDO é bem simples, vá ate o seu arquivo php.ini que encontra-se dentro do diretório onde foi instalado o PHP e remova os comentários (;) das linhas abaixo.</p>

<h4><strong>Listagem 1 - Habilitando PDO no Windows</strong></h4>

<p>extension=php_pdo.dll<br>
extension=php_pdo_mysql.dll</p>

<h4><strong>Listagem 2 - Habilitando PDO no Linux</strong></h4>

<p>extension=pdo.so<br>
extension=pdo_mysql.so</p>

<h2>PDO (PHP Data Object) - Definição</h2>
<p>PDO_MYSQL é um driver que implementa a interface PHP Data Objects (PDO) - <a href="http://www.php.net/manual/pt_BR/intro.pdo.php">link</a>  para acesso do PHP ao MySQL 3.x, 4.x and 5.x.</p>

<p>PDO_MYSQL tem vantagens do nativo suporte a prepared statement presente no MySQL 4.1 e superior. Se você está usando um versão antiga da biblioteca do mysql client, PDO irá emular para você.<a href="http://php.net/manual/pt_BR/ref.pdo-mysql.php">Neste link.</a></p>

<p>A utilização do PDO fornece uma camada de abstração em relação a conexão com o banco de dados visto que o PDO efetua a conexão com diversos bancos de dados da mesma maneira, modificando apenas a sua string de conexão.</p>

<h4><strong>Listagem 3 - Conexão com o banco de dados com o PDO</strong></h4>

<pre class="prettyprint linenums">
$con = new PDO("mysql:host=localhost;dbname=exercicio", "root", "senha");
</pre>

A classe PDO em sua instancia pede como parâmetro primeiro o banco que será utilizado, O caminho do banco de dados e o nome da base de dados. Após devemos inserir o login e a senha do banco de dados.</p>

<p>BANCO DE DADOS:host=CAMINHO BANCO;dbname=NOME BASE</p>

<p>Logo basta modificarmos essa string teremos conexão com qualquer outro banco de dados. Note que estamos apenas efetuando uma conexão simples com o banco de dados mysql, com a utilização do PDO poderíamos, se necessário, utilizar transações para as operações do banco, porem não é o objetivo deste artigo.</p>

<p>Para trabalhar com operações no banco, o PDO possui um método conhecido como prepare. Como o próprio nome diz, este método apenas prepara uma operação no banco de dados, logo se faz necessário a utilização de outros métodos como execute por exemplo, para realmente executar a operação.</p>

<p>Vejamos abaixo o exemplo de um inserção de dados no banco, imagem que temos uma tabela chamada de pessoa com os campos idpessoa, nome e email e iremos utilizar a biblioteca para inserir nesta tabela.</p>

<p>Lembrando, os métodos utilizados neste é exemplo são apenas alguns dos métodos existentes na biblioteca PDO, para o conhecimento de todos os métodos sugiro que acessem ao Manual do PHP <a href="http://www.php.net/manual/pt_BR/book.pdo.php">neste link.</a></p>

<h4><strong>Listagem 4 - Criando a Tabela do Banco de dados</strong></h4>

<pre class="prettyprint linenums">
CREATE  TABLE IF NOT EXISTS pessoa (
  	idpessoa INT NOT NULL AUTO_INCREMENT ,
  	nome VARCHAR(45) NOT NULL ,
  	email VARCHAR(45) NOT NULL ,
  	PRIMARY KEY (idpessoa));
)
</pre>

<h4><strong>Listagem 5 - Exemplo de Inserção de Dados</strong></h4>

<pre class="prettyprint linenums">
	$stmt = $con->prepare("INSERT INTO pessoa(nome, email) VALUES(?, ?)");
	$stmt->bindParam(1,”Nome da Pessoa”);
	$stmt->bindParam(2,”email@email.com”);
	$stmt->execute();
</pre>

<p>Conforme podemos observar no código acima, primeiramente houve uma preparação no SQL que será enviado ao banco de dados. O método prepare ele apenas inicia uma query, esta possui diversos interrogações (?) que devemos substituir pelos valores reais adicionado.</p>

<p>Os valores deverão ser adicionados com o método bindParam, este método utiliza 2 ou 3 passagens de parâmetros. No exemplo criado temos apenas duas passagens de parâmetros, sendo a primeira referente a posição do interrogação que será substituído e o segundo parâmetro referente ao valor que será inserido no banco. Existe um 3 parâmetro que é referente ao tipo de valor que será enviado.</p>

<p>Com isso já temos uma inserção no banco de dados com o auxilio da biblioteca, com os dados já inseridos vamos conhecer como devemos fazer para buscar todos os valores da tabela pessoa.</p>

<h4><strong>Listagem 6 - Exemplo de Listagem de dados</strong></h4>

<pre class="prettyprint linenums">
	$rs = $con->query(“SELECT idpessoa, nome, email FROM pessoa”);
	while($row = $rs->fetch(PDO::FETCH_OBJ))  {
		echo $row->idpessoa;
		echo $row->nome;
		echo $row->email;
	}
</pre>

<p>No código acima temos uma consulta sem passagem de parâmetro de todos os dados armazenados na tabela pessoa. Utilizamos o método query para isso. O método query ira armazenar na variável $rs todos os dados referentes a consulta do banco.</p>

<p>Após a variável $rs ser populada, devemos utilizar um while para percorrer esses dados e trabalharmos com os valores. Dentro do while inserimos o método fetch do PDO que tem como função resgatar linha a linha do resultado da consulta. No método fetch utilizamos um parâmetro PDO::FETCH_OBJ, este parâmetro define a forma na qual os dados serão retornados e armazenados na variável $row, criada dentro do while.</p>

<p>O PDO::FETCH_OBJ trata cada linha da consulta como um objeto, transformando os campos que foram retornados em atributos do objeto $row. Acessamos estes atributos utilizando os caracteres -> (traço maior) e o nome do campo buscado.</p>

<p>Exemplo para imprimir o valor do campo nome da consulta teria que utilizar</p>

<h4><strong>Listagem 7 - Imprimindo Dados</strong></h4>

<pre class="prettyprint linenums">
$row->nome<br><br> 
</pre>

<p>Se fossemos criar uma consulta com passagem de parâmetros seria utilizado o método prepara, pois o mesmo suporta inserção de elementos após a criação da query. Veja no exemplo abaixo se a consulta dos dados da tabela pessoa fosse realizada através de uma igualdade do nome.</p>

<h4><strong>Listagem 8 - Consulta com igualdade do nome</strong></h4>

<pre class="prettyprint linenums">
$rs = $con->prepare("SELECT idpessoa, nome, email FROM pessoa WHERE nome LIKE ?");
$rs->bindParam(1, $nome . “%”);
if($rs->execute()) {
	if($rs->rowCount() > 0) {
		while($row = $rs->fetch(PDO::FETCH_OBJ)){
			echo $row->idpessoa;
			echo $row->nome;
			echo $row->email;
		}
        }    
}
</pre>

<p>O método prepare foi utilizado no exemplo acima com a idéia apenas de iniciar a query e aguardar pela inclusão de valores posteriormente. O nome foi inserido em um segundo momento com o % (per cento), pois em SQL ele representa um coringa. Logo estaremos buscando por todas as pessoas armazenadas no banco de dados cujo seu nome inicie com a(s) letra(s) informada na variável $nome por exemplo.</p>

<p>Para efetuar as operações de atualização e deleção de dados no banco teremos um processo parecido com a inserção, seguem exemplos abaixo:</p>

<h4><strong>Listagem 9 - Deletando dados</strong></h4>

<pre class="prettyprint linenums">
$stmt = $con->prepare("DELETE FROM pessoa WHERE idpessoa = ?");
$stmt->bindParam(1, $id);
$stmt->execute();
</pre>

<h4><strong>Listagem 10 - Atualizando dados</strong></h4>

<pre class="prettyprint linenums">
$stmt = $con->prepare("UPDATE pessoa SET nome = ?, email = ? WHERE idpessoa = ?");
$stmt->bindParam(1,$nome );
$stmt->bindParam(2,$email);
$stmt->bindParam(3,$id);
$stmt->execute();
</pre>

</div>
<hr>

<div class="info-post">
<b>em 09/02/2015 <br/>
por:  Luis Felipe Oliveira </b><br/>
<div class="image-author-luis"></div>
<div class="author-description-luis">
	Trabalha com T.I voltado ao suporte para usuario, estudante<br/> de TSI e nas horas vagas degustador de cervejas.
</div>
</div>

