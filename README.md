# Gesture Control Air-Mouse

This project uses a standard webcam and the TensorFlow Object Detection API to control your computer's mouse with hand gestures. It recognizes different hand poses in real-time to move the cursor, left-click, and right-click.

## Features

* **Mouse Movement:** Use a 'pinch' gesture to move the cursor.
* **Left Click:** Use a 'single' finger gesture.
* **Right Click:** Use a 'double' finger gesture.
* **Real-time:** All detection and control happens in real-time via your webcam.
* **Visualization:** An OpenCV window shows your webcam feed with the detection boxes overlaid (can be toggled).

## Technology Stack

* **Python 3.10**
* **TensorFlow 2 Object Detection API**
* **OpenCV** (for webcam capture and display)
* **PyAutoGUI** (for mouse control)

---

## Installation Guide (Corrected & Verified)

This project has very specific dependencies. These steps have been verified to resolve all common build and version conflicts (like `protobuf` and C++ build errors).

### 1. Prerequisites

You must install these tools on your system first.

1.  **Git:** Download and install from [git-scm.com](https://git-scm.com/).

2.  **Python 3.10:** This is critical. **Do not use Python 3.11 or newer**, as it will cause build failures.
    * Download and install **Python 3.10** from the [official site](https://www.python.org/downloads/windows/).
    * **Important:** During installation, check the box that says **"Add Python 3.10 to PATH"**.

3.  **Protocol Buffer Compiler (`protoc`) v3.19.6:**
    * Go to the [protoc v3.19.6 release page](https://github.com/protocolbuffers/protobuf/releases/tag/v3.19.6).
    * Download `protoc-3.19.6-win64.zip`.
    * Create a new folder on your computer, e.g., `C:\protoc`.
    * Unzip the file and copy the `bin` and `include` folders into `C:\protoc`.
    * Add this folder to your Windows System Environment **`PATH`** variable: `C:\protoc\bin`

### 2. Clone Repositories

1.  Clone this repository from your GitHub account:
    ```powershell
    git clone [https://github.com/clawalone/gesture-control-mouse.git](https://github.com/clawalone/gesture-control-mouse.git)
    cd gesture-control-mouse
    ```

2.  Clone the TensorFlow Models repository into the `API` folder, as required by the script:
    ```powershell
    mkdir API
    cd API
    git clone [https://github.com/tensorflow/models.git](https://github.com/tensorflow/models.git)
    ```

### 3. Setup Environment & Install Dependencies

This is the most important part. We will install all packages in a specific order to avoid conflicts.

1.  Navigate to the `models/research` directory:
    ```powershell
    cd models/research
    ```

2.  Create a Python virtual environment:
    ```powershell
    python -m venv venv
    ```

3.  Activate the environment:
    ```powershell
    .\venv\Scripts\activate
    ```
    *(Your terminal prompt should now start with `(venv)`)*

4.  Upgrade `pip` (the Python package manager):
    ```powershell
    python -m pip install --upgrade pip
    ```

5.  **Install the "Golden Key" Dependencies:**
    We install these *first* to prevent all the build errors you faced. This combination is known to be stable.
    ```powershell
    pip install "protobuf==3.19.6"
    pip install "Cython<3.0"
    pip install PyYAML==5.3.1
    ```

6.  **Compile the Protobuf Files:**
    Now that we have the right compiler (`protoc 3.19.6`) and library (`protobuf 3.19.6`), we can compile the files.
    ```powershell
    protoc object_detection/protos/*.proto --python_out=.
    ```

7.  **Install the TensorFlow Object Detection API:**
    ```powershell
    cp object_detection/packages/tf2/setup.py .
    python -m pip install .
    ```

8.  **Install Project Dependencies:**
    Finally, go back to your project's root folder and install `OpenCV` and `PyAutoGUI`.
    ```powershell
    cd ..\..\..
    ```
    *(You should be back in your `gesture-control-mouse` folder)*
    ```powershell
    pip install opencv-python pyautogui
    ```

You are now fully set up and all dependencies are installed correctly.

---

## How to Run

1.  Make sure your virtual environment is active:
    ```powershell
    .\API\models\research\venv\Scripts\activate
    ```

2.  Run the main script:
    ```powershell
    python main.py
    ```

3.  An OpenCV window will open, showing your webcam. The script will now track your hand and control your mouse.

4.  To stop the program, click on the OpenCV window and press the **'q'** key.
