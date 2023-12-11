>[!question] Duvida
>Porque temos um CSS para cada Root ? Os botões são iguais não ? Acredito que uma variante resolveria tudo.
##### FooterButtonsRootModal:

Talvez na condição do `if (newValueTooggle)`, tenhamos uma redundancia, pois o state ja está trazendo por default esse valor como false, fica como sugestão refatorar.
```ts
const handleToggle = (newValueTooggle?: boolean) => { setToggle(newValueTooggle ?? !toggle) }
```

Ou questão que temos é no codigo 
```ts
 const handleClick = () => {
    if (onFn() || false) return
    handleToggle()
  }
```

Acredito que seja melhor remover os `|| false`, pois isso é desnecessário.

```ts
const handleClick = () => {
    if (onFn && onFn()) return
    handleToggle()
  }
```

