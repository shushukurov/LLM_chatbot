
# GPT-4-Driven Chatbot for Handling Large/Many PDFs

This solution leverages the GPT-4 API to develop a ChatGPT chatbot that can interact with several extensive PDF files.

The technology stack encompasses LangChain, Pinecone, Typescript, OpenAI, and Next.js. LangChain offers a simplified pathway for crafting scalable AI/LLM-based applications and chatbots, while Pinecone acts as a vector store, preserving embeddings and converting PDF content to enable the retrieval of similar documents later on.

A visual walkthrough and tutorial for this repository can be found within the `visual guide` directory.

**Facing issues? Refer to the troubleshooting part at the bottom of this document.**

Introductory Note: Ensure Node is pre-installed on your system, and its version is 18 or above.

## Setting Up Development

1. **Installing Necessary Packages**

   First, execute `npm install yarn -g` to globally install yarn (if not done previously).

   Follow it with:

   ```
   yarn install
   ```
   Completion will manifest as a new `node_modules` directory.

2. **Configure your `.env` file**

   - Duplicate `.env.example` to `.env`
   - For API keys, refer to [OpenAI's documentation](https://help.openai.com/en/articles/4936850-where-do-i-find-my-secret-api-key) and [Pinecone's website](https://pinecone.io/). Populate the `.env` file accordingly.

3. Within the `config` directory, modify the `PINECONE_NAME_SPACE` to your preferred `namespace`. This will be used for embedding storage in Pinecone and subsequent queries.

4. Under `utils/makechain.ts`, adjust the `QA_PROMPT` based on your requirements. If `gpt-4` API access is granted, switch `modelName` in `new OpenAI` to `gpt-4`. Do confirm the availability of the `gpt-4` API outside this repository; absence can halt the application's functionality.

## Converting PDFs into Embeddings

**This repository supports multiple PDF file uploads.**

1. Place your PDF files or directories containing them in the `docs` folder.
2. Initiate the script using `npm run ingest` to embed the content. Troubleshoot if required.
3. Validate the successful addition of namespaces and vectors on Pinecone's dashboard.

## Launching the Application

After ensuring the embeddings and data are accurately integrated with Pinecone, execute `npm run dev` to boot up the local development platform. Post that, you can engage with the chat interface.

**General Troubleshooting:**

- Ensure you're on the latest Node version (`node -v`).
- Consider converting problematic PDFs to text or choose another PDF. Some PDFs might be damaged, scanned, or need OCR for text conversion.
- Verify the exposure of `env` variables using `Console.log`.
- Ensure LangChain and Pinecone versions align with this repository's.
- Confirm the creation of a proper `.env` file with functional API keys.
- If the `modelName` in `OpenAI` is altered, ensure API access for the designated model.
- Verify OpenAI account credit and ensure billing details are correct.
- Avoid multiple OPENAPI keys in your global environment; it can override the project's local `env`.
- If issues persist, embed API keys directly into the `process.env` variables.

**Pinecone-specific Troubleshooting:**

- Confirm the `environment` and `index` on your Pinecone dashboard match those in `pinecone.ts` and `.env`.
- Set vector dimensions to `1536`.
- Ensure Pinecone namespaces are lowercase.
- Remember, Pinecone indices for Starter users get purged after a week of inactivity. To avoid this, ping Pinecone with an API request to reset the timer within that window.
- If all else fails, start afresh with a new Pinecone project and repository clone.
