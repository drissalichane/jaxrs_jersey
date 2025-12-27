# Testing Instructions

You can test the application using `curl` or by using the H2 Console.

## Prerequisites
- Ensure the application is running (e.g., via `mvn spring-boot:run` or your IDE).
- The server runs on **port 8082**.

## 1. H2 Console
Access the in-memory database at:
[http://localhost:8082/h2-console](http://localhost:8082/h2-console)

- **JDBC URL**: `jdbc:h2:mem:banque`
- **User Name**: `sa`
- **Password**: (Empty)

## 2. API Testing with Curl

### Get All Accounts (JSON)
```bash
curl -X GET "http://localhost:8082/banque/comptes" -H "Accept: application/json"
```

### Get All Accounts (XML)
```bash
curl -X GET "http://localhost:8082/banque/comptes" -H "Accept: application/xml"
```

### Get Account by ID
```bash
curl -X GET "http://localhost:8082/banque/comptes/1" -H "Accept: application/json"
```

### Create New Account
```bash
curl -X POST "http://localhost:8082/banque/comptes" \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -d '{"solde": 4500.0, "type": "COURANT", "dateCreation": "2024-12-27T00:00:00.000+00:00"}'
```

### Update Account
```bash
curl -X PUT "http://localhost:8082/banque/comptes/1" \
     -H "Content-Type: application/json" \
     -d '{"solde": 6000.0, "type": "EPARGNE", "dateCreation": "2024-12-27T00:00:00.000+00:00"}'
```

### Delete Account
```bash
curl -X DELETE "http://localhost:8082/banque/comptes/1"
```

## 3. Testing with SOAP UI

Since this is a REST API, you can use SOAP UI to create a REST project and test the endpoints.

### 3.1 Download and Install
If you don't have SOAP UI, you can download the **Open Source** version for free:
1.  Go to the official [SoapUI Open Source Downloads](https://www.soapui.org/downloads/soapui/) page.
2.  Download the installer for your OS (Windows, macOS, or Linux).
3.  Install usage instructions are typically straightforward: run the installer and follow the wizard.

### 3.2 Setup Project
1.  **Create Project**: Open SOAP UI -> File -> New REST Project.
2.  **URI**: Enter `http://localhost:8082`.
3.  **Define Resources**: Add a resource named `/banque/comptes`.

### Test Cases

**Get All Accounts**
- Method: GET
- Resource: `/banque/comptes`
- Header: `Accept: application/json` or `application/xml` (click on the 'Header' tab at the bottom).

**Get Account by ID**
- Method: GET
- Resource: `/banque/comptes/{id}`. Add a parameter `id` (e.g. `1`) with Style "TEMPLATE".
- Request: `http://localhost:8082/banque/comptes/1`

**Create Account**
- Method: POST
- Resource: `/banque/comptes`
- Media Type: `application/json`
- Request Body (in the payload window):
  ```json
  {
      "solde": 8000.0,
      "type": "EPARGNE",
      "dateCreation": "2024-12-28T10:00:00.000+00:00"
  }
  ```

**Update Account**
- Method: PUT
- Resource: `/banque/comptes/{id}` (e.g., id=1)
- Media Type: `application/json`
- Request Body:
  ```json
  {
      "solde": 9500.0,
      "type": "COURANT",
      "dateCreation": "2024-12-28T10:00:00.000+00:00"
  }
  ```

**Delete Account**
- Method: DELETE
- Resource: `/banque/comptes/{id}` (e.g., id=1)

