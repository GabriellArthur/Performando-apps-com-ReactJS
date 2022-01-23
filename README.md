# memo | useMemo | useCallBack | Virtualização | Bundle Analyzer
<img alt="Ignite" src="https://i.imgur.com/eCVyxxy.png">

1. Criar uma nova versão do componente (memo - evita a criação caso não tenha alterações)
2. Comparar com a versão anterior 
3. Se houverem alterações, vai atualizar o que alterou

memo faz shallow compare => comparação rasa 

Pior momento é fazer calculo na hora de rendeziação

{} === {} /false
javascript faz igualdade referencial

# memo
1. Pure Functional Componentes = componentes puros (retorna sempre a mesma coisa)
2. Renderes too often = componentes que renderizam de mais
3. Re-renderes with same props = rendereizam muitas vezes com as mesmas propriedades
4. medium to big size = ganhar muita perfomace

# useMemo/useCallBack
useMemo = eveitar que evite muito processamento toda vezes que o componente renderizar 
<br/>
1- Cálculos pesados
<br/>
2- igualdade referencial (quando a gente repassa aquela informação para o componente filho)
<br/><br/>
useCallBack = memorizar uma função
<br/>
1- uma função fica pesada por igualdade referencial e não por quantidade de linhas
<br/>
# Dividingo o Código (code splitting)
yarn dev = gera um arquivo bundle.js | build.js 

react
```tsx
import {lazy} from 'react'
```
next
```tsx
import dynamic from 'next/dynamic'
```

```tsx
   import {AddProductToWishlistProps} from './AddProductToWishlist'

   const AddProductToWishlist = dynamic<AddProductToWishlistProps>(()=>{
      return import('./AddProductToWishlist').the(mod => mod.AddProductToWishlist)
   },{
      loading: () => <span>Carregando...</span>
   })
```
Outro exemplo:

```tsx
async function showFormattedDate(){
   const {format} = await import('date-fns')

   format()
}
```

# Virtualização
(telas com muitas informações, permite que a gente mostre em tela apenas os itens que cabem na tela do usuario)

[Bibilioteca](http://bvaughn.github.io/react-virtualized/#/components/List)

```jsx
import { List, ListRowRenderer } from 'react-virtualized';

  const rowRenderer: ListRowRenderer = ({ index, key, style }) => {
    return (
      <div key={key} style={style}>
        <ProductItem
          product={results[index]}
          onAddToWishlist={onAddToWishlist}
        />
      </div>
    );
  };

   <List
      width={900} 
      height={300}
      rowHeight={30}
      overscanRowCount={5}       //Quantos itens eu quero deixar pre-carregaveis para cima e para baixo
      rowCount={results.length}  //Quantos itens tem na lista no max
      rowRenderer={rowRenderer}  //rendereziar cada item da lista
   />
```
# Bundle Analyzer
Ver o peso do nosso bundle na nossa aplicação

[npm](https://www.npmjs.com/package/@next/bundle-analyzer)

# Execução da aplicação

instalação das dependencias 
```jsx
yarn
```

subindo a aplicação front-end (localhost:3000)
```jsx
yarn dev
```

subindo o servidor local (localhost:3333)
```jsx
yarn server
```
