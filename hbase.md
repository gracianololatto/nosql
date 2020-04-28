1.1. Crie a tabela com 2 famílias de colunas:
     a. personal-data
     b. professional-data
create 'italians', 'personal-data', 'professional-data'

1.2. Importe o arquivo via linha de comando
shell /tmp/italians.txt

Agora execute as seguintes operações:

2.1. Adicione mais 2 italianos mantendo adicionando informações como data de nascimento nas informações pessoais e um atributo de anos de experiência nas informações profissionais.
put 'italians', '11', 'personal-data:name', 'Joao Jessus'
put 'italians', '11', 'personal-data:city', 'Blumenau'
put 'italians', '11', 'personal-data:birthday', '01/01/1980'
put 'italians', '11', 'professional-data:role', 'Analista'
put 'italians', '11', 'professional-data:salary', '15000'
put 'italians', '12', 'professional-data:job_experience', '9'
put 'italians', '12', 'personal-data:name', 'Maria Jesus'
put 'italians', '12', 'personal-data:city', 'Blumenau'
put 'italians', '12', 'personal-data:birthday', '02/02/1980'
put 'italians', '12', 'professional-data:role', 'Especialista'
put 'italians', '12', 'professional-data:salary', '20000'
put 'italians', '12', 'professional-data:job_experience', '7'

2.2. Adicione o controle de 5 versões na tabela de dados pessoais.
alter 'italians', { NAME => 'personal-data', VERSIONS => '5' }

2.3. Faça 5 alterações em um dos italianos;
put 'italians', '12', 'professional-data:role', 'Jovem Aprendiz'
put 'italians', '12', 'professional-data:role', 'Estagiário'
put 'italians', '12', 'professional-data:role', 'Analista'
put 'italians', '12', 'professional-data:role', 'Especialista'
put 'italians', '12', 'professional-data:role', 'Coordernador'

2.4. Com o operador get, verifique como o HBase armazenou o histórico.
get 'italians', '12', { COLUMN => 'professional-data:role', VERSIONS => 5 }

2.5. Utilize o scan para mostrar apenas o nome e profissão dos italianos.
scan 'italians', { COLUMNS => ['personal-data:name', 'professional-data:role'] }

2.6. Apague os italianos com row id ímpar
deleteall 'italians', '1'
deleteall 'italians', '3'
deleteall 'italians', '5'
deleteall 'italians', '7'
deleteall 'italians', '9'
deleteall 'italians', '11'

2.7. Crie um contador de idade 55 para o italiano de row id 5
incr 'italians', '5', 'personal-data:age', 55

2.8. Incremente a idade do italiano em 1
incr 'italians', '5', 'personal-data:age', 1
