# picoCTF – Heap Dump (Web Exploitation)

## Challenge Walkthrough

### Step 1: Exploring the Web Application

The challenge starts with a simple blog-style website. After launching the instance, I navigated through the available pages and paid attention to any references to internal functionality.

One article mentioning **API Documentation** stood out. Clicking it redirected me to the Swagger UI interface located at:

/api-docs


Swagger UI exposed the available API endpoints and allowed interaction with them directly from the browser.

---

### Step 2: Identifying the Critical Endpoint

While reviewing the documented routes, I focused on endpoints that appeared internal or diagnostic in nature. Under the **Diagnosing** section, the following endpoint immediately stood out:

GET /heapdump


The description suggested that this endpoint generated a memory dump, which aligned perfectly with the challenge objective.

---

### Step 3: Executing the Endpoint

Using Swagger’s **“Try it out”** feature, I executed the `/heapdump` endpoint.  
This action caused the server to generate and download a `.heapsnapshot` file containing the application’s runtime memory.

Alternatively, the endpoint could be accessed directly via the browser:

http://verbal-sleep.picoctf.net:57495/heapdump



---

### Step 4: Extracting the Flag

Heap dump files can be extremely large, so instead of manually inspecting the file, I searched for the expected flag format.

On Windows, I used [Ctrl + F] and searched for "picoctf"

This quickly revealed the flag stored in plaintext within the server’s memory.
picoCTF{Pat!3nt_15_Th3_K3y_1c3af720}



Security Takeaway

This challenge demonstrates the danger of leaving debug or diagnostic endpoints publicly accessible. Heap dumps can expose sensitive data such as credentials, tokens, and secrets, and should never be exposed in production environments.
