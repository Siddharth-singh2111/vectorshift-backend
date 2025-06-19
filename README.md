This is the backend API for the VectorShift Pipeline Builder, built using FastAPI. It receives the pipeline graph from the frontend, validates its structure (e.g., checks if it's a valid DAG), and returns success or error messages.

🚀 Deployed at: https://vectorshift-backend.onrender.com/docs

🧠 What It Does
✅ Accepts nodes and edges as JSON via /validate endpoint

✅ Checks for basic validity (non-empty, properly connected graph)

✅ Can be extended to support:

DAG structure validation (no cycles)

Node/edge schema validation

Custom error messages

🗂 Project Structure
javascript
Copy
Edit
vectorshift-backend/
├── main.py              ← FastAPI app with `/validate` endpoint
├── requirements.txt     ← Python dependencies
🔍 File Breakdown
File	Purpose
main.py	Main entry file for FastAPI app, defines /validate endpoint
requirements.txt	Declares fastapi, uvicorn for deployment

🔧 /validate Endpoint
🔗 URL
bash
Copy
Edit
POST /validate
📥 Request Body
json
Copy
Edit
{
  "nodes": [ ... ],
  "edges": [ ... ]
}
✅ Successful Response
json
Copy
Edit
{
  "status": "success",
  "message": "Valid DAG"
}
❌ Error Response
json
Copy
Edit
{
  "status": "error",
  "message": "Empty graph"
}
🧪 How to Run Locally
✅ Step 1: Install dependencies
bash
Copy
Edit
cd vectorshift-backend
pip install -r requirements.txt
✅ Step 2: Run the server
bash
Copy
Edit
uvicorn main:app --reload --port 8000
Now open: http://localhost:8000/docs
👉 This opens Swagger UI to test /validate

🌍 Deployment (Render)
Already deployed at:

arduino
Copy
Edit
https://vectorshift-backend.onrender.com
Render Setup:
Setting	Value
Build Command	pip install -r requirements.txt
Start Command	uvicorn main:app --host 0.0.0.0 --port 10000
Port	10000 (Render requires this port)
Region	Singapore (closest to India)

⚠️ No environment variables are required.

📥 Example Request (for testing)
json
Copy
Edit
{
  "nodes": [
    { "id": "input_1", "type": "customInput" },
    { "id": "text_1", "type": "text" },
    { "id": "output_1", "type": "customOutput" }
  ],
  "edges": [
    { "source": "input_1", "target": "text_1" },
    { "source": "text_1", "target": "output_1" }
  ]
}
✅ CORS Enabled
python
Copy
Edit
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Or restrict to your frontend Vercel domain
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
