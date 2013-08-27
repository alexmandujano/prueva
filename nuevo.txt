<?php
$mysqli=mysqli_init();
$mysqli->options(MYSQLI_OPT_INT_AND_FLOAT_NATIVE,1);

$mysqli ->real_connect("localhost", "root", "root", "world");
if ($mysqli->connect_errno) {
    echo "Falló la conexión a MySQL: (" . $mysqli->connect_errno . ") " . $mysqli->connect_error;
}

if (!$mysqli->query("DROP TABLE IF EXISTS test1") ||
    !$mysqli->query("CREATE TABLE test1(id INT, etiqueta CHAR(1))") ||
    !$mysqli->query("INSERT INTO test1(id, etiqueta) VALUES (1, 'a')")) {
    echo "Falló la creación de la tabla: (" . $mysqli->errno . ") " . $mysqli->error;
}

$resultado = $mysqli->query("SELECT id, etiqueta FROM test1 WHERE id = 1");
$fila = $resultado->fetch_assoc();

printf("id = %s (%s)\n", $fila['id'], gettype($fila['id']));
printf("etiqueta = %s (%s)\n", $fila['etiqueta'], gettype($fila['etiqueta']));
?>