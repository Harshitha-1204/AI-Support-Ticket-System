{
  "name": "Knowledge Base Ingestion",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        -240,
        -16
      ],
      "id": "ab15f469-aba4-4536-978f-3a19da043f1c",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "fileSelector": "C:\\Users\\sindh\\.n8n-files\\knowledgebase\\*.md",
        "options": {}
      },
      "type": "n8n-nodes-base.readWriteFile",
      "typeVersion": 1.1,
      "position": [
        -32,
        -16
      ],
      "id": "a7e6d8c1-48c8-475b-87f6-e324356827aa",
      "name": "Read/Write Files from Disk"
    },
    {
      "parameters": {
        "operation": "text",
        "options": {}
      },
      "type": "n8n-nodes-base.extractFromFile",
      "typeVersion": 1.1,
      "position": [
        176,
        -16
      ],
      "id": "ed4b3f78-d9d7-45d6-9569-e734b7fbea85",
      "name": "Extract from File"
    },
    {
      "parameters": {
        "mode": "insert",
        "qdrantCollection": {
          "__rl": true,
          "value": "noavia_knowledge_base",
          "mode": "id"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.vectorStoreQdrant",
      "typeVersion": 1.3,
      "position": [
        384,
        -16
      ],
      "id": "675abca8-4aa9-40d0-8659-f08700f4ef43",
      "name": "Qdrant Vector Store",
      "credentials": {
        "qdrantApi": {
          "id": "EjxOrGlfRlBGqIXa",
          "name": "Qdrant account"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.documentDefaultDataLoader",
      "typeVersion": 1.1,
      "position": [
        512,
        240
      ],
      "id": "c76c0bd0-f120-46f7-b806-cf05fcd996c1",
      "name": "Default Data Loader"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.embeddingsOpenAi",
      "typeVersion": 1.2,
      "position": [
        352,
        256
      ],
      "id": "ee0ac355-bcd5-45af-b04f-ef2fd8857db7",
      "name": "Embeddings OpenAI",
      "credentials": {
        "openAiApi": {
          "id": "liF4u28KTM9BKVWY",
          "name": "OpenAI account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Read/Write Files from Disk",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Read/Write Files from Disk": {
      "main": [
        [
          {
            "node": "Extract from File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract from File": {
      "main": [
        [
          {
            "node": "Qdrant Vector Store",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Default Data Loader": {
      "ai_document": [
        [
          {
            "node": "Qdrant Vector Store",
            "type": "ai_document",
            "index": 0
          }
        ]
      ]
    },
    "Embeddings OpenAI": {
      "ai_embedding": [
        [
          {
            "node": "Qdrant Vector Store",
            "type": "ai_embedding",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1",
    "binaryMode": "separate"
  },
  "versionId": "0a7dae04-00cf-4f88-a22c-f87fb9df44f4",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "3ce675209222b9894b6cdc9463c45b665e04e03cef1a885907416f3e0fd6bf56"
  },
  "id": "tslhk6HR95csBiJY",
  "tags": []
}