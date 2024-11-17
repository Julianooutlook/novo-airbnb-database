# Novo Airbn

# O objetivo aqui é descrever como eu organizaria um banco de dados que precisa, no inicio de:

⏭️Usuários;

⏭️Lugares para se hospedar - cadastrados pelos usuários;

⏭️ Hospedagens (um período de tempo no qual usuário Y vai ficar no lugar X) - realizadas também por usuários;

⏭️ Avaliações feitas pelos usuários nas hospedagens.


📍 A descrição deve conter: 

⏭️ Nomes de tabelas que você faria;

⏭️ Colunas que você acha mais importantes nas tabelas;

⏭️ Relacionamentos delas e como ficaria nas colunas das tabelas;

⏭️ Uma explicação mínima de o que te levou por essas decisões.
#


# Tabela: Usuarios

<ins>Colunas:</ins>

***UsuarioID (PK, INT, auto-increment): Identificador único do usuário.***

***Nome (VARCHAR, NOT NULL): Nome completo do usuário.***

***Email (VARCHAR, UNIQUE, NOT NULL): Endereço de e-mail para login e contato.***

***SenhaHash (VARCHAR, NOT NULL): Hash da senha para autenticação segura.***

***Telefone (VARCHAR): Número de telefone do usuário.***

***DataCadastro (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP): Data de registro do usuário.***

***Explicação: Essa tabela é fundamental para armazenar as informações dos usuários, garantindo a segurança dos dados de login e suporte a funcionalidades de autenticação.***
#
# Tabela: Lugares

<ins>Colunas:</ins>

***LugarID (PK, INT, auto-increment): Identificador único do lugar.***

***UsuarioID (FK, INT, NOT NULL): Referência ao proprietário do lugar (relacionado a Usuarios).***

***Titulo (VARCHAR, NOT NULL): Título descritivo do lugar.***

***Descricao (TEXT): Descrição detalhada do lugar.***

***Endereco (VARCHAR, NOT NULL): Localização do lugar.***

***PrecoPorNoite (DECIMAL, NOT NULL): Preço de estadia por noite.***

***Capacidade (INT, NOT NULL): Número máximo de hóspedes permitidos.***

***DataCriacao (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP): Data de cadastro do lugar.***

***Explicação: Essa tabela representa as propriedades listadas pelos usuários, armazenando informações essenciais para exibição e reservas.***
#
# Tabela: Hospedagens

<ins>Colunas:</ins>

***HospedagemID (PK, INT, auto-increment): Identificador único da hospedagem.***

***UsuarioID (FK, INT, NOT NULL): Referência ao usuário que realiza a hospedagem (relacionado a Usuarios).***

***LugarID (FK, INT, NOT NULL): Referência ao lugar reservado (relacionado a Lugares).***

***DataInicio (DATE, NOT NULL): Data de início da hospedagem.***

***DataFim (DATE, NOT NULL): Data de término da hospedagem.***

***Status (VARCHAR, DEFAULT 'pendente'): Estado da hospedagem (ex.: "confirmada", "concluída", "cancelada").***

***Explicação: A tabela de Hospedagens liga usuários e lugares com detalhes do período da reserva, sendo crucial para o gerenciamento de disponibilidade e históricos de hospedagem.***
#
# Tabela: Avaliações

<ins>Colunas:</ins>

***AvaliacaoID (PK, INT, auto-increment): Identificador único da avaliação.***

***HospedagemID (FK, INT, NOT NULL): Referência à hospedagem avaliada (relacionado a Hospedagens).***

***UsuarioID (FK, INT, NOT NULL): Referência ao autor da avaliação (relacionado a Usuarios).***

***Nota (INT, NOT NULL, CHECK (Nota BETWEEN 1 AND 5)): Classificação da avaliação (ex.: 1 a 5).***

***Comentario (TEXT): Comentário adicional sobre a experiência.***

***DataAvaliacao (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP): Data de publicação da avaliação.***

***Explicação: As avaliações estão vinculadas a hospedagens e usuários, permitindo feedback detalhado e a construção da reputação dos locais e dos hóspedes.***
#
# Relacionamentos

***Usuarios e Lugares: Relacionamento 1, onde um usuário pode cadastrar múltiplos lugares (UsuarioID em Lugares).***

***Usuarios e Hospedagens: Relacionamento 1, onde um usuário pode fazer múltiplas hospedagens (UsuarioID em Hospedagens).***

***Lugares e Hospedagens: Relacionamento 1, onde um lugar pode ter múltiplas hospedagens (LugarID em Hospedagens).***

***Hospedagens e Avaliacoes: Relacionamento 1:1, onde uma hospedagem pode ter uma única avaliação (HospedagemID em Avaliacoes).***

# ***Essa estrutura foi projetada para oferecer flexibilidade e escalabilidade. A separação de Hospedagens e Avaliacoes permite que avaliações sejam feitas apenas após a conclusão de uma hospedagem, garantindo a veracidade do feedback. As referências com chaves estrangeiras asseguram a integridade dos dados e simplificam consultas complexas para relatórios e análises.***