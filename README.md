# trabalhobncodados

ETAPA 01:
1. Modelagem no minimundo do banco, constar pelo menos 3 tabelas relacionadas,
pode ser mais do que 3 tabelas. Nesta etapa será dividido os grupos, escolha do
tema do sistema e apresentação para o professor da proposta do grupo para
validação.
![image](https://github.com/Ericaoliveira12/trabalhobncodados/assets/111866617/e2bf77c6-2888-4cc6-a568-ef100843f711)

ETAPA 02:
2. Construir o Modelo Entidade Relacionamento(MER) com todos os atributos para
cada entidade.
![image](https://github.com/Ericaoliveira12/trabalhobncodados/assets/111866617/ed6cc55f-3bdc-4118-aeb8-ac5d75c1bda1)

ETAPA 03:
3. Construir o Modelo Logico/Relacional do modelo.

Esse código é usado para criar tabelas em um banco de dados relacionado a vendas de CDs. As tabelas são "cd" para armazenar informações sobre os CDs, "cliente" para armazenar informações sobre os clientes, "Compra" para armazenar informações sobre as compras feitas pelos clientes e "cd_cliente" como uma tabela de junção para relacionar os CDs aos clientes. As declarações ALTER TABLE são usadas para adicionar restrições de chave estrangeira às tabelas. Isso garante que as relações entre as tabelas sejam mantidas e que as exclusões em cascata não sejam permitidas.

![image](https://github.com/Ericaoliveira12/trabalhobncodados/assets/111866617/1fb7bcf6-b388-4761-acd5-572c28e02078)

![image](https://github.com/Ericaoliveira12/trabalhobncodados/assets/111866617/e2480c0a-7505-4889-818a-138be8c36e99)

ETAPA 04:
4. Construir as tabelas do banco, definindo os relacionamentos entre elas através de
chaves primarias e estrangeiras.

-- Tabela de Artistas
CREATE TABLE Artistas (
    ArtistaID INT PRIMARY KEY,
    NomeArtista VARCHAR(100)
);

-- Tabela de Álbuns
CREATE TABLE Albuns (
    AlbumID INT PRIMARY KEY,
    NomeAlbum VARCHAR(100),
    ArtistaID INT,
    FOREIGN KEY (ArtistaID) REFERENCES Artistas(ArtistaID)
);

-- Tabela de Canções
CREATE TABLE Cancoes (
    CancaoID INT PRIMARY KEY,
    NomeCancao VARCHAR(100),
    AlbumID INT,
    FOREIGN KEY (AlbumID) REFERENCES Albuns(AlbumID)
);

1. Tabela de Artistas:
   - `ArtistaID` é a chave primária que identifica exclusivamente um artista.
   - `NomeArtista` armazena o nome do artista.

2. Tabela de Álbuns:
   - `AlbumID` é a chave primária que identifica exclusivamente um álbum.
   - `NomeAlbum` armazena o nome do álbum.
   - `ArtistaID` é uma chave estrangeira que se relaciona com a tabela de Artistas, conectando cada álbum a um artista específico.

3. Tabela de Canções:
   - `CancaoID` é a chave primária que identifica exclusivamente uma canção.
   - `NomeCancao` armazena o nome da canção.
   - `AlbumID` é uma chave estrangeira que se relaciona com a tabela de Albuns, conectando cada canção a um álbum específico.

Essas tabelas são um exemplo de um esquema de banco de dados relacionais para armazenar informações sobre artistas, álbuns e canções de música.

Etapa 05:

5. Criar um sistema que alimente o banco inserindo as informações através de uma
interface web com PHP, pode-se utilizar o phpMyadmin para a conexão e definir
pelo menos 10 consultas para o banco, seu sistema também deve ter gráficos
gerados a partir dos dados que estão no banco, com informações que sejam úteis.

processar_formulario.php:

<?php
include("config.php"); // Inclui o arquivo de configuração

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $titulo = $_POST["titulo"];
    $artista = $_POST["artista"];
    $genero = $_POST["genero"];
    $preco = $_POST["preco"];
    $estoque = $_POST["estoque"];
    $idioma = $_POST["idioma"];

    // Inserção de dados no banco de dados (sem stmt)
    $sql = "INSERT INTO cd (titulo, artista, genero, preco, estoque, idioma) VALUES ('$titulo', '$artista', '$genero', $preco, $estoque, '$idioma')";

    if ($conn->query($sql) === TRUE) {
        echo "<script>alert('Dados Cadastrados')</script>";
        echo "<script>window.location.href = 'http://localhost/loja_cds/index.php'</script>";
        echo "<br>";
        echo "<a href='index.php'>Voltar ao Menu</a>";
        
    } else {
        echo "Erro na inserção de dados: " . $conn->error;
        echo "<br>";
        echo "<a href='index.php'>Voltar ao Menu</a>";

    }
}
?>

processar_compra.php:

<?php
include("config.php"); // Inclui o arquivo de configuração

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $data = $_POST["data"];
    $cliente = $_POST["cliente"];
    $total = $_POST["total"];
    $produto = $_POST["produto"];
    $totalp = $_POST["totalp"];
    $idioma = $_POST["idioma"];
    
    // Inserção de dados no banco de dados (sem stmt)
    $sql = "INSERT INTO Compra (data, cliente, Total, produto, Totalp, idioma) VALUES ('$data', '$cliente', $total, '$produto', $totalp, '$idioma')";

    if ($conn->query($sql) === TRUE) {
        echo "<script>alert('Compra Cadastrada')</script>";
        echo "<script>window.location.href = 'http://localhost/loja_cds/index.php'</script>";
        echo "<br>";
        echo "<a href='cd.php'>Adicionar produto</a>";
        echo "<br>";
        echo "<a href='compra.php'>Fazer compra</a>";
        echo "<br>";
        echo "<a href='crud.php'>Cadastrar cliente</a>";
    } else {
        echo "Erro na inserção de dados: " . $conn->error;
        echo "<br>";
        echo "<a href='cd.php'>Adicionar produto</a>";
        echo "<br>";
        echo "<a href='compra.php'>Fazer compra</a>";
        echo "<br>";
        echo "<a href='cadastro.php'>Cadastrar cliente</a>";
    }
}
?>

index.php:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Login</title>
</head>
<body>
    <div class="main-login">
        <div class="card-login">
            <img src="https://img.freepik.com/premium-vector/mobile-music-design_25030-2940.jpg" alt="Imagem de fundo" />
             <a class="button" href="cd.php">Cadastrar Produto</a>
             <a class="button" href="crud.php">Cadastrar Cliente</a>
             <a class="button" href="compra.php">Cadastrar Compra</a>
        </div>
    </div>
</body>
</html>


<style>
    body {
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.card-login {
    text-align: center;
    background: #2f2841;
    border-radius: 20px;
    box-shadow: 0px 10px 40px #00000056;
    padding: 30px;
    max-width: 400px;
    width: 100%;
}

img {
    max-width: 100%;<a class="button" href="#">Botão 1</a>
    <a class="button" href="#">Botão 2</a>
    <a class="button" href="#">Botão 3</a>
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    margin: 10px;
}

/* Estilos para os botões */
.button {
    display: block; /* Torna os botões elementos de bloco */
    width: 150px;
    margin: 10px 0; /* Adiciona espaçamento vertical entre os botões */
    padding: 10px 20px;
    background-color: #3498db;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    text-align: center;
    text-decoration: none; /* Remove sublinhado em links */
}

.button:hover {
    background-color: #1e70c1;
}



.textfield > input {
    width: 100%;
    border: none;
    border-radius: 10px;
    padding: 15px;
    background: #514869;
    color: #f0ffffde;
    font-size: 12pt;
    box-shadow: 0px 10px 40px #00000056;
    outline: none;
    box-sizing: border-box;
}

.textfield > label {
    color: #f0ffffde;
    margin-bottom: 10px;
}

.textfield > input::placeholder {
    color: #f0ffff94;
}

.btn-login {
    width: 100%;
    padding: 16px 0px;
    margin-top: 40px;
    border: none;
    border-radius: 8px;
}

.custom-button {
    background-color: #3498db;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin: 5px;
    font-size: 16px;
}

.custom-button:hover {
    background-color: #1e70c1;
}

</style>

Grafico_barra.php:
![image](https://github.com/Ericaoliveira12/trabalhobncodados/assets/111866617/a6aec2dd-28b3-41d8-aefe-b1544312747c)


<!DOCTYPE html>
<html>
  <head>
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['bar']});
      google.charts.setOnLoadCallback(drawChart);

      function drawChart() {
        var data = new google.visualization.DataTable();
        data.addColumn('string', 'Produto');
        data.addColumn('number', 'Quantidade Vendida');

        <?php
        include 'config.php';

        $sql = "SELECT produto, SUM(Totalp) AS quantidade_vendida FROM Compra GROUP BY produto ORDER BY quantidade_vendida DESC LIMIT 10";
        $result = mysqli_query($config, $sql);

        while ($row = mysqli_fetch_assoc($result)) {
          $produto = $row['produto'];
          $quantidade = (int)$row['quantidade_vendida'];
          echo "data.addRow(['$produto', $quantidade]);";
        }
        ?>
        
        var options = {
          chart: {
            title: 'Produtos Mais Vendidos',
            subtitle: 'Quantidade Vendida',
          },
          bars: 'horizontal' // Gráfico de barras horizontais
        };

        var chart = new google.charts.Bar(document.getElementById('barchart_material'));

        chart.draw(data, google.charts.Bar.convertOptions(options));
      }
    </script>
  </head>
  <body>
    <div id="barchart_material" style="width: 900px; height: 500px;"></div>
  </body>
</html>


crud.php:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Cadastro</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>
<body>
    <div class="container mt-5">
        <h2>Formulário de Cadastro</h2>
        <form method="post" action="cadastro.php">
            <div class="form-group">
                <label for="nome">Nome:</label>
                <input type="text" class="form-control" id="nome" name="nome" required>
            </div>
            <div class="form-group">
                <label for="endereco">Endereço:</label>
                <input type="text" class="form-control" id="endereco" name="endereco" required>
            </div>
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" class="form-control" id="email" name="email" required>
            </div>
            <div class="form-group">
                <label for="telefone">Número de Telefone:</label>
                <input type="tel" class="form-control" id="telefone" name="telefone" required>
            </div>
            <button type="submit" class="btn btn-primary">Enviar</button>
        </form>
    </div>
</body>
</html>

Config.php:

<?php
    $servidor = "localhost";
    $username = "root";
    $password = "";
    $banco = "loja_cds";

    $conn = mysqli_connect($servidor, $username,$password,$banco); 

   /*  if (!$conn){
        echo "Não Conectado";
    }
 
    else {
        echo "Conectado";
    }    
 */

?>

Compra.php:

!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Conexão ao Banco de Dados</title>
    <!-- Inclua as referências ao Bootstrap CSS -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>
<body>
    <div class="container">
        <h2>Formulário de Conexão ao Banco de Dados</h2>
        <form action="processar_compra.php" method="post">
            <div class="form-group">
                <label for="data">Data:</label>
                <input type="date" class="form-control" id="data" name="data" required>
            </div>
            <div class="form-group">
                <label for="cliente">Cliente:</label>
                <input type="text" class="form-control" id="cliente" name="cliente" required>
            </div>
            <div class="form-group">
                <label for="produto">Produto:</label>
                <input type="text" class="form-control" id="produto" name="produto" required>
            </div>
            <div class="form-group">
                <label for="idioma">Idioma:</label>
                <input type="text" class="form-control" id="idioma" name="idioma" step="0.01" required>
            </div>
            <div class="form-group">
                <label for="total">Total:</label>
                <input type="number" class="form-control" id="total" name="total" step="0.01" required>
            </div>
            <div class="form-group">
                <label for="totalp">Quantidade de produtos:</label>
                <input type="number" class="form-control" id="totalp" name="totalp" step="0.01" required>
            </div>
            <button type="submit" class="btn btn-primary">Conectar ao Banco de Dados</button>
        </form>
    </div>

    <!-- Inclua as referências ao Bootstrap JavaScript e jQuery (opcional) para recursos interativos -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>

Cd.php:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Produtos</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>
<body>
    <div class="container mt-5">
        <h2>Formulário de Produtos</h2>
        <form method="post" action="processar_formulario.php">
            <div class="form-group">
                <label for="titulo">Título do Disco:</label>
                <input type="text" class="form-control" id="titulo" name="titulo" required>
            </div>
            <div class="form-group">
                <label for="artista">Artista:</label>
                <input type="text" class="form-control" id="artista" name="artista" required>
            </div>
            <div class="form-group">
                <label for="genero">Gênero:</label>
                <input type="text" class="form-control" id="genero" name="genero" required>
            </div>
            <div class="form-group">
                <label for="idioma">Idioma:</label>
                <input type="text" class="form-control" id="idioma" name="idioma" required>
            </div>
            <div class="form-group">
                <label for="preco">Preço:</label>
                <input type="number" class="form-control" id="preco" name="preco" step="0.01" required>
            </div>
            <div class="form-group">
                <label for="estoque">Quantidade em Estoque:</label>
                <input type="number" class="form-control" id="estoque" name="estoque" required>
            </div>
            <button type="submit" class="btn btn-primary">Enviar</button>
        </form>
    </div>

</body>
</html>

Cadastro.php:

<?php
include("config.php"); // Inclui o arquivo de configuração

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nome = $_POST["nome"];
    $endereco = $_POST["endereco"];
    $email = $_POST["email"];
    $telefone = $_POST["telefone"];

    // Inserção de dados no banco de dados
    $sql = "INSERT INTO cliente (Nome, Endereco, Email, Numero_de_telefone) VALUES ('$nome', '$endereco', '$email', '$telefone')";

    if ($conn->query($sql) === TRUE) {
        echo "<script>alert('Dados Cadastrados')</script>";
        echo "<script>window.location.href = 'http://localhost/loja_cds/index.php'</script>";
        echo "<br>";
        echo "<a href='cd.php'>Adicionar produto</a>";
        echo "<br>";
        echo "<a href='compra.php'>Fazer compra</a>";
        echo "<br>";
        echo "<a href='crud.php'>Cadastrar cliente</a>";
    } else {
        echo "Erro na inserção de dados: " . $conn->error;
        echo "<br>";
        echo "<a href='cd.php'>Adicionar produto</a>";
        echo "<br>";
        echo "<a href='compra.php'>Fazer compra</a>";
        echo "<br>";
        echo "<a href='crud.php'>Cadastrar cliente</a>";
    }
}
?>

ETAPA 06:

6. Todas essas informações devem estar em um repositório do github, onde o grupo
colocará os diagramas, códigos SQL, consultas criadas e demais detalhes. Todos
os participantes devem constar nesse repositório, pode-se criar uma “organização”
onde todos de forma colaborativa construam a aplicação e mantenham ela no
repositório.







