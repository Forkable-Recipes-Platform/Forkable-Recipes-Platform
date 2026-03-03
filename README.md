# 🍴 Forkable Recipes Platform

**Autora:** Thais Gomes  

Uma plataforma social de receitas inspirada no conceito de *fork* do GitHub, onde usuários podem postar receitas, derivar versões modificadas e acompanhar a linhagem de cada criação.

---

## 📌 Descrição

O **Forkable Recipes Platform** é uma aplicação que permite:

- Publicar receitas originais  
- Favoritar receitas de outros usuários  
- Criar versões derivadas (*forkar*) de receitas existentes  
- Visualizar a linhagem completa de uma receita  

A proposta é aplicar o conceito de versionamento colaborativo ao universo culinário.

---

## 👤 Perfis

### 👩‍🍳 Usuário (Chefe)
- Criar receitas
- Forkar receitas
- Favoritar receitas

### 🛠 Administrador
- Gerenciar usuários
- Moderar conteúdos

---

## 🧠 Lógica de Negócio

### 📖 Publicação de Receita
Um usuário pode publicar uma receita original.

---

### ⭐ Sistema de Favoritos
- Relação Many-to-Many  
- Um usuário pode favoritar várias receitas  
- Uma receita pode ser favoritada por vários usuários  

---

### 🍴 Sistema de Fork

Ao forkar uma receita, o sistema deve:

1. Criar uma nova receita no banco de dados  
2. Associar a nova receita ao usuário que realizou o fork  
3. Manter referência à receita original através do campo `forked_from_id`  

Exemplo:

Usuário A → Receita 10 (Original)
Usuário B → Receita 11 (forked_from_id: 10)
Usuário C → Receita 15 (forked_from_id: 11)


O frontend deve exibir a linhagem, por exemplo:

> "Versão de C, derivada da receita de B, originalmente criada por A."

---

## ✅ Requisitos Funcionais

- **RF-01:** O usuário deve poder postar uma receita original  
- **RF-02:** O usuário deve poder forkar uma receita existente  
- **RF-03:** O sistema deve permitir forks encadeados (fork de fork)  
- **RF-04:** O usuário deve poder favoritar qualquer receita  

---

## ⚙️ Requisitos Não Funcionais

- **RNF-01 (Performance):**  
  A exibição da árvore de derivações deve ser otimizada para evitar consultas ineficientes no banco de dados.

- **RNF-02 (Armazenamento):**  
  O sistema deve permitir upload e associação de fotos às receitas.

---

## 🗄️ Modelagem Simplificada

### Entidade Usuario
- id  
- nome  
- email  
- senha  

### Entidade Receita
- id  
- titulo  
- descricao  
- ingredientes  
- modo_preparo  
- usuario_id  
- forked_from_id (nullable)  

### Tabela Favoritos
- usuario_id  
- receita_id  

---

## 🌳 Estrutura de Linhagem

Receita 10 (A)

└── Receita 11 (B)

  └── Receita 15 (C)
