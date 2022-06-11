# 06 MoveBackToStateless

En el ejemplo 05 aprendimos como eliminar el estado de un control secundario para tener una gestión limpia del estado.

Es hora de hacer limpieza, simplificando el componente _[nameEdit.tsx](./src/nameEdit.tsx)_ convirtiéndolo en un componente sin estado.

Tomaremos como punto de partida el ejemplo _[05 Refactor](./../05%20Refactor)_.

## Pasos resumidos:

- Actualizar _[nameEdit.tsx](./src/nameEdit.tsx)_, convirtiéndolo en un componente sin estado y añadir los métodos inline.

## Prerrequisitos

Instalar [Node.js y npm](https://nodejs.org/en/) (v6.6.0 o superior) si aún no los tienes instalados en tu equipo.

> Verifica que estás usando al menos node v6.x.x y npm 3.x.x usando los comandos `node -v` y `npm -v` en un terminal/consola. Versiones anteriores pueden producir errores.

## Pasos para construirlo

- Copia el contenido de _[05 Refactor](./../05%20Refactor)_ y ejecuta `npm install`.

- Actualiza _[nameEdit.tsx](./src/nameEdit.tsx)_, convirtiendo en un componente sin estados y añadiendo los métodos inline. Debería verse como:

 ```jsx
import * as React from 'react';

interface Props {
    editingUserName : string;
    onEditingNameUpdated : (newEditingName : string) => void;
    onNameUpdateRequest : () => void;  
}

export const NameEditComponent = (props : Props) =>
  <div>
      <label>Update Name:</label>
      <input value={props.editingUserName}
        onChange={(e) : void => props.onEditingNameUpdated((e.target as HTMLInputElement).value)} />

      <button 
            onClick={props.onNameUpdateRequest}
      >
            Change
      </button>
  </div>
 ```

 Nota aclarativa: cuando refactorizamos este código, nosotros hemos remplazado ```this.props``` por ```props```. Esto es porque ```NameEditComponent``` es ahora una función, no una clase. Si tu guardas ```this.props```, falla en tiempo de ejecución porqué ```this``` es ahora undefined

- Ahora podemos arrancar el ejemplo y obtendremos los mismos resultados.

```bash
npm start
```