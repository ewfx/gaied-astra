# 🚀 Project Name

## 📌 Table of Contents
- [Introduction](#introduction)
- [Demo](#demo)
- [Inspiration](#inspiration)
- [What It Does](#what-it-does)
- [How We Built It](#how-we-built-it)
- [Challenges We Faced](#challenges-we-faced)
- [How to Run](#how-to-run)
- [Tech Stack](#tech-stack)
- [Team](#team)

---

## 🎯 Introduction
A Flask-based API for classifying email content and attachments (PDF, DOCX, EML, or plain text) using OpenAI's GPT model.

Features

- Classify single files or multiple files in bulk
- Supports PDF, DOCX, EML, and plain text files
- Duplicate detection using content hashing
- Configurable request types and sub-types
- Swagger/OpenAPI documentation
- Parallel processing for bulk classification

## 🎥 Demo
🔗 [Live Demo](#) (if applicable)  
- Not Applicable
- 📹 [Video Demo](#) (if applicable)  
- (https://github.com/ewfx/gaied-astra/blob/main/artifacts/demo/demo_part1.mp4)
- (https://github.com/ewfx/gaied-astra/blob/main/artifacts/demo/demo_part2.mp4)
- 🖼️ Screenshots:
- (https://github.com/ewfx/gaied-astra/blob/main/code/test/TestReport/Test%20result.docx)


## 💡 Inspiration
What inspired you to create this project? Describe the problem you're solving.

## ⚙️ What It Does
- API: [http://localhost:7100](http://localhost:7100)
- Swagger documentation: [http://localhost:7100/apidocs](http://localhost:7100/apidocs)

## API Endpoints

### Classify Single File

- **Endpoint:** `POST /classify`
- **Content-Type:** `multipart/form-data`
- **Parameters:**
  - `file`: The file to classify (PDF, DOCX, EML, or plain text)

### Bulk Classify Multiple Files

- **Endpoint:** `POST /bulk_classify`
- **Content-Type:** `multipart/form-data`
- **Parameters:**
  - `files`: Multiple files to classify (use "Add Item" in Swagger UI)

### Update Configuration

- **Endpoint:** `POST /update_config`
- **Content-Type:** `application/json`
- **Parameters:**
  - JSON body with new request types configuration

## Example Requests

### Using cURL
```bash
# Single file classification
curl -X POST -F "file=@example.pdf" http://localhost:7100/classify

# Bulk classification
curl -X POST \
  -F "files=@file1.pdf" \
  -F "files=@file2.docx" \
  http://localhost:7100/bulk_classify

# Update configuration
curl -X POST -H "Content-Type: application/json" \
  -d '{"request_types": {"New Type": ["Subtype1", "Subtype2"]}}' \
  http://localhost:7100/update_config
```



## 🛠️ How We Built It
Briefly outline the technologies, frameworks, and tools used in development.

## 🚧 Challenges We Faced
- Extracting structured data from unstructured emails, PDFs, and DOCX files can be tricky. Text extraction may not always be clean, leading to noisy data for processing.
- The OpenAI free tier may have limitations on the number of requests and usage, so the challenge is to fine-tune the AI model with limited data and ensure it can generalize well to unseen requests.
- Identifying exact duplicates across different formats (e.g., an email and a PDF with the same content) can be challenging. We need to handle cases where a request is similar but not
- Automatically determining the priority of a request is not always straightforward. Requests may require additional contextual understanding that the AI needs to infer from keywords and context.
- The system needs to be efficient enough to process large volumes of incoming requests in real-time or near-real-time.

## 🏃 How to Run
## Prerequisites

- Python 3.7+
- MongoDB (running locally or via connection string)
- OpenAI API key

## Setup

### Clone the repository:
```bash
git clone https://github.com/your-repo/email-classifier-api.git
cd email-classifier-api
```

### Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Install dependencies:
```bash
pip install -r requirements.txt
```

### Configuration:

Create a `config.yml` file in the root directory with your request types:
```yaml
request_types:
  "Money Movement – Outbound": ["Timebound", "Recurring"]
  "Account Maintenance": ["Update Details", "Close Account"]
  "Information Request": ["Balance", "Statement"]
```

Set your OpenAI API key in `app.py`:
```python
classifier = Classifier(api_key="your-openai-api-key")
```

Configure MongoDB connection in `database.py` if needed.

## Running the Application

### Start the Flask development server:
```bash
python app.py
```

### Access the API:

### Using Python Requests
```python
import requests

# Single file
with open('example.pdf', 'rb') as f:
    response = requests.post('http://localhost:7100/classify', files={'file': f})
    print(response.json())

# Multiple files
files = [('files', open('file1.pdf', 'rb')), ('files', open('file2.docx', 'rb'))]
response = requests.post('http://localhost:7100/bulk_classify', files=files)
print(response.json())
```

## Requirements

Ensure `requirements.txt` includes:

```text
flask==2.3.2
flasgger==0.9.5
python-docx==0.8.11
pdfminer.six==20221105
pymongo==4.3.3
pyyaml==6.0
openai==0.27.8
python-dotenv==1.0.0
concurrent-log-handler==0.9.20
```

## Deployment

For production, consider using:

- Gunicorn or uWSGI as the WSGI server
- Nginx as a reverse proxy
- Docker for containerization

### Example Dockerfile:
```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY . .

RUN pip install -r requirements.txt

EXPOSE 7100
CMD ["gunicorn", "--bind", "0.0.0.0:7100", "app:app"]
```

## Troubleshooting

- **Swagger UI not showing multiple file upload:** Ensure you're using the "Add Item" button in Swagger UI.
- **MongoDB connection issues:** Verify MongoDB is running and the connection string is correct.
- **File processing errors:** Check file types and sizes (large files may need special handling).

   ```

## 🏗️ Tech Stack

- 🔹 Backend: Python / Flask
- 🔹 Database: MongoDB
- 🔹 Other: OpenAI API 

## 👥 Team
- **Prerna Kumari** 
- **Veena Kumari Reddypalli**
- **Prameet K Pradhan**
- **Ravikanth Pratti**
- **Archana Paliath**
