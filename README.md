![image](https://github.com/user-attachments/assets/35a17b1c-961d-4cb5-9a10-379c584c4065)# DBA Challenge 20240802


## Introdução

Nesse desafio trabalharemos utilizando a base de dados da empresa Bike Stores Inc com o objetivo de obter métricas relevantes para equipe de Marketing e Comercial.

Com isso, teremos que trabalhar com várioas consultas utilizando conceitos como `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `GROUP BY` e `COUNT`.

### Antes de começar
 
- O projeto deve utilizar a Linguagem específica na avaliação. Por exempo: SQL, T-SQL, PL/SQL e PSQL;
- Considere como deadline da avaliação a partir do início do teste. Caso tenha sido convidado a realizar o teste e não seja possível concluir dentro deste período, avise a pessoa que o convidou para receber instruções sobre o que fazer.
- Documentar todo o processo de investigação para o desenvolvimento da atividade (README.md no seu repositório); os resultados destas tarefas são tão importantes do que o seu processo de pensamento e decisões à medida que as completa, por isso tente documentar e apresentar os seus hipóteses e decisões na medida do possível.
 
 ## O projeto

- Criar as consultas utilizando a linguagem escolhida;
- Entregar o código gerado do Teste.

### Modelo de Dados:

Para entender o modelo, revisar o diagrama a seguir:

![<img src="samples/model.png" height="500" alt="Modelo" title="Modelo"/>](samples/model.png)


## Selects

Construir as seguintes consultas:

- Listar todos Clientes que não tenham realizado uma compra;
   
 /* Aqui, uso left join entre a tabela customers e a tabela orders, pois, ele me trará todos os registros da tabela customers, mesmo que eles não existam
    na tabela orders. Em seguida, utilizo o Null na cláusula where para filtrar apenas os clientes que não possuem registros na tabela orders, significando
    que eles ainda não realizaram nenhuma compra */
  
  select
         customers.*
  from
         customers
  left join
         orders
  on
         customers.customer_id = orders.customer_id
  where
         orders.customer_id is null
 
- Listar os Produtos que não tenham sido comprados

  /* Aqui, uso left join entre a tabela products e a tabela order_items, pois, ele me trará todos os registros da tabela products, mesmo que eles não existam
     na tabela order_items. Em seguida, utilizo o Null na cláusula where para filtrar apenas os produtos que não possuem registros na tabela order_items,               significando que eles ainda não foram comprados. */
  
 select
        products.*
 from
        products
 left join
        order_items
 on
       products.product_id = order_items.product_id
 where
       order_items.product_id is null

- Listar os Produtos sem Estoque;

  /* Aqui, uso um inner join entre as tabelas products e stocks, utilizando como filtro na cláusula where, o campo quantity da tabela stocks igual a 0.
     Supondo que, todos os registros da tabela stocks tenham sido inseridos com algum valor que seja 0 ou qualquer número acima dele. No caso, desconsiderei a           possibilidade de qualquer um dos registros estar com o campo quantity igual a Null, já que considero isso um problema na inserção deles e não deveria
      existir. */
  
  select
        products.*
  from
        products
  inner join
        stocks
  on
        products.product_id = stocks.product_id
  where
        stocks.quantity = 0

- Agrupar a quantidade de vendas que uma determinada Marca por Loja.

  /*Aqui, mesmo que eu não precisasse trazer dados da tabela products, foi necessário incluí-la, pois, ela é a única que possuí ligação com a tabela
    brands, utilizada para consultar as marcas. No caso das demais, as usei para trazer as lojas(tabela stores) e poder contar as vendas(tabela orders).
    Por fim, ordenei os registros por marca e loja, respectivamente. 
  
  select
        brands.brand_name,
        stores.store_name,
        count(orders.order_id) as count_orders
  from
       products
  inner join
       order_items
  on
       products.product_id = order_items.product_id
  inner join
       orders
  on
       order_items.order_id = orders.order_id
  inner join
       stores
  on
       orders.store_id = stores.store_id
  inner join
       brands
  on
       products.brand_id = brands.brand_id
  group by
       brands.brand_name,
       stores.store_name
  order by
       brands.brand_name,
       stores.store_name
  
- Listar os Funcionarios que não estejam relacionados a um Pedido.

  /* Aqui, uso left join entre a tabela staffs e a tabela orders, pois, ele me trará todos os registros da tabela staffs, mesmo que eles não existam
    na tabela orders. Em seguida, utilizo o Null na cláusula where para filtrar apenas os funcionários que não possuem registros na tabela orders, significando
    que eles não estão relacionados a nenhum pedido /*
   
  select
         staffs.*
  from
         staffs
  left join
         orders
  on
         staffs.staff_id = orders.staff_id
  where
         orders.staff_id is null
  

## Readme do Repositório

- Deve conter o título do projeto
- Uma descrição sobre o projeto em frase
- Deve conter uma lista com linguagem, framework e/ou tecnologias usadas
- Como instalar e usar o projeto (instruções)
- Não esqueça o [.gitignore](https://www.toptal.com/developers/gitignore)
- Se está usando github pessoal, referencie que é um challenge by coodesh:  

>  This is a challenge by [Coodesh](https://coodesh.com/)

## Finalização e Instruções para a Apresentação

1. Adicione o link do repositório com a sua solução no teste
2. Verifique se o Readme está bom e faça o commit final em seu repositório;
3. Envie e aguarde as instruções para seguir. Caso o teste tenha apresentação de vídeo, dentro da tela de entrega será possível gravar após adicionar o link do repositório. Sucesso e boa sorte. =)


## Suporte

Para tirar dúvidas sobre o processo envie uma mensagem diretamente a um especialista no chat da plataforma. 
