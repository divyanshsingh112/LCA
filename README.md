# 🌍 Metallurgy Life Cycle Assessment (LCA) Analytics Engine

An end-to-end framework for predicting environmental impacts (CO₂ emissions) and Material Circularity Indicators (MCI) for metals. This tool uses a machine learning model integrated with a Fast API backend and a professional terminal user interface to help engineers and researchers transition from linear to circular economies.

## ✨ Features

- **Predictive AI Modeling**: Utilizes an optimized Random Forest Regressor to predict highly non-linear relationships in metallurgy datasets.
- **RESTful API Backend**: High-performance FastAPI server (`app.py`) built with strictly validated Pydantic models.
- **Interactive Terminal UI**: A beautiful, menu-driven CLI experience (`main.py`) powered by `Rich` that automatically orchestrates the server and inputs.
- **Circularity Focus**: Outputs critical metrics like MCI Score and kg CO₂ equivalent per kg of material produced.

## 🚀 QuickStart

1. **Install Dependencies**
   It's highly recommended to use a virtual environment.
   ```bash
   pip install -r requirements.txt
   ```

2. **Train the Model (If not already trained)**
   *The repository might not include the 100MB+ model file.*
   ```bash
   python -m src.train_model
   ```

3. **Run the Application**
   Everything you need is wrapped inside the unified launcher. It will automatically start the lightweight API server in the background and walk you through a user-friendly data entry process.
   ```bash
   python main.py
   ```

## 🧠 Project Architecture

* `main.py`: The unified entry point. Contains the interactive UI and manages background threads for the FastAPI server.
* `app.py`: The FastAPI application defining the routes (`/api/v1/predict`) and input data validation schemas.
* `src/train_model.py`: The machine learning training pipeline. Reads from data, preprocesses features, trains the Random Forest, and serializes it to `models/`.
* `src/core/inference.py`: The wrapper module used by the API to load the `.pkl` model and handle prediction requests safely.
* `src/config.py`: Centralized configuration for directory paths to ensure the project works anywhere.

## 📝 Input Parameters

The tool takes 19 parameters categorised into:
1. **Material Identity**: Material type (Aluminum, Steel, etc.) & Route (Primary/Secondary).
2. **Energy Profile**: Energy used during Mining, Smelting, Refining, etc.
3. **Circularity Metrics**: Recycled Content, Recycling Efficiency, Product Lifetime.
4. **End-of-Life & Transport**: EOL Route, Transport Distance, and Transport Mode.
5. **Grid & Criticality**: Grid Renewable Share and Material Criticality.

## 🧪 Step-by-Step Dummy Inputs

To quickly test the application, enter the following values exactly as they are prompted in the CLI. The fields are grouped exactly how the application asks for them.

<details>
<summary><b>🟢 1. Aluminum (Secondary) — Highly Circular, Low Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **1**
  * `Production Route`: **2**
* **② Energy Profile**
  * `Mining Energy`: **2.1**
  * `Smelting Energy`: **4.5**
  * `Refining Energy`: **3.0**
  * `Fabrication Energy`: **2.5**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.85**
  * `Recycling Efficiency`: **0.90**
  * `Recycled Output`: **0.765**
  * `Loop Closing Potential`: **0.15**
  * `Reuse Potential`: **0.8**
  * `Repairability`: **0.7**
  * `Product Lifetime`: **15.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **1** *(Recycled)*
  * `Transport Distance`: **150.0**
  * `Transport Mode`: **2** *(Rail)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **60.0**
  * `Renewable Electricity`: **0.6**
  * `Material Criticality`: **0.2**
</details>

<details>
<summary><b>🔴 2. Copper (Primary) — Linear, High Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **2**
  * `Production Route`: **1**
* **② Energy Profile**
  * `Mining Energy`: **8.5**
  * `Smelting Energy`: **15.0**
  * `Refining Energy`: **8.0**
  * `Fabrication Energy`: **4.0**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.10**
  * `Recycling Efficiency`: **0.30**
  * `Recycled Output`: **0.03**
  * `Loop Closing Potential`: **0.05**
  * `Reuse Potential`: **0.4**
  * `Repairability`: **0.3**
  * `Product Lifetime`: **5.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **2** *(Landfill)*
  * `Transport Distance`: **2000.0**
  * `Transport Mode`: **1** *(Truck)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **20.0**
  * `Renewable Electricity`: **0.2**
  * `Material Criticality`: **0.6**
</details>

<details>
<summary><b>🟢 3. Steel (Secondary) — Highly Circular, Low Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **3**
  * `Production Route`: **2**
* **② Energy Profile**
  * `Mining Energy`: **3.0**
  * `Smelting Energy`: **7.0**
  * `Refining Energy`: **4.0**
  * `Fabrication Energy`: **3.0**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.70**
  * `Recycling Efficiency`: **0.85**
  * `Recycled Output`: **0.59**
  * `Loop Closing Potential`: **0.12**
  * `Reuse Potential`: **0.7**
  * `Repairability`: **0.8**
  * `Product Lifetime`: **30.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **1** *(Recycled)*
  * `Transport Distance`: **300.0**
  * `Transport Mode`: **3** *(Ship)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **50.0**
  * `Renewable Electricity`: **0.5**
  * `Material Criticality`: **0.3**
