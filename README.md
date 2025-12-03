<img src="static/images/bookheadedBannerREADME.svg" style="height: 18rem; align-self: center;">

📖 BookHub

Bem-vindo ao BookHub! Uma rede social literária focada na criação e gestão de comunidades de leitura, com uma identidade visual imersiva. O objetivo é centralizar discussões, engajar leitores com maratonas e facilitar a gestão de clubes de leitura.

📂 Estrutura do Projeto

O sistema foi desenvolvido utilizando Django (Python) no backend e HTML/CSS/Bootstrap no frontend. Abaixo, um resumo técnico dos principais componentes:

🐍 Backend (Arquivos .py)

A lógica de negócios reside principalmente no aplicativo site_cc, gerenciando a interação entre o usuário e o banco de dados SQLite.

models.py: Define a arquitetura do banco de dados.

Principais Tabelas: Clube (núcleo do sistema), Profile (dados do usuário e seguidores), Membro, Enquete, Voto e HistoricoMaratona.

views.py: Controla as regras de negócio e o fluxo de dados.

Gerencia a lógica de gamificação (Maratonas), sistema de follow/unfollow, criação de enquetes e renderização das páginas.

forms.py: Manipula e valida a entrada de dados.

Utilizado para o registro de usuários, criação de clubes e edição de perfil.

urls.py: Roteamento da aplicação, definindo os caminhos para acesso às views (ex: /clube/<id>, /perfil/<user>).

🎨 Frontend (Telas .html)

A interface utiliza o sistema de templates do Django, com um design system próprio focado em tons escuros e destaque em vermelho vinho.

Estrutura Base:

base.html: O layout mestre que contém o <head>, importações de CSS/JS e estrutura global.

navbar.html: Barra de navegação responsiva presente em todas as páginas logadas.

Telas Principais:

login.html & register.html: Telas de autenticação com animações interativas e validação de formulário.

club.html: Página principal de exploração, contendo carrossel de destaques e listagem de clubes com filtros.

clubDetail.html: O painel de controle do clube. Exibe a barra de progresso de leitura, chat (comentários), enquetes ativas e o pódio de livros favoritos.

profile.html: Perfil do usuário exibindo biografia, estatísticas (seguidores/seguindo), badges e clubes favoritados.

addclub.html: Interface para criação de novas comunidades com animações dinâmicas baseadas no input do usuário.

⚙ Tecnologias

Backend: Python, Django

Frontend: HTML5, CSS3, JavaScript, Bootstrap

Banco de Dados: SQLite

Projeto desenvolvido na disciplina de Desenvolvimento Web.


