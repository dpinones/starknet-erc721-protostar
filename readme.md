# ERC721 en StarkNet con Protostar

El tutorial a realizar es [ERC721](https://github.com/starknet-edu/starknet-erc721) de la gente de Staknet-edu.
Este repositorio es una copia del tutorial original pero se encuentra adaptado para poder realizar el mismo con la herramienta Protostar.

## Resumen del tutorial
Consiste en modificar el contrato ERC721.cairo dependiendo las [consignas](https://github.com/starknet-edu/starknet-erc721#tasks-list), hacer el deploy en testnet y luego en el contrato evaluador subir el address del contrato que estuvimos trabajando. Y de esta forma obtener puntos y seguir avanzando.

## Configuración
### Step 1 - Clonar el repositorio
```bash
git clone https://github.com/dpinones/starknet-erc721-protostar.git
cd starknet-erc721-protostar
```
### Step 2 - Instalar curl 
```bash
sudo apt install curl
```

### Step 3 - Instalar protostar
```bash
curl -L https://raw.githubusercontent.com/software-mansion/protostar/master/install.sh | bash
```

Reiniciar el terminal

Ver la versión que instalamos
```bash
protostar -v
>> Protostar version: 0.4.2                                                        
>> Cairo-lang version: ^0.10.0
```

### Step 4 - Instalar la biblioteca de OpenZeppelin
```bash
protostar install https://github.com/OpenZeppelin/cairo-contracts
```

### Step 5 - Build al contrato
```bash
protostar build
```

### Step 6 - Realizar el deploy en tesnet

Para realizar el deploy del ERC721 necesitamos pasarle parámetros nombre, símbolo, y un address.
El address en este caso tiene que ser el del contrato evaluador que es: x2d15a378e131b0a9dc323d0eae882bfe8ecc59de0eb206266ca236f823e0a15.
Para el nombre y el simbolo debemos convertir los string en int(al final se explica como hacer). Si queremos hacer el deploy del ERC721 con:
nombre = 'STARKNET' = 6004496024898258260
símbolo = 'STARK' = 357895852619

Quedaría de la siguiente manera
```bash
protostar deploy ./build/ERC721.json --network alpha-goerli -i 6004496024898258260 357895852619 0x2d15a378e131b0a9dc323d0eae882bfe8ecc59de0eb206266ca236f823e0a15
```

Listo ya realizo el deploy de su contrato. Ahora puede continuar en [consignas](https://github.com/starknet-edu/starknet-erc721#tasks-list)

## Convertir string a int

Puede convertir un string en un int utilizando el editor online https://www.cairo-lang.org/playground/ 

Utilice el siguiente código
```
%builtins output

from starkware.cairo.common.serialize import serialize_word

func main{output_ptr : felt*}():
    tempvar x = 'STARKNET'
    serialize_word(x)
    return ()
end
```

Ejemplo
<img src="/exampleCairoPlayground.png" alt="Example string to int"/>

Debe copiar el int que retorna Program output. 
Reemplazar el contenido de las comillas para convertir un string en int.


## Links

- [Documentación de Protostar](https://docs.swmansion.com/protostar/docs/tutorials/introduction)
- [Henri explica como realizar el tutorial ERC721](https://www.youtube.com/watch?v=PJWIgIoj5kw)
- [OpenZeppelin Contracts for Cairo](https://github.com/OpenZeppelin/cairo-contracts)
