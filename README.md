# 🏆 Hackathon Judge's Guide (Technical Overview)

This document provides deep-dive technical details for judges regarding the AI, Mapping, and Scientific models used in KisanDost.

---

## 🤖 AI & Machine Learning (TensorFlow.js)

The application uses **TensorFlow.js** to run sophisticated agricultural models directly in the browser and Node.js environment.

### 1. Yield AI Predictor (Neural Network)
- **Architecture**: A Sequential Neural Network with an input layer (3 features), a hidden dense layer (10 units with ReLU activation), and a single output unit for regression.
- **Inputs**: 
    - **NDVI** (Normalized Difference Vegetation Index - measuring plant health).
    - **Soil Moisture** (Relative humidity mapped to saturation levels).
    - **Rainfall** (Local precipitation data in mm).
- **Training**: The model was trained on synthetic datasets generated to reflect non-linear agricultural patterns (e.g., the diminishing returns of rainfall on yield).
- **Why TF.js?**: By using TensorFlow.js, we eliminate the need for a separate Python/Flask backend. This results in **zero-latency predictions**, lower hosting costs, and potential for offline field usage.

---

## 🛰️ Satellite Map & Auto-Pilot

### Mapping Stack
- **Library**: `react-leaflet` / `leaflet`.
- **Imagery**: **Google Maps Hybrid Tiles**. We chose this to allow high-resolution field scanning without the API key/quota hurdles of Google Maps Platform for hackathon prototypes.

### The "Auto-Pilot" Pipeline
1.  **Map Tap**: User selects their farm on the satellite map.
2.  **Weather Fetch**: The app hits our weather proxy with the tap's `lat/lon`.
3.  **Data Injection**: Live Humidity and Precipitation are extracted.
4.  **AI Run**: These values are normalized and "fed" into the TensorFlow.js model immediately.

---

## 🌡️ Scientific Methodology

### 1. Remote Sensing (NDVI Analysis)
We simulate NDVI tracking by analyzing chlorophyll reflectance patterns.
$$NDVI = \frac{NIR - Red}{NIR + Red}$$
The app interprets this for the farmer:
- **0.7+**: Healthy/Vigorous growth.
- **0.4 - 0.7**: Moderate stress/Growth issues.
- **Below 0.4**: Critical stress or bare soil.

### 2. Fertilizer Optimization
The calculator uses a logic-based subtraction model adjusted for soil leaching coefficients ($S$):
$$Y = (R_{crop} \times S_{coeff}) - N_{curr}$$
This prevents NPK wastage, which is both an environmental and economic win for the farmer.

---

## ❓ Judge's Q&A

**Q: How is this better than a simple Excel formula?**
*   **A:** Formulas are linear. Agriculture is not. Our Neural Network can learn that 200mm of rain is good, but 1000mm is a flood that kills yield. A formula often fails at these extremes.

**Q: How do you handle low-connectivity areas?**
*   **A:** Because we use TensorFlow.js on the client, once the page loads, the AI logic doesn't need the cloud. Only the initial map/weather fetch requires data, making it resilient for remote rural usage.

**Q: Is the data localized?**
*   **A:** Yes. Using `next-intl`, we provide full Hindi and Gujarati support (not just Google Translate, but hand-written agricultural terminology).

---

*Prepared for Hackathon Judges & Tech Reviewers.*
