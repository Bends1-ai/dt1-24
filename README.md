[DT1 - Assigment 1 - Plan.docx](https://github.com/user-attachments/files/17792011/DT1.-.Assigment.1.-.Plan.docx)This project implements a Flask application that serves as a proxy to interact with the Huggingface Inference API. The aim of the assignment is to demonstrate the integration of backend development, Docker containerization, Google Cloud deployment, and frontend no-code tools like Bubble or Retool.

By completing this assignment, I learned how to build and deploy a backend system, integrate APIs, and create secure and user-friendly interfaces using modern technologies.

---

## **Plan**

### Assignment Goals:
1. **Backend Development**: Design a Flask-based proxy for interacting with the Huggingface API.
2. **Docker Containerization**: Build and deploy the backend in a Docker container.
3. **Google Cloud Platform Deployment**: Securely host the Dockerized application on a GCP Virtual Machine.
4. **Frontend Development**: Create a no-code user interface using Bubble or Retool.
5. **Security**: Implement firewall rules to restrict access to the backend.

### Assignment Outline:
- **Create Accounts**: Register on GitHub, Docker Hub, Huggingface, and Google Cloud.
- **Setup Development Environment**: Install necessary tools like Ubuntu Terminal, Docker Desktop.
- **Develop the Backend**: Clone the repository, modify the code, and test locally.
- **Containerization**: Build and push the Docker image to Docker Hub.
- **GCP Deployment**: Deploy the Dockerized application to a VM on GCP.
- **Frontend Integration**: Build no-code interfaces to interact with the backend.
- **Testing and Security**: Test the API and configure firewall rules.

---

## **Features**

- **Huggingface Proxy**: Interacts with Huggingface's text generation models.
- **No-Code Frontend**: User-friendly interfaces built on Bubble and Retool.
- **Dockerized Deployment**: Containerized backend for portability and scalability.
- **Secure Backend**: GCP-hosted backend with IP-restricted access.

---

## **Steps Completed**

### 1. Accounts Setup
- Registered accounts for:
  - [GitHub](https://github.com/)
  - [Docker Hub](https://www.docker.com/)
  - [Huggingface](https://huggingface.co/)
  - [Google Cloud](https://cloud.google.com/)

---

### 2. Development Environment Setup
- Installed tools:
  - **Ubuntu Terminal (Windows WSL)**: Simulated a Linux-based environment locally.
  - **Docker Desktop**: Built and tested Docker images locally.

---

### 3. Backend Development

#### Cloned the Repository:
```bash
git clone https://github.com/sid027/dt1-24.git
cd dt1-24

#### Built and Pushed the Docker Image Locally:
  - On your local machine, navigate to the directory with the Dockerfile from the GitHub repository you cloned.

    cd /mnt/c/Assignment/dt1-24

  - Build the Docker image using the command:

    sudo docker build -t yourusername/projectname:tag .
    -> Pie-1.0.0 à Pie
    Replace yourusername with your Docker Hub username “bends1”, projectname with the name you wish to give your project,
    and tag with the version of this build (commonly latest for the most recent build).
    Create Docker Hub personnal account “bends1”

    docker build -t bends1/imgassignment:Pie .

  - Push the Docker Image to Docker Hub:

    Log in to Docker Hub from your command line using:docker login
    Enter your Docker Hub credentials when prompted.

    Once logged in, push the Docker image to Docker Hub using: docker push bends1/imgassignment:Pie

    Verify the Push: After the command completes, log into your Docker Hub account at https://hub.docker.com/.
    Navigate to Repositories. Ensure the imgassignment repository contains your image with the Pie tag.

  - Tested the Docker Image Locally: docker run -p 8080:8080 bends1/imgassignment:Pie

  - Create a Hugging Face account and create an API Key :


#### Start a Virtual Machine (VM) on Google Cloud Platform:
  - Go to the Google Cloud Console.
  - Navigate to the Compute Engine and then to VM instances.
  - Click on ‘Create instance’ to set up a new VM, we called it “vm-assignment”
  - Select the boot disk with a preferred OS (Ubuntu for Docker deployments).
  - Allow HTTP/HTTPS traffic in the firewall settings during creation.
  - SSH into the virtual machine by clicking on 'SSH/connect'

  ** Created and Configured a VM **

    VM Name: vm-assignment
    External IP: 34.56.232.196
    Firewall Rules: Allowed HTTP/HTTPS traffic.

#### Install Docker on the VM:
Once the VM is set up, SSH into it from the Google Cloud Console or use an SSH client with the VM's IP.
 - Update the package list: sudo apt-get update

 - Install Docker on the VM: sudo apt-get install docker.io

#### Pull the Docker Image and Run It:
Once Docker is installed,
 - pull your Docker image from Docker Hub: docker pull bends1/imgassignment:Pie

 - Run the Docker container on VM: docker run –p 8080:5000 bends1/imgassignment:Pie
Adjust the port mappings (-p 8080:5000) as necessary based on how your application is configured.

#### Set Up Security Settings for the Backend:
 - Go back to the Google Cloud Console.
 - Navigate to the VPC Network and then to Firewall rules.
 - Create a new firewall rule to limit access to the ports your application uses (port 8080 for HTTP).
   Allowed HTTP traffic only on port 8080.
 - Specify target tags (http-server)
 - Firewall the system so that only you can access the system (Access should be blocked from any IP other than mine : 194.230.146.0.)

#### Frontend Development:

 - Huggingface Token:
   Generated a token: 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

 - Create the frontend Bubble/Retool interface with the appropriate elements (I've tried it on both)

** Bubble Interface: **
Input Field (ID: Input1): Accepts user input for the prompt.
Output Field (ID: Output1): Displays the API response.
Button (ID: Button1): Triggers the API call.

** Retool Interface: **
called it "textcompletion Interface"
Input Field (ID: Input1): Accepts user input for the prompt.
Output Field (ID: Output1): Displays the API response.
Button (ID: Button1): Triggers the API call.


#### Testing the Backend:

 - API Testing:
   Used curl to test the backend API:

   curl "http://34.56.232.196:8080/chat?model_id=gpt2&huggingface_token=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&input=Life%20is"

 - Response:
   {
  "ack": "model loaded and ready"
   }

   Which confirms that Flask API is working correctly and accessible from server

#### Connecting Frontend to Backend:

  - API Endpoint:
   Connected Bubble and Retool to. Used Retool for testing, Output1 is now displaying "model loaded and ready",
   it confirms that your query1 is working and the binding is successfully displaying the API's response.

   ** Query Configuration using Retool **

   Resource : TextCompletionAPI
   Method: GET http://34.56.232.196:8080/chat http://34.56.232.196:8080/chat /load_model?model_id=gpt2&huggingface_token=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&input={{Input1.value}}
   Description: Generates text completion based on user input.
   Parameters:
          - model_id (string): gpt2.
          - huggingface_token (string): API token.
          - input (string): User input.

   /load_model
   Method: GET
   Description: Preloads the Huggingface model for optimization.
   Parameters:
          - model_id (string): Model to preload.
          - huggingface_token (string): API token.

#### Security:

- Firewall Rules: Port 8080 restricted to authorized IPs (194.230.146.0).
- Collaborators Added: Josh Levent Siddhartha Singh

#### Conclusion:
This assignment demonstrates:

*Integration of APIs with a Flask-based backend.
*Efficient use of Docker for containerization and deployment.
*Secure deployment on Google Cloud Platform.
*Practical use of no-code tools like Bubble and Retool for user-friendly interfaces.

Attached File : 
[DT1 - Assigment 1 - Plan.docx](https://github.com/user-attachments/files/17792027/DT1.-.Assigment.1.-.Plan.docx)

