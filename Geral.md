>[!alerta]
>Melhorar a nomenclatura de variáveis, e diminuir a complexidade dos códigos para uma manutenção mais rápida e melhor ambientação.
>Ex:. createSetupObjects.ts
>```ts
>21:  return data.map((l: DataG) => {
> ```
> "l" é uma variável atribuída ao tipo DataG, mas o que em si significa o l ? No caso l significa line.

>[!note]
>Uma boa prática é realivazer estas validações 
>``` ts
> {memorandum && memorandum.length > 0 && (
          <ComponentMemorando memorando={memorandum} />
        )}
>```
>Dentro do próprio componente.
>
>Ex:.
>```ts
><ComponentMemorando memorando={memorandum} />
>
>// No componente 'ComponentMemorando' realizar a validação de render:
>const ComponentMemorando = ({ memorando }: PropsMemorando) => {
  if (!memorandum || memorandum.length === 0)  return null;  	
>...
>```
>

>[!question]
>Deixar todos os types em apenas uma pasta separada no topo do projeto ?

>[!Note]
> Verificar a viabilidade de utilizar useCallback ou useMemo em funções, e o componente memo, para componentes com renderizações pesadas.

>[!question]
>Talvez não seria interessante mudar o método de render da pagina ?
>Atualmente geramos a página por Server Side, mas e se gerarmos a página no building, salvando tudo de primeiro momento, deixando as funções de render via Client. isso faria com que a página não realizasse o Side novamente, deixando em cargo de um refetch do mutate. (Algo semelhante ao que temos no mobile, e na tela de cadastros), trabalharíamos com uma SPA.
>

# Conteudos

## Tópicos:
 - Componentes:
    -  [[Headers]]
    - [[StepModel]]
- Pages:
    - [[Server Side]]
    - [[Apontamento Parada]]
