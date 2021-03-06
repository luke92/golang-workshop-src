# Linea de comandos

## Argumentos

Interactuar con la linea de comando es muy util y muy comun al ejecutar scripts y programas que no tienen GUI. El paquete `os` se usa para tener acceso a los argumentos de la linea de comandos al ejecutar un programa de Golang.

Los argumentos de la linea de comandos estan disponibles en el arreglo `os.Args`:

```go
import "os"

os.Args // Lista completa incluyendo el nombre del programa
os.Args[1:] // Solo los argumentos
```

## Flags

Especificar los argumentos como valores separados por espacios en la terminal es muy basico y dificil de extender. El uso de `flags` provee mas flexibilidad en como los argumentos se especifican, sobre todo los opcionales. Golang cuenta con un paquete llamado `flag` para soportarlos.

```go
import "flag"

flag.<type>(nombre del flag, valor default, descripcion)
```

Un flag se define con la sintaxis anterior. El `<type>` puede ser `string`, `int` o `bool`.

Un flag opcional se puede indicar controlando si el valor es el mismo que el valor especificado por defecto.

Un flag se puede leer independientemente de la posicion en que el usuario los hubiera especificado.

Las flag se pasan en la ejecución del programa con la siguiente sintaxis `-flag="value"`

```
go run . -addr=":80"
```

## Environment Variables

La variables de entorno se usan para configurar aspectos de sistema en la mayoria de los *NIX y tambien en Windows. Son pares de clave-valor usualmente disponibles para todos los programas que corren en la terminal/shell. Se pueden definir variables de entorno custom solo disponibles durante la ejecucion de un script de shell.

El paquete `os` proporciona dos funciones, `Setenv` y `Getenv`, para escribir y leer variables de entorno. Un string vacio se retorna si la clave no existe.

```go
import "os"

os.Setenv("FOO", "1")
fmt.Println("FOO:", os.Getenv("FOO"))
fmt.Println("BAR:", os.Getenv("BAR"))

> FOO: 1
  BAR:
```

En el ejemplo anterior se le da a la variable de entorno `FOO` el valor `1` al comienzo del programa, y se lee el valor de la variable `BAR` desde la lista de variables de entorno existentes.

La funcion `Environ` retorna la lista completa de todas las variables de entorno existentes.

```go
import "strings"

for _, e := range os.Environ() {
    pair := strings.Split(e, "=")
    fmt.Println(pair[0])
}
```

La lista se retorna en el formato `KEY=VALUE`. Por la tanto el string se puede dividir en `=` para tener acceso a la clave y al valor. Esto se hace con la funcion `strings.Split` que retorna un arreglo.