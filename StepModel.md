
#### Root:
Rever algumas funções dentro do código, pois temos redundâncias.
```ts 
const closeAndResetForm = useCallback(
    (toggle = false) => {
      methods.reset()
      onToggle()
      changeStep(0) //  <---- Uma das redundâncias:
      retornoPush(router)
      footerButtons.handleToggle(toggle)
    },
    [router, methods]
  )
```


#### Componente de Seleção (Combo Box):
Criar um componente para este item facilita na hora da implantar.
```ts
 <S.Form.Label>
   Selecione o produto: * <Text.Sup>(campo obrigatório)</Text.Sup>
 </S.Form.Label>
 <Controller
   control={methods.control}
   name="product"
   render={({ field }) => (
     <S.Form.Select
       ref={field.ref}
       options={product}
       value={product?.find(
         (product) => product.value === valuesSelecteds.product
       )}
       isLoading={mutateProduct.isLoading}
       placeholder="Selecione  ou pesquise um produto"
       isSearchable
       onChange={(val) => {
         const event = val as OptionValue<number>
         event?.value ? field.onChange(event?.value) : field.onChange(0)
         setValuesSelecteds((prev) => ({
           ...prev,
           product: event.value || 0
         }))
       }}
     />
    )}
 />
```

#### Bloqueio do Comportamento do avançar:
Realizar um Hook para isto:
```ts
const checkRequiredField = (
    fieldName: (keyof newAddStoppedApointamentData)[]
  ) => {
    const method = methods.watch(fieldName)
    return method.every((element: string | number | undefined) => {
      if (element == undefined) return false
      const value = parseInt(element as string)
      return value > 0
    })
  }
  
  useEffect(() => {
    onRequired(
      () => !checkRequiredField(['equip', 'product', 'stopreason', 'typeStopped'])
    )
  }, [methods.watch(['equip', 'product', 'stopreason', 'typeStopped'])])
```