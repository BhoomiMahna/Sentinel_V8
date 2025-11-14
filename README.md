# 🚀 Space Station Object Detection Deployment

This project deploys a custom-trained **YOLOv8 model** (from the Duality AI Hackathon) using a high-performance **FastAPI** backend and a **React** frontend for real-time object detection.

## 🛠️ I. Environment and Setup

### A. Python Backend Setup

1.  **Dependencies:** Navigate to the **`backend/`** directory in your terminal and install all required packages:
    ```bash
    pip install fastapi uvicorn[standard] ultralytics opencv-python-headless numpy python-multipart
    ```

2.  **Model Placement (Crucial Step):** The application loads your trained weights (`best.pt`) directly from the root of the `backend/` directory.
    * **Action:** Copy your final trained weights file, **`best.pt`**, and paste it directly into the **`backend/`** folder.

### B. Node/React Frontend Setup

1.  **Dependencies:** Navigate to your **`frontend/`** directory.
    ```bash
    npm install  # or yarn install
    ```

***

## ⚙️ II. Execution and Running the Model

### 1. Start the Backend API

* **Terminal 1:** Navigate to the **`backend/`** folder and run the server:
    ```bash
    python -m uvicorn main:app --reload
    ```
* **Verification:** The API is ready when you see: `Uvicorn running on http://127.0.0.1:8000` and `Application startup complete.`

### 2. Start the Frontend Application

* **Terminal 2:** Navigate to the **`frontend/`** folder and start the React app:
    ```bash
    npm start
    ```
* **Verification:** The application should open in your browser (typically `http://localhost:3000`).

***

## 🔬 III. Testing and Expected Outputs

### A. Testing Procedure

1.  In the running frontend, use the **"Choose from Gallery"** button to select a test image.
2.  Click the **"Process Image"** button.
3.  The request is sent to the backend, the model predicts the objects, and the response is sent back.

### B. Expected Output and Interpretation

The frontend displays the processed image with **red bounding boxes** and **labels** drawn over the detected objects.

| Feature | Backend Source | Interpretation |
| :--- | :--- | :--- |
| **Bounding Box** | `box_2d: [xmin, ymin, xmax, ymax]` | The precise location of the detected object. |
| **Label** | `label: "Space_Tool"` | The classified object type. |
| **Confidence** | `confidence: 0.98` | The model's certainty in the prediction. |

***

## 📜 IV. Key Solution Details

| Component | Technology | Configuration Notes |
| :--- | :--- | :--- |
| **Model** | **YOLOv8** | Loaded using `YOLO('best.pt')` in `yolo_model_loader.py`. |
| **Backend** | **FastAPI** | Uses Pydantic for robust API response schema validation. |
| **Networking** | **API URL** | Frontend connects to `"http://127.0.0.1:8000/detect"`. |