</details>

<details>
<summary><b>🟡 4. Zinc (Primary) — Linear, Moderate Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **4**
  * `Production Route`: **1**
* **② Energy Profile**
  * `Mining Energy`: **6.0**
  * `Smelting Energy`: **12.0**
  * `Refining Energy`: **6.0**
  * `Fabrication Energy`: **3.5**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.15**
  * `Recycling Efficiency`: **0.25**
  * `Recycled Output`: **0.04**
  * `Loop Closing Potential`: **0.03**
  * `Reuse Potential`: **0.3**
  * `Repairability`: **0.4**
  * `Product Lifetime`: **10.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **2** *(Landfill)*
  * `Transport Distance`: **800.0**
  * `Transport Mode`: **1** *(Truck)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **30.0**
  * `Renewable Electricity`: **0.3**
  * `Material Criticality`: **0.4**
</details>

<details>
<summary><b>🔴 5. Nickel (Primary) — Linear, High Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **5**
  * `Production Route`: **1**
* **② Energy Profile**
  * `Mining Energy`: **15.0**
  * `Smelting Energy`: **25.0**
  * `Refining Energy`: **12.0**
  * `Fabrication Energy`: **5.0**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.05**
  * `Recycling Efficiency`: **0.20**
  * `Recycled Output`: **0.01**
  * `Loop Closing Potential`: **0.08**
  * `Reuse Potential`: **0.5**
  * `Repairability`: **0.5**
  * `Product Lifetime`: **8.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **2** *(Landfill)*
  * `Transport Distance`: **5000.0**
  * `Transport Mode`: **6** *(Air)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **25.0**
  * `Renewable Electricity`: **0.25**
  * `Material Criticality`: **0.8**
</details>

<details>
<summary><b>🔴 6. Titanium (Primary) — Linear, Extreme Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **6**
  * `Production Route`: **1**
* **② Energy Profile**
  * `Mining Energy`: **45.0**
  * `Smelting Energy`: **70.0**
  * `Refining Energy`: **35.0**
  * `Fabrication Energy`: **15.0**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.02**
  * `Recycling Efficiency`: **0.10**
  * `Recycled Output`: **0.002**
  * `Loop Closing Potential`: **0.10**
  * `Reuse Potential`: **0.6**
  * `Repairability`: **0.6**
  * `Product Lifetime`: **20.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **2** *(Landfill)*
  * `Transport Distance`: **8000.0**
  * `Transport Mode`: **6** *(Air)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **15.0**
  * `Renewable Electricity`: **0.15**
  * `Material Criticality`: **0.9**
</details>

<details>
<summary><b>🟢 7. Lead (Secondary) — Highly Circular, Low Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **7**
  * `Production Route`: **2**
* **② Energy Profile**
  * `Mining Energy`: **1.5**
  * `Smelting Energy`: **3.5**
  * `Refining Energy`: **2.0**
  * `Fabrication Energy`: **1.5**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.95**
  * `Recycling Efficiency`: **0.95**
  * `Recycled Output`: **0.90**
  * `Loop Closing Potential`: **0.05**
  * `Reuse Potential`: **0.9**
  * `Repairability`: **0.9**
  * `Product Lifetime`: **3.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **1** *(Recycled)*
  * `Transport Distance`: **100.0**
  * `Transport Mode`: **2** *(Rail)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **45.0**
  * `Renewable Electricity`: **0.45**
  * `Material Criticality`: **0.5**
</details>

<details>
<summary><b>🟡 8. Tin (Primary) — Linear, Moderate Emissions</b></summary>

* **① Material Identity**
  * `Material Type`: **8**
  * `Production Route`: **1**
* **② Energy Profile**
  * `Mining Energy`: **10.0**
  * `Smelting Energy`: **18.0**
  * `Refining Energy`: **9.0**
  * `Fabrication Energy`: **4.0**
* **③ Circularity Metrics**
  * `Recycled Content`: **0.10**
  * `Recycling Efficiency`: **0.20**
  * `Recycled Output`: **0.02**
  * `Loop Closing Potential`: **0.04**
  * `Reuse Potential`: **0.4**
  * `Repairability`: **0.5**
  * `Product Lifetime`: **4.0**
* **④ End-of-Life & Transport**
  * `End-of-Life Route`: **2** *(Landfill)*
  * `Transport Distance`: **1500.0**
  * `Transport Mode`: **3** *(Ship)*
* **⑤ Grid & Material Criticality**
  * `Grid Renewable Share`: **30.0**
  * `Renewable Electricity`: **0.30**
  * `Material Criticality`: **0.7**
</details>

## 🛡️ Best Practices Applied

- Strict separation of concerns (Training vs. Inference vs. UI).
- Robust error handling for Server Timeouts and Validation Failures.
- Zero Data Leakage (Target-derived columns were strictly eliminated from the training feature set).
- Complete Path Safety via `pathlib` and centralized configs.
