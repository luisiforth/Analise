>[!Alerta]
>Corrigir os any's🔥🔥
##### CSS:
 >[!caution] Refatorar, temos algumas redundâncias, ou até mesmo processamento de estilos mais do que o necessário.
 >Ex:.
>>[!example]-
>>
>>``` ts
>> const HeaderRoot = styled.header`
    ${({ theme }) => css`
    width: 100%;
    height: 100%;  // <--- Remover esta linha é redundante ou
    max-height: 54px; // <--- Remover esta linha é redundante.
    ... 
>> ```
 
>[!note] Variantes
>Utilizar mais as variantes com o Styled Components:
>``` ts
const variantStyles = (theme: DefaultTheme, variant = 'primary') =>
  ({
    primary: css`
      color: ${theme.colors.light};
      background: ${theme.colors.primary};
      border: 1px solid ${theme.colors.primary};
    `
  }[variant])
>```
### Componentes

###### ComponentMemorando:

Talvez o melhor seja guardar o maping dentro de um memo.

>[!example]-
>``` ts
const memorandoItems = useMemo(() => {
  return memorando.map((v) => (
    <div key={v.IDMEM}></div>
  ));
}, [memorando]);
>```

##### Page-header: 
 
 Para melhor visualização, quand há muitas props, realizar a desestruturação.
>[!example]-
> ```ts
 >// Antes
 >export function PageHeaderRoot({
  >title,
  >children,
  >haveReturn,
  >memorandum
>}: PageHeaderProps) {
 ...
>}
 >
> // Depois:
 >export function PageHeaderRoot(props: PageHeaderProps) {
>	const { children, title, haveReturn, memorandum } = props
>	...
 >}
>```
##### PageHeaderFilter: 

No trecho a seguir, nos passamos o 3x o props por componentes.
```ts
{toggleFilter && <PageFilter onToggle={handleToggleFilter} {...props} />}
```

Acredito que seja melhor revermos o conceito deste componentes, e evitar este tipo de acontecimento.

- FormFilter: 
	Temos uma repetição de código, no qual uma função com useCallBack e  parâmetros para auxilio da performance.
``` ts
    const newValueOfRelief =
      selectedValues.relief?.value !== 0
        ? {
            label: selectedValues.relief?.label,
            value: selectedValues.relief?.value
          }
        : undefined
```

O ``methods.setError('unitId', { type: 'required' })`` dentro do handleReset, é necessário, não seria uma redundância  ? Zod já não gera o `methods.formState.errors` diretamente, ou não podemos utilizar uma função ja pronta para realizar estas validações, como `.refine()`
```ts
  const handleReset = () => {
    handleSelectedValue('initialDate', format(hooks.INITIAL_DATE, 
    'yyyy-MM-dd'))
    handleSelectedValue('finalDate', format(new Date(), 'yyyy-MM-dd'))
    removeFilters()
    methods.reset()
    methods.setError('unitId', { type: 'required' }) //< --- Necessário ?
    methods.setError('lineId', { type: 'required' }) //< --- Necessário ?
  }
```

>[!note] Nota
>Utilizar o pattern de factory seria algo interessante para separar alguns comportamentos do nosso código.
>
>>[!example]-
>>```ts
>  const handleReset = () => {
    handleSelectedValue('initialDate', format(hooks.INITIAL_DATE,
     'yyyy-MM-dd'))
    handleSelectedValue('finalDate', format(new Date(), 'yyyy-MM-dd'))
    removeFilters()
    methods.reset()
    methods.setError('unitId', { type: 'required' })
    methods.setError('lineId', { type: 'required' })
  }
>>```
>Por:
>>```ts
>>  const handleResetMethods = () => {
>>   methods.reset()
>>   methods.setError('unitId', { type: 'required' })
>>   methods.setError('lineId', { type: 'required' })
>> }
>>```
>>```ts
>> const handleReset = () => {
>>   handleSelectedValue('initialDate', format(hooks.INITIAL_DATE,
>>    'yyyy-MM-dd'))
>>   handleSelectedValue('finalDate', format(new Date(), 'yyyy-MM-dd'))
>>   removeFilters()
>>   handleResetMethods() <---- Factory
>> }
>>```

>[!caution] Cuidado
>Dentro do `filter-format.tsx` encontramos uma redundância, pois, dentro do hook a função handleSelectedValue, se encarrega de retornar o valor 0 por default para certos casos. 
>```ts
 event?.value ? handleSelectedValue('formats', event.value) : handleSelectedValue('formats', 0)
>```

