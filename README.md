# Hands-On Lab: Agentic Memory Buffers in Google ADK

This repository contains `memorylab.ipynb`, an interactive Google Colab lab
covering the three memory buffers in the Google Agent Development Kit
(`google-adk`):

*   **Short-Term Memory (Working Buffer):** Turn-scoped `temp:*` state keys and
    context window controls (`ContextFilterPlugin` and
    `EventsCompactionConfig`).
*   **Session Memory (Episodic Buffer):** Conversation state (`SessionService`),
    event logs, and `user:*` state across restarts.
*   **Long-Term Memory (Memory Bank):** Cross-session fact extraction and recall
    with `VertexAiMemoryBankService`, `add_events_to_memory()`, and
    `preload_memory_tool`.

## Getting Started

### Step 1 - Create a Google Cloud Project

1.  Open the [Google Cloud Console](https://console.cloud.google.com/) and
    create a new Google Cloud (GCP) project (or select an existing project with
    billing enabled).
2.  Note your **Project ID**, which you will pass into **Step 2B** of the
    notebook.

### Step 2 - Enable the Required APIs

Open [Google Cloud Shell](https://shell.cloud.google.com/) for your project and
run the following command to enable both the **Vertex AI API** and the
**Generative Language (Gemini) API**:

```bash
gcloud services enable aiplatform.googleapis.com generativelanguage.googleapis.com --project="$(gcloud config get-value project)"
```

### Step 3 - Open `memorylab.ipynb` in Google Colab

Add `memorylab.ipynb` into [Google Colab](https://colab.research.google.com/)
using either method:

*   **From GitHub:** In Colab, select **File → Open notebook → GitHub**, paste
    the URL of this repository, and select `memorylab.ipynb`.
*   **Manual Upload:** Download `memorylab.ipynb` from this repository, then in
    Colab select **File → Upload notebook** and upload the file.

### Step 4 - Create and Store Your API Key

If you are using an API key (for **Vertex AI Express Mode** or **Gemini API /
Local Mode** in **Step 2A**), create your key and add it to Colab in one of two
ways:

1.  **Create an API key (optional if using GCP Project Sign-In in Step 2B):**

    *   For **Vertex AI Express Mode**, generate an Express Mode API key in the
        Vertex AI Studio settings, or create a key in your project with Cloud
        Shell:

        ```bash
        gcloud services api-keys create \
          --display-name="adk-memory-lab-key" \
          --api-target=service=aiplatform.googleapis.com \
          --api-target=service=generativelanguage.googleapis.com \
          --project="$(gcloud config get-value project)"
        ```

2.  **Provide the key to the notebook:**

    *   **Option A — Colab Secrets (Recommended):** Click the **Secrets** (key)
        icon in the left sidebar of Colab, add a new secret named
        `GOOGLE_API_KEY`, paste your key as the value, and toggle **Notebook
        access** on.
    *   **Option B — Directly in the Code Form:** Paste your key into the
        `API_KEY_OVERRIDE` field in **Step 2A** (or into the interactive prompt
        when **Step 2A** runs).

> [!NOTE]
> By default, **Step 2A** and **Step 2B** are pre-configured for **GCP
> Project Sign-In (`Vertex AI with GCP project (Colab sign-in)`)**, which
> authenticates with your Google account in Colab and only requires your
> `GCP_PROJECT_ID` in **Step 2B** to provision Vertex AI Agent Engine Sessions
> and Memory Bank.

## Running the Lab

1.  Run **Step 1** to install `google-adk` and `google-cloud-aiplatform`.
2.  Run **Step 2A** to configure the model and authentication mode.
3.  In **Step 2B**, enter your `GCP_PROJECT_ID` and run the cell to create (or
    connect to) your Vertex AI Agent Engine instance. Use the generated buttons
    to open the **Sessions** and **Memories** tabs in the Cloud Console.
4.  Run **Step 3A–3D** to register the ADK memory tools, the **Memory X-Ray**
    inspector, and the `Runner`.
5.  Work through **Modules 1–4** and run the **Cleanup** cell at the end of the
    notebook when finished.
