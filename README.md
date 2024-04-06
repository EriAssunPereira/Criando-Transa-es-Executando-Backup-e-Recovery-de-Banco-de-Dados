# Criando-Transa-es-Executando-Backup-e-Recovery-de-Banco-de-Dados
**Projeto de Desafio: Transações, Backup e Recovery de Banco de Dados**:

### **Parte 1 – Transações**

Nesta etapa, você relembrará como executar transações no MySQL. Aqui estão os passos principais:

1. **Desabilitar o Autocommit**: Antes de iniciar uma transação, é importante desativar o autocommit. Isso evita que cada instrução SQL seja confirmada automaticamente. Para desabilitar o autocommit, utilize o seguinte comando:

    ```sql
    SET autocommit = 0;
    ```

2. **Executar Consultas e Modificações de Dados**: Agora você pode executar suas instruções SQL dentro da transação. Por exemplo, para inserir dados em uma tabela:

    ```sql
    START TRANSACTION;
    INSERT INTO minha_tabela (coluna1, coluna2) VALUES ('valor1', 'valor2');
    COMMIT;
    ```

### **Parte 2 – Transação com Procedure**

Nesta parte, você criará uma transação dentro de uma **procedure**. A ideia é incluir uma verificação de erro e, se necessário, realizar um **ROLLBACK**. Aqui está um exemplo básico:

```sql
DELIMITER //
CREATE PROCEDURE minha_procedure()
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        -- Lógica para lidar com o erro (pode ser um log, mensagem, etc.)
    END;

    START TRANSACTION;
    -- Instruções SQL dentro da transação
    INSERT INTO minha_tabela (coluna1, coluna2) VALUES ('valor1', 'valor2');
    COMMIT;
END;
//
DELIMITER ;
```

### **Parte 3 – Backup e Recovery**

Nesta etapa, você realizará o backup do banco de dados e-commerce. Siga estas etapas:

1. Utilize o comando `mysqldump` para criar um backup do banco de dados:

    ```bash
    mysqldump -u seu_usuario -p sua_senha nome_do_banco_de_dados > backup.sql
    ```

2. Para restaurar o backup, utilize o seguinte comando:

    ```bash
    mysql -u seu_usuario -p sua_senha nome_do_banco_de_dados < backup.sql
    ```

3. Além disso, considere incluir outros recursos no backup, como **procedures** e **eventos**.

4. Por fim, adicione o arquivo de backup ao GitHub junto com o script utilizado.
