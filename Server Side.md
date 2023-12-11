> [!note]
> Separar uma parte do código, repetimos isso em todos os Server Sides, conseguimos reduzir isso para um Hook, ou função.
> ```js
> const filters = cookies[COOKIE_FILTER_NAME]
      ? (JSON.parse(
          cookies[COOKIE_FILTER_NAME]
        ) as StorageFiltersType<'default'>)
      : null
   const isValidFilters =
      filters &&
      filters.line &&
      filters.unit &&
      filters.initialDate &&
      filters.finalDate
   if (!isValidFilters) {
      return {
        props: {
          data: [],
          total: 0
        }
      }
    }  
>``` 
> Também  podemos fazer uma função apropriada para este 
>```js
   const validDates = {
      final: dateFormatValidate(filters.finalDate)
        ? filters.finalDate
        : format(parseISO(filters.finalDate), 'dd/MM/yyyy'),
      initial: dateFormatValidate(filters.initialDate)
        ? filters.initialDate
        : format(parseISO(filters.initialDate), 'dd/MM/yyyy')
       }
> ``` 




    
       
    


