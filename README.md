# ![SAPOSalas](https://img.shields.io/badge/SAPOSalas-API_v1.7.0-8A2BE2?style=for-the-badge&logo=php&logoColor=white)

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
| **Local** | `http://saw.pt/PHP` | Servidor XAMPP |
| **Swagger-InfinityFree** | `https://sapossalas.rf.gd/api-docs/#/` | Swagger InfinityFree  |
| **Swagger-GitHub** | `https://arpaoceleste.github.io/saposalas-api-docs/` | Swagger GitHub  |

---

## 🟪 1. Backend API (JSON)

Estes endpoints retornam dados estruturados para operações assíncronas (JavaScript/AJAX).

### 🔮 Gestão 2FA (Google Auth) - **NOVO**
Gere a configuração, ativação e desativação do Google Authenticator.

* **Endpoint:** `/backend/api_2fa.php`
* **Método:** `POST`
* **Ações:** `generate_secret`, `verify_and_enable`, `disable`
* **Campos:** `code` (obrigatório para ativar)

**Exemplo de Resposta:**
```json
{
  "success": true,
  "qr_code_url": "[https://api.qrserver.com/v1/create-qr-code/](https://api.qrserver.com/v1/create-qr-code/)...",
  "secret": "JBSWY3DPEHPK3PXP"
}
```
🔮 Obter Ocupação (Grid)

Retorna a disponibilidade das salas e as reservas existentes para uma data.

    Endpoint: /backend/api_occupancy.php

    Método: GET

    Parâmetros: data (Y-m-d)

Exemplo de Resposta:
```json

{
  "success": true,
  "rooms": [ { "id": 1, "nome": "Sala A" } ],
  "reservations": [ { "id": 10, "room_id": 1, "start": "09:00", "end": "10:00" } ],
  "updated_at": "2023-10-25 14:00:00"
}
```
🔮 Segurança e Email (Legacy 2FA)

Gere o envio e validação de códigos de segurança via email (Login antigo, Eliminar Conta, Mudar Pass).

    Endpoint: /backend/api_security.php

    Método: POST

    Campos: action (send_code, verify_code), context, code, csrf_token

Exemplo de Resposta:
```json

{
  "success": true,
  "message": "Código validado com sucesso.",
  "action_required": "proceed_login"
}
```
🔮 Gestão de Utilizador

Atualização de perfil, alteração de palavra-passe e eliminação de conta.

    Endpoint: /backend/update_user.php

    Método: POST

    Ações: update_profile, update_password, execute_delete

Exemplo de Resposta:
```json

{
  "success": true,
  "message": "Dados de perfil atualizados com sucesso."
}
```
🔮 Detalhes da Sala (Modal)

Dados completos de uma sala para janelas modais.

    Endpoint: /backend/admin_room_details.php

    Método: GET

    Parâmetro: room_id (Inteiro)

Exemplo de Resposta:
```json

{
  "success": true,
  "data": {
    "id": 5,
    "nome": "Sala Azul",
    "galeria": [ "uploads/img1.jpg" ]
  }
}
```
🟪 2. Autenticação

Endpoints responsáveis pelo ciclo de vida da sessão.
Endpoint	Método	Descrição
```text
/login.php	POST	Híbrido: Valida credenciais (Formulário) OU valida código Google Auth (JSON via verify_google_2fa).

/criar-conta.php	POST	Cria conta inativa e envia email de confirmação.

/confirmar-conta.php	GET	Ativa a conta via token de email.

/repor-password.php	POST	Gere o pedido e definição de nova palavra-passe.

/logout.php	GET	Destrói a sessão e redireciona.
```
🟪 3. Administração e Reservas (Formulários)

Processamento de formulários HTML e redirecionamentos (302).
🔮 Gestão de Salas (CRUD)

Exclusivo para administradores.

    Endpoint: /backend/manage_rooms.php

    Método: POST

    Ações: adicionar, editar, eliminar

    Nota: Suporta upload de múltiplas imagens na galeria.

Exemplo de Payload (Multipart/Form-data):
Plaintext

action: adicionar
nome: Sala de Formação
galeria[]: (binary file)
csrf_token: a1b2c3d4...

🔮 Processar Reserva

Submissão de uma nova reserva.

    Endpoint: /backend/processar_reserva.php

    Método: POST

    Campos: room_id, data, hora_inicio, hora_fim, descricao

Exemplo de Payload (Form Data):
Plaintext

room_id: 3
data: 2025-12-12
hora_inicio: 09:00
hora_fim: 11:00
descricao: Reunião Geral
csrf_token: xyz789...

🔮 Gerir Reservas do Utilizador

Cancelamento ou edição pelo próprio utilizador.

    Endpoint: /backend/manage_user_reservations.php

    Método: POST

    Ações: cancel, edit

Exemplo de Payload (Form Data):
Plaintext

action: edit
id: 45
data: 2025-12-15
descricao: Alteração de horário
csrf_token: wxyz123...

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

    /perfil.php (ou userdashboard.php) - Área do utilizador

    /login.php - Formulário de acesso

