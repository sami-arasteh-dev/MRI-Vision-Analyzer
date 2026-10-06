# GapGPT MRI Vision Analyzer

A client-side web application for analyzing MRI images using Large Language Models (LLMs) with Vision capabilities via the GapGPT API.

This tool allows users to upload MRI scans and receive detailed, AI-generated descriptive analysis. It supports multiple vision models (GPT-4o, Gemini, DeepSeek) and is designed with a focus on privacy and user control.

> **⚠️ MEDICAL DISCLAIMER:** This software is for **educational and exploratory purposes only**. It does not provide medical diagnoses. AI-generated text should not be used for clinical decision-making. Always consult a qualified medical professional for actual medical advice.

## Features

*   **Multi-Model Support:** Switch between various Vision models (e.g., `gpt-4o`, `gemini-2.5-flash-image-preview`, `deepseek-v4-flash-vision-exp`).
*   **Client-Side Processing:** Images are processed in the browser and sent directly to the API. No intermediate server storage.
*   **Customizable Prompts:** Pre-configured with a safety-conscious prompt template that encourages descriptive analysis over definitive diagnosis.
*   **Real-Time Preview:** Instant visual feedback of uploaded images.
*   **Error Handling:** Robust error handling for API failures, invalid inputs, and network issues.
*   **Responsive Design:** Clean, modern UI built with vanilla CSS, compatible with desktop and mobile devices.

## Architecture

This is a **single-page application (SPA)** contained entirely within one `HTML` file.

*   **Frontend:** HTML5 structure, CSS3 for styling, and Vanilla JavaScript for logic.
*   **API Integration:** Communicates with the **GapGPT API** (`https://api.gapgpt.app/v1/responses`) using the `POST` method.
*   **Data Flow:**
    1.  User selects an image file.
    2.  JavaScript converts the file to a Base64 Data URL.
    3.  The image and text prompt are packaged into a JSON payload compatible with the OpenAI Responses API format.
    4.  The payload is sent to the GapGPT API with the user's Bearer token.
    5.  The response text is extracted and displayed.

## Prerequisites

*   A modern web browser (Chrome, Firefox, Edge, Safari).
*   A valid **GapGPT API Key**. You can obtain this from the GapGPT platform.

## Installation & Usage

Since this is a static HTML file, no installation or build process is required.

1.  **Download:** Save the `mri-decoder.html` file to your local machine.
2.  **Open:** Double-click the file to open it in your web browser.
3.  **Configure:**
    *   Enter your **API Key** in the designated field.
    *   Select the desired **Vision Model** from the dropdown menu.
4.  **Upload:** Click the upload box to select an MRI image (PNG, JPG, WEBP).
5.  **Analyze:** Click the **"🔍 تحلیل تصویر MRI"** button.
6.  **Review:** View the analysis results in the output section below the button.

## Configuration

### API Endpoint
The application is hardcoded to use the GapGPT API endpoint:
```javascript
const API_URL = "https://api.gapgpt.app/v1/responses";
```

### Supported Models
The following models are available in the dropdown menu. Ensure your API key has access to these models:
*   `gpt-4o`
*   `gemini-3-pro-image-preview`
*   `gemini-2.5-flash-image-preview`
*   `gemini-2.5-flash-image`
*   `deepseek-v4-flash-vision-exp`

### Default Prompt
The default prompt is designed to be cautious and descriptive. It asks the model to:
1.  Describe visible structures.
2.  Note any potential abnormalities (with caution).
3.  Differentiate between clear findings and uncertainties.
4.  Avoid definitive medical diagnoses.

You can modify the text in the `<textarea id="prompt">` element to suit specific research or educational needs.

## Technical Details

### Image Handling
Images are converted to Base64 Data URLs using the browser's `FileReader` API. This allows the image to be embedded directly in the JSON payload sent to the API.

### Response Parsing
The `extractResponseText` function handles various response formats from different AI providers. It looks for:
*   `output_text` field (common in some OpenAI-compatible APIs).
*   `output` array containing `message` objects with `output_text` content.
*   Fallback mechanisms for unexpected response structures.

### Security
*   **API Key:** The API key is stored only in the browser's memory during the session. It is not persisted in local storage or sent to any third-party service other than the specified API endpoint.
*   **CORS:** Ensure your browser allows CORS requests to `api.gapgpt.app`. Most modern browsers handle this automatically for user-initiated requests.

## Development

To modify the application:

1.  Open `mri-decoder.html` in any text editor.
2.  Edit the CSS within the `<style>` tag to change the UI.
3.  Edit the JavaScript within the `<script>` tag to change the logic.
4.  Save the file and refresh the browser.

## License

This project is provided as-is for educational and experimental purposes. Please ensure you comply with the terms of service of the GapGPT API and the respective AI model providers.

## Disclaimer

**This tool is not a medical device.** The AI-generated analysis is for informational purposes only. Do not rely on this tool for medical diagnosis or treatment. Always consult a healthcare professional for medical advice.
