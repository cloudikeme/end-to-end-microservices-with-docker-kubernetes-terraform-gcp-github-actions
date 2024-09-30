# **Part 3: Create Code for Individual Microservices in Repository**

In **Part 3** of the **Mastering Microservices** series, we will start building the core functionality of the **conference application** by creating code for each of the microservices using **Next.js** for the frontend and **Go** for the backend services. Specifically, we’ll implement the **Frontend**, **C4P (Call for Papers) Service**, **Agenda Service**, and **Notifications Service**.

If you'd prefer to skip the manual coding and directly use the pre-written code, you can clone the official repository and move on to the next article.

---

## **Skip Writing Code: Copy from the Official Repository**

To skip the manual setup and move forward quickly, clone the official repository where all the code is pre-written:

```bash
git clone https://github.com/cloudikeme/mastering-microservices-with-azure-docker-kubernetes-terraform-github-actions.git
```

Navigate to the `services/` directory to access the code for all the microservices, and once cloned, you can proceed directly to [**Part 4: Difference Between Containers and Images**](#).

---

## **Step-by-Step Guide to Creating Microservices (For Those Who Want to Code)**

For readers who want to write the code themselves, we will now create the code for each microservice step-by-step, using **Next.js** for the frontend and **Go** for the backend services.

---

## **Microservices Overview**

We will build the following core microservices:

1. **Frontend Service**: The user interface for users to interact with the application (**Next.js**).
2. **C4P (Call for Papers) Service**: Manages the submission of talk proposals (**Go**).
3. **Agenda Service**: Handles the scheduling and retrieval of the conference agenda (**Go**).
4. **Notifications Service**: Sends notifications (via Kafka, built in **Go**).

---

## **Step 1: Organize the Services in the Repository**

Ensure your repository is structured as follows to support multiple microservices:

```bash
conference-microservices-app/
│
├── services/               
│   ├── frontend/              # Frontend service (Next.js)
│   ├── c4p-service/           # C4P service (Go)
│   ├── agenda-service/        # Agenda service (Go)
│   └── notifications-service/ # Notifications service (Go, Kafka)
│
└── ...
```

Each microservice will have its own directory under `services/` to ensure separation of concerns and modularity.

---

## **Step 2: Create the Frontend Service with Next.js**

We will use **Next.js**, a React-based framework for building production-ready web applications with server-side rendering.

### **1. Initialize the Next.js Application**

1. Navigate to the `frontend` directory:

   ```bash
   cd services/frontend
   ```

2. Use **Create Next App** to initialize the project:

   ```bash
   npx create-next-app@latest frontend-app
   ```

3. Start the development server:

   ```bash
   cd frontend-app
   npm run dev
   ```

   The app will be available at `http://localhost:3000`.

### **2. Create Basic Pages for Conference Application**

In the `pages` folder, replace `index.js` to reflect the purpose of the conference app:

```jsx
import Head from 'next/head';

export default function Home() {
  return (
    <div>
      <Head>
        <title>Conference Application</title>
      </Head>
      <main>
        <h1>Welcome to the Conference Application</h1>
        <p>Submit your talk proposals and view the conference agenda here.</p>
      </main>
    </div>
  );
}
```

We will later extend this frontend to connect with the **C4P** and **Agenda** services via API calls.

---

## **Step 3: Create the C4P (Call for Papers) Service Using Go**

### **1. Initialize the C4P Service**

We’ll use **Go** to create the backend service that allows speakers to submit their talk proposals.

1. Navigate to the `c4p-service` directory:

   ```bash
   cd ../../c4p-service
   ```

2. Create a basic Go project:

   ```bash
   go mod init c4p-service
   ```

3. Create the main `server.go` file:

   ```bash
   touch server.go
   ```

4. Write the server code in `server.go`:

   ```go
   package main

   import (
       "encoding/json"
       "log"
       "net/http"
   )

   type Proposal struct {
       SpeakerName string `json:"speaker_name"`
       Topic       string `json:"topic"`
       Email       string `json:"email"`
   }

   func submitProposal(w http.ResponseWriter, r *http.Request) {
       var proposal Proposal
       err := json.NewDecoder(r.Body).Decode(&proposal)
       if err != nil {
           http.Error(w, err.Error(), http.StatusBadRequest)
           return
       }
       // You would normally save this data to a database here.
       log.Printf("Received proposal from %s for topic: %s", proposal.SpeakerName, proposal.Topic)
       w.WriteHeader(http.StatusOK)
       w.Write([]byte("Proposal submitted successfully"))
   }

   func main() {
       http.HandleFunc("/submit", submitProposal)
       log.Println("C4P Service is running on http://localhost:3001")
       log.Fatal(http.ListenAndServe(":3001", nil))
   }
   ```

### **2. Run the C4P Service**

To run the service:

```bash
go run server.go
```

The service will now listen for POST requests at `http://localhost:3001/submit`.

---

## **Step 4: Create the Agenda Service Using Go**

The **Agenda Service** will handle fetching and managing the conference schedule.

### **1. Initialize the Agenda Service**

1. Navigate to the `agenda-service` directory:

   ```bash
   cd ../agenda-service
   ```

2. Initialize the Go project:

   ```bash
   go mod init agenda-service
   ```

3. Create the `server.go` file:

   ```bash
   touch server.go
   ```

4. Write the server code for managing the agenda in `server.go`:

   ```go
   package main

   import (
       "encoding/json"
       "log"
       "net/http"
   )

   type AgendaItem struct {
       Session string `json:"session"`
       Time    string `json:"time"`
   }

   func getAgenda(w http.ResponseWriter, r *http.Request) {
       agenda := []AgendaItem{
           {Session: "Keynote", Time: "09:00 AM"},
           {Session: "Microservices Architecture", Time: "10:30 AM"},
           {Session: "Lunch Break", Time: "12:00 PM"},
       }
       json.NewEncoder(w).Encode(agenda)
   }

   func main() {
       http.HandleFunc("/agenda", getAgenda)
       log.Println("Agenda Service is running on http://localhost:3002")
       log.Fatal(http.ListenAndServe(":3002", nil))
   }
   ```

### **2. Run the Agenda Service**

To run the service:

```bash
go run server.go
```

The service will now be available at `http://localhost:3002/agenda`, and it will return a static conference agenda in JSON format.

---

## **Step 5: Create the Notifications Service Using Go and Kafka**

The **Notifications Service** will use Kafka to send messages to other services or users.

### **1. Initialize the Notifications Service**

1. Navigate to the `notifications-service` directory:

   ```bash
   cd ../notifications-service
   ```

2. Initialize the Go project:

   ```bash
   go mod init notifications-service
   ```

3. Create the `main.go` file:

   ```bash
   touch main.go
   ```

### **2. Write the Go Code for Kafka Integration**

For now, we will simulate a simple notification system (Kafka integration will be added later).

In `main.go`:

```go
package main

import (
    "fmt"
    "log"
    "net/http"
)

func notify(w http.ResponseWriter, r *http.Request) {
    if r.Method == http.MethodPost {
        fmt.Fprintf(w, "Notification sent")
        log.Println("Notification sent successfully")
    } else {
        http.Error(w, "Invalid request method", http.StatusMethodNotAllowed)
    }
}

func main() {
    http.HandleFunc("/notify", notify)
    log.Println("Notifications Service is running on http://localhost:3003")
    log.Fatal(http.ListenAndServe(":3003", nil))
}
```

### **3. Run the Notifications Service**

To run the service:

```bash
go run main.go
```

The service will now listen for POST requests at `http://localhost:3003/notify` to simulate sending notifications.

---

## **Step 6: Test the Microservices Locally**

You can test each of the services by interacting with their respective APIs:

- **Frontend**: Available at `http://localhost:3000`.
- **C4P Service**: Accepts POST requests at `http://localhost:3001/submit`.
- **Agenda Service**: Responds to GET requests at `http://localhost:3002/agenda`.
- **Notifications Service**: Accepts POST requests at `http://localhost:3003/notify`.

In later parts, we will integrate these services, add data storage, and implement Kafka for the notifications.\

Now, once you are done with this step, you can proceed to [**Part 4: Difference Between Containers and Images**](#).