🟣 Contactos

Para suporte técnico ou dúvidas sobre a integração:

    Equipa: SAPOSalas

    Email: infosaposalas@gmail.com




    🟣 Servers and Environments
Environment	Base URL	Description
Production	https://sapossalas.rf.gd	InfinityFree Server
Local	http://saw.pt/PHP	XAMPP Server
Swagger-InfinityFree	https://sapossalas.rf.gd/api-docs/#/	Swagger InfinityFree
Swagger-GitHub	https://arpaoceleste.github.io/saposalas-api-docs/	Swagger GitHub
🟪 1. Backend API (JSON)

These endpoints return structured data for asynchronous operations (JavaScript/AJAX).
🔮 2FA Management (Google Auth) - NEW

Manages the configuration, activation, and deactivation of Google Authenticator.

    Endpoint: /backend/api_2fa.php

    Method: POST

    Actions: generate_secret, verify_and_enable, disable

    Fields: code (required to activate)

Response Example:
```json

{
  "success": true,
  "qr_code_url": "https://api.qrserver.com/v1/create-qr-code/...",
  "secret": "JBSWY3DPEHPK3PXP"
}
```
🔮 Get Occupancy (Grid)

Returns room availability and existing reservations for a specific date.

    Endpoint: /backend/api_occupancy.php

    Method: GET

    Parameters: data (Y-m-d)

Response Example:
```json

{
  "success": true,
  "rooms": [ { "id": 1, "nome": "Room A" } ],
  "reservations": [ { "id": 10, "room_id": 1, "start": "09:00", "end": "10:00" } ],
  "updated_at": "2023-10-25 14:00:00"
}
```
🔮 Security and Email (Legacy 2FA)

Manages the sending and validation of security codes via email (Legacy Login, Delete Account, Change Password).

    Endpoint: /backend/api_security.php

    Method: POST

    Fields: action (send_code, verify_code), context, code, csrf_token

Response Example:
```json

{
  "success": true,
  "message": "Code validated successfully.",
  "action_required": "proceed_login"
}
```
🔮 User Management

Profile updates, password changes, and account deletion.

    Endpoint: /backend/update_user.php

    Method: POST

    Actions: update_profile, update_password, execute_delete

Response Example:
```json

{
  "success": true,
  "message": "Profile data updated successfully."
}
```
🔮 Room Details (Modal)

Complete data of a room for modal windows.

    Endpoint: /backend/admin_room_details.php

    Method: GET

    Parameter: room_id (Integer)

Response Example:
```json

{
  "success": true,
  "data": {
    "id": 5,
    "nome": "Blue Room",
    "galeria": [ "uploads/img1.jpg" ]
  }
}
```
🟪 2. Authentication

Endpoints responsible for the session lifecycle.
Endpoint	Method	Description

```text
/login.php	POST	Hybrid: Validates credentials (Form) OR validates Google Auth code (JSON via verify_google_2fa).
/criar-conta.php	POST	Creates inactive account and sends confirmation email.
/confirmar-conta.php	GET	Activates the account via email token.
/repor-password.php	POST	Handles password reset request and definition.
/logout.php	GET	Destroys the session and redirects.
```

🟪 3. Administration and Reservations (Forms)

HTML form processing and redirects (302).
🔮 Room Management (CRUD)

Exclusive to administrators.

    Endpoint: /backend/manage_rooms.php

    Method: POST

    Actions: adicionar (add), editar (edit), eliminar (delete)

    Note: Supports multiple image uploads to gallery.

Payload Example (Multipart/Form-data):
Plaintext

action: adicionar
nome: Training Room
galeria[]: (binary file)
csrf_token: a1b2c3d4...

🔮 Process Reservation

Submission of a new reservation.

    Endpoint: /backend/processar_reserva.php

    Method: POST

    Fields: room_id, data, hora_inicio (start_time), hora_fim (end_time), descricao (description)

Payload Example (Form Data):
Plaintext

room_id: 3
data: 2025-12-12
hora_inicio: 09:00
hora_fim: 11:00
descricao: General Meeting
csrf_token: xyz789...

🔮 Manage User Reservations

Cancellation or editing by the user themselves.

    Endpoint: /backend/manage_user_reservations.php

    Method: POST

    Actions: cancel, edit

Payload Example (Form Data):
Plaintext

action: edit
id: 45
data: 2025-12-15
descricao: Time change
csrf_token: wxyz123...

🟪 4. Page Structure (GET)

Mapping of public and backoffice pages.
💜 Public

    /index.php - Homepage

    /reservar.php - Search and filters

    /detalhes.php?id={N} - Room detail

    /pagina_sobrenos.php - About the team

    /termos_de_utilizador.php - Terms and conditions

💜 Private / System

    /admin.php - Administrative dashboard

    /perfil.php (or userdashboard.php) - User area

    /login.php - Login form

🟣 Contacts

For technical support or questions regarding integration:

    Team: SAPOSalas

    Email: infosaposalas@gmail.com
