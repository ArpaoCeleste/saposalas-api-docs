# ![SAPOSalas](https://img.shields.io/badge/SAPOSalas-API_v1.5.0-8A2BE2?style=for-the-badge&logo=php&logoColor=white)

> **Documentação técnica completa do sistema de reservas.**
> Abrange APIs JSON (AJAX), processamento de formulários (POST) e estrutura de páginas (GET).

![Status](https://img.shields.io/badge/Status-Operacional-blueviolet?style=flat-square)
![Tech](https://img.shields.io/badge/Backend-PHP-9370DB?style=flat-square)
![Data](https://img.shields.io/badge/Data-JSON-mediumpurple?style=flat-square)

---

## 🟣 Servidores e Ambientes

| Ambiente | URL Base | Descrição |
| :--- | :--- | :--- |
| **Produção** | `https://sapossalas.rf.gd` | Servidor InfinityFree |
| **Local** | `http://localhost/saposalas` | Servidor XAMPP |

---

## 🟪 1. Backend API (JSON)

Estes endpoints retornam dados estruturados para operações assíncronas (JavaScript/AJAX).

### 🔮 Obter Ocupação (Grid)
Retorna a disponibilidade das salas e as reservas existentes para uma data.

* **Endpoint:** `/backend/api_occupancy.php`
* **Método:** `GET`
* **Parâmetros:** `data` (Y-m-d)

**Exemplo de Resposta:**
```json
{
  "success": true,
  "rooms": [
    {
      "id": 1,
      "nome": "Sala A"
    }
  ],
  "reservations": [
    {
      "id": 10,
      "room_id": 1,
      "start": "09:00",
      "end": "10:00"
    }
  ],
  "updated_at": "2023-10-25 14:00:00"
}
```
##🔮 Segurança e 2FA

Gere o envio e validação de códigos de segurança via email.

    Endpoint: /backend/api_security.php

    Método: POST

    Campos: action (send_code, verify_code), context, code, csrf_token

🔮 Gestão de Utilizador

Atualização de perfil, alteração de palavra-passe e eliminação de conta.

    Endpoint: /backend/update_user.php

    Método: POST

    Ações: update_profile, update_password, execute_delete

🔮 Detalhes da Sala (Modal)

Dados completos de uma sala para janelas modais.

    Endpoint: /backend/admin_room_details.php

    Método: GET

    Parâmetro: room_id

🟪 2. Autenticação

Endpoints responsáveis pelo ciclo de vida da sessão.
Endpoint	Método	Descrição
/login.php	POST	Valida credenciais e inicia o fluxo de 2FA.
/criar-conta.php	POST	Cria conta inativa e envia email de confirmação.
/confirmar-conta.php	GET	Ativa a conta via token de email.
/repor-password.php	POST	Gere o pedido e definição de nova palavra-passe.
/logout.php	GET	Destrói a sessão e redireciona.
🟪 3. Administração e Reservas (Formulários)

Processamento de formulários HTML e redirecionamentos (302).
🔮 Gestão de Salas (CRUD)

Exclusivo para administradores.

    Endpoint: /backend/manage_rooms.php

    Método: POST

    Ação: adicionar, editar, eliminar

    Nota: Suporta upload de múltiplas imagens na galeria.

🔮 Processar Reserva

Submissão de nova reserva.

    Endpoint: /backend/processar_reserva.php

    Método: POST

    Campos: room_id, data, hora_inicio, hora_fim, descricao

🔮 Gerir Reservas do Utilizador

Cancelamento ou edição pelo próprio utilizador.

    Endpoint: /backend/manage_user_reservations.php

    Método: POST

    Ação: cancel, edit

🟪 4. Estrutura de Páginas (GET)

Mapeamento das páginas públicas e de backoffice.
💜 Públicas

    /index.php - Homepage

    /reservar.php - Pesquisa e filtros

    /detalhes.php?id={N} - Detalhe da sala

    /pagina_sobrenos.php - Sobre a equipa

    /termos_de_utilizador.php - Termos e condições

💜 Privadas / Sistema

    /admin.php - Dashboard administrativo

    /login.php - Formulário de acesso

🟣 Contactos

Para suporte técnico ou dúvidas sobre a integração:

    Equipa: SAPOSalas

    Email: infosaposalas@gmail.com
