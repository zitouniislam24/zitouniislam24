
    "name": "Livre blanc (avec illustration)",
    "flow": [
        {
            "id": 28,
            "module": "builtin:BasicRepeater",
            "version": 1,
            "parameters": {},
            "mapper": {
                "step": "1",
                "start": "1",
                "repeats": "1"
            },
            "metadata": {
                "designer": {
                    "x": -593,
                    "y": 144
                },
                "restore": {},
                "expect": [
                    {
                        "name": "start",
                        "type": "number",
                        "label": "Initial value",
                        "required": true
                    },
                    {
                        "name": "repeats",
                        "type": "number",
                        "label": "Repeats",
                        "required": true,
                        "validate": {
                            "max": 10000,
                            "min": 0
                        }
                    },
                    {
                        "name": "step",
                        "type": "number",
                        "label": "Step",
                        "required": true
                    }
                ]
            }
        },
        {
            "id": 12,
            "module": "google-docs:getADocument",
            "version": 1,
            "parameters": {
                "__IMTCONN__": 1998737
            },
            "mapper": {
                "filter": "image",
                "select": "dropdown",
                "document": "/1z4f7KFGYd5sIgfMGhmxX7nOAnBVBbH0f7_O9w6Tm_MA",
                "destination": "drive",
                "includeTabsContent": false
            },
            "metadata": {
                "designer": {
                    "x": -255,
                    "y": 150
                },
                "restore": {
                    "expect": {
                        "filter": {
                            "label": "Image"
                        },
                        "select": {
                            "label": "By Dropdown"
                        },
                        "document": {
                            "path": [
                                "Livre blanc"
                            ]
                        },
                        "destination": {
                            "label": "My Drive"
                        }
                    },
                    "parameters": {
                        "__IMTCONN__": {
                            "data": {
                                "scoped": "true",
                                "connection": "google"
                            },
                            "label": "@Thibault (hello@ottho.fr)"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "__IMTCONN__",
                        "type": "account:google",
                        "label": "Connection",
                        "required": true
                    }
                ],
                "expect": [
                    {
                        "name": "select",
                        "type": "select",
                        "label": "Get Content of a Document",
                        "required": true,
                        "validate": {
                            "enum": [
                                "map",
                                "dropdown"
                            ]
                        }
                    },
                    {
                        "name": "includeTabsContent",
                        "type": "boolean",
                        "label": "Include Tabs Content",
                        "required": true
                    },
                    {
                        "name": "filter",
                        "type": "select",
                        "label": "Filter",
                        "required": true,
                        "validate": {
                            "enum": [
                                "image",
                                "drawing",
                                "chart"
                            ]
                        }
                    },
                    {
                        "name": "destination",
                        "type": "select",
                        "label": "Choose a Drive",
                        "required": true,
                        "validate": {
                            "enum": [
                                "drive",
                                "share",
                                "team"
                            ]
                        }
                    },
                    {
                        "name": "document",
                        "type": "file",
                        "label": "Document ID",
                        "required": true
                    }
                ]
            }
        },
        {
            "id": 10,
            "module": "openai-gpt-3:CreateCompletion",
            "version": 1,
            "parameters": {
                "__IMTCONN__": 1427740
            },
            "mapper": {
                "model": "chatgpt-4o-latest",
                "top_p": "1",
                "select": "chat",
                "messages": [
                    {
                        "role": "system",
                        "content": "You are an assistant helping me write a white paper aimed at {target}. As an assistant, you write the paragraphs based on my instructions.\n\n{target} = young mothers"
                    },
                    {
                        "role": "user",
                        "content": "I will provide you with a text: {{12.text}}\n\nFollow these steps:\t\n1.\tAnalyze the table of contents and the existing paragraphs.\t\n2.\tDeduce the next paragraph to write based on the last paragraph already written.\t\n3.\tIf there are no paragraphs, start with the first title in the table of contents.Write only the next paragraph in the order of the table of contents.\n\nEach paragraph should be 1000 characters.\nIMPORTANT: Do not add any words or characters to introduce or conclude the paragraph other than those related to the text. Leave a blank line between each paragraph and title. Do not use any markdown-style formatting.\n\nAlways write in french.",
                        "imageDetail": "auto"
                    }
                ],
                "max_tokens": "2048",
                "temperature": "1",
                "n_completions": "1",
                "response_format": "text"
            },
            "metadata": {
                "designer": {
                    "x": 300,
                    "y": 150
                },
                "restore": {
                    "expect": {
                        "stop": {
                            "mode": "chose"
                        },
                        "model": {
                            "mode": "chose",
                            "label": "chatgpt-4o-latest (system)"
                        },
                        "select": {
                            "label": "Create a Chat Completion (GPT and o1 models)"
                        },
                        "messages": {
                            "mode": "chose",
                            "items": [
                                {
                                    "role": {
                                        "mode": "chose",
                                        "label": "System"
                                    }
                                },
                                {
                                    "role": {
                                        "mode": "chose",
                                        "label": "User"
                                    },
                                    "imageDetail": {
                                        "mode": "chose",
                                        "label": "Auto"
                                    },
                                    "imageInputType": {
                                        "mode": "chose",
                                        "label": "Empty"
                                    }
                                }
                            ]
                        },
                        "logit_bias": {
                            "mode": "chose"
                        },
                        "response_format": {
                            "mode": "chose",
                            "label": "Text"
                        },
                        "additionalParameters": {
                            "mode": "chose"
                        }
                    },
                    "parameters": {
                        "__IMTCONN__": {
                            "data": {
                                "scoped": "true",
                                "connection": "openai-gpt-3"
                            },
                            "label": "@Thibault"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "__IMTCONN__",
                        "type": "account:openai-gpt-3",
                        "label": "Connection",
                        "required": true
                    }
                ],
                "expect": [
                    {
                        "name": "select",
                        "type": "select",
                        "label": "Select Method",
                        "required": true,
                        "validate": {
                            "enum": [
                                "chat",
                                "prompt"
                            ]
                        }
                    },
                    {
                        "name": "temperature",
                        "type": "number",
                        "label": "Temperature",
                        "validate": {
                            "max": 2,
                            "min": 0
                        }
                    },
                    {
                        "name": "top_p",
                        "type": "number",
                        "label": "Top P",
                        "validate": {
                            "max": 1,
                            "min": 0
                        }
                    },
                    {
                        "name": "n_completions",
                        "type": "number",
                        "label": "Number"
                    },
                    {
                        "name": "frequency_penalty",
                        "type": "number",
                        "label": "Frequency Penalty",
                        "validate": {
                            "max": 2,
                            "min": -2
                        }
                    },
                    {
                        "name": "presence_penalty",
                        "type": "number",
                        "label": "Presence Penalty",
                        "validate": {
                            "max": 2,
                            "min": -2
                        }
                    },
                    {
                        "name": "logit_bias",
                        "spec": {
                            "name": "value",
                            "spec": [
                                {
                                    "name": "token",
                                    "type": "text",
                                    "label": "Token ID",
                                    "required": true
                                },
                                {
                                    "name": "probability",
                                    "type": "number",
                                    "label": "Probability",
                                    "required": true,
                                    "validate": {
                                        "max": 100,
                                        "min": -100
                                    }
                                }
                            ],
                            "type": "collection",
                            "label": "Token Probability"
                        },
                        "type": "array",
                        "label": "Token Probability"
                    },
                    {
                        "name": "seed",
                        "type": "integer",
                        "label": "Seed"
                    },
                    {
                        "name": "stop",
                        "spec": {
                            "name": "value",
                            "type": "text",
                            "label": "Stop Sequence"
                        },
                        "type": "array",
                        "label": "Stop Sequences",
                        "validate": {
                            "maxItems": 4
                        }
                    },
                    {
                        "name": "additionalParameters",
                        "spec": {
                            "name": "value",
                            "spec": [
                                {
                                    "name": "key",
                                    "type": "text",
                                    "label": "Parameter Name",
                                    "required": true
                                },
                                {
                                    "name": "type",
                                    "type": "select",
                                    "label": "Input Type",
                                    "options": [
                                        {
                                            "label": "Text",
                                            "value": "text",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "text",
                                                    "label": "Parameter Value"
                                                }
                                            ],
                                            "default": true
                                        },
                                        {
                                            "label": "Number",
                                            "value": "number",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "number",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        },
                                        {
                                            "label": "Boolean",
                                            "value": "boolean",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "boolean",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        },
                                        {
                                            "label": "Date",
                                            "value": "date",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "date",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        },
                                        {
                                            "label": "Any",
                                            "value": "any",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "any",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "type": "collection",
                            "label": "Input Parameter"
                        },
                        "type": "array",
                        "label": "Other Input Parameters"
                    },
                    {
                        "name": "model",
                        "type": "select",
                        "label": "Model",
                        "required": true
                    },
                    {
                        "name": "max_tokens",
                        "type": "uinteger",
                        "label": "Max Completion Tokens"
                    },
                    {
                        "name": "messages",
                        "spec": {
                            "name": "value",
                            "spec": [
                                {
                                    "name": "role",
                                    "type": "select",
                                    "label": "Role",
                                    "options": {
                                        "store": [
                                            {
                                                "label": "System",
                                                "value": "system",
                                                "nested": [
                                                    {
                                                        "help": "Text content of the message on behalf of the selected __Role__.",
                                                        "name": "content",
                                                        "type": "text",
                                                        "label": "Text Content"
                                                    }
                                                ]
                                            },
                                            {
                                                "label": "User",
                                                "value": "user",
                                                "nested": [
                                                    {
                                                        "help": "Text content of the message on behalf of the selected __Role__.",
                                                        "name": "content",
                                                        "type": "text",
                                                        "label": "Text Content"
                                                    },
                                                    {
                                                        "name": "imageInputType",
                                                        "type": "select",
                                                        "label": "Image Input Type",
                                                        "options": [
                                                            {
                                                                "label": "URL",
                                                                "value": "url",
                                                                "nested": [
                                                                    {
                                                                        "help": "Make sure to use a publically accessible URL.\nYou can test if your image is publically accessible by opening the link in an incognito tab.",
                                                                        "name": "imageUrl",
                                                                        "type": "url",
                                                                        "label": "Image URL"
                                                                    }
                                                                ]
                                                            },
                                                            {
                                                                "label": "Image File",
                                                                "value": "file",
                                                                "nested": [
                                                                    {
                                                                        "name": "imageFile",
                                                                        "spec": [
                                                                            {
                                                                                "help": "Accepted extensions: `.jpg`, `.jpeg`, `.png`, `.webp` and `.gif`.",
                                                                                "name": "imageFilename",
                                                                                "type": "filename",
                                                                                "label": "Image Filename",
                                                                                "semantic": "file:name",
                                                                                "extension": [
                                                                                    "jpg",
                                                                                    "jpeg",
                                                                                    "png",
                                                                                    "webp",
                                                                                    "gif"
                                                                                ]
                                                                            },
                                                                            {
                                                                                "name": "imageData",
                                                                                "type": "buffer",
                                                                                "label": "Image Data",
                                                                                "semantic": "file:data"
                                                                            }
                                                                        ],
                                                                        "type": "collection",
                                                                        "label": "Image"
                                                                    }
                                                                ]
                                                            }
                                                        ],
                                                        "mappable": false
                                                    },
                                                    {
                                                        "name": "imageDetail",
                                                        "type": "select",
                                                        "label": "Image Detail",
                                                        "options": [
                                                            {
                                                                "label": "Auto",
                                                                "value": "auto",
                                                                "default": true
                                                            },
                                                            {
                                                                "label": "High",
                                                                "value": "high"
                                                            },
                                                            {
                                                                "label": "Low",
                                                                "value": "low"
                                                            }
                                                        ],
                                                        "advanced": true
                                                    }
                                                ]
                                            },
                                            {
                                                "label": "Assistant",
                                                "value": "assistant",
                                                "nested": [
                                                    {
                                                        "help": "Text content of the message on behalf of the selected __Role__.",
                                                        "name": "content",
                                                        "type": "text",
                                                        "label": "Text Content"
                                                    }
                                                ]
                                            }
                                        ]
                                    },
                                    "required": true
                                }
                            ],
                            "type": "collection",
                            "label": "Message"
                        },
                        "type": "array",
                        "label": "Messages",
                        "required": true
                    },
                    {
                        "name": "response_format",
                        "type": "select",
                        "label": "Response Format",
                        "validate": {
                            "enum": [
                                "text",
                                "json_object"
                            ]
                        }
                    }
                ],
                "interface": [
                    {
                        "name": "result",
                        "type": "any",
                        "label": "Result"
                    },
                    {
                        "name": "id",
                        "type": "text",
                        "label": "ID"
                    },
                    {
                        "name": "object",
                        "type": "text",
                        "label": "Object"
                    },
                    {
                        "name": "created",
                        "type": "date",
                        "label": "Created"
                    },
                    {
                        "name": "model",
                        "type": "text",
                        "label": "Model"
                    },
                    {
                        "name": "choices",
                        "spec": {
                            "spec": [
                                {
                                    "name": "text",
                                    "type": "text",
                                    "label": "Text"
                                },
                                {
                                    "name": "index",
                                    "type": "number",
                                    "label": "Index"
                                },
                                {
                                    "name": "logprobs",
                                    "type": "text",
                                    "label": "Log Probs"
                                },
                                {
                                    "name": "finish_reason",
                                    "type": "text",
                                    "label": "Finish Reason"
                                },
                                {
                                    "name": "message",
                                    "spec": [
                                        {
                                            "name": "role",
                                            "type": "text",
                                            "label": "Role"
                                        },
                                        {
                                            "name": "content",
                                            "type": "text",
                                            "label": "Content"
                                        },
                                        {
                                            "name": "refusal",
                                            "type": "text",
                                            "label": "Refusal"
                                        }
                                    ],
                                    "type": "collection",
                                    "label": "Message"
                                }
                            ],
                            "type": "collection"
                        },
                        "type": "array",
                        "label": "Choices"
                    },
                    {
                        "name": "usage",
                        "spec": [
                            {
                                "name": "prompt_tokens",
                                "type": "number",
                                "label": "Prompt Tokens"
                            },
                            {
                                "name": "completion_tokens",
                                "type": "text",
                                "label": "Completion Tokens"
                            },
                            {
                                "name": "total_tokens",
                                "type": "number",
                                "label": "Total Tokens"
                            },
                            {
                                "name": "prompt_tokens_details",
                                "spec": [
                                    {
                                        "name": "cached_tokens",
                                        "type": "uinteger",
                                        "label": "Cached Tokens"
                                    },
                                    {
                                        "name": "text_tokens",
                                        "type": "uinteger",
                                        "label": "Text Tokens"
                                    },
                                    {
                                        "name": "image_tokens",
                                        "type": "uinteger",
                                        "label": "Image Tokens"
                                    },
                                    {
                                        "name": "audio_tokens",
                                        "type": "uinteger",
                                        "label": "Audio Tokens"
                                    }
                                ],
                                "type": "collection",
                                "label": "Prompt Tokens Details"
                            },
                            {
                                "name": "completion_tokens_details",
                                "spec": [
                                    {
                                        "name": "reasoning_tokens",
                                        "type": "uinteger",
                                        "label": "Reasoning Tokens"
                                    },
                                    {
                                        "name": "text_tokens",
                                        "type": "uinteger",
                                        "label": "Text Tokens"
                                    },
                                    {
                                        "name": "audio_tokens",
                                        "type": "uinteger",
                                        "label": "Audio Tokens"
                                    }
                                ],
                                "type": "collection",
                                "label": "Completion Tokens Details"
                            }
                        ],
                        "type": "collection",
                        "label": "Usage"
                    },
                    {
                        "name": "system_fingerprint",
                        "type": "text",
                        "label": "System Fingerprint"
                    }
                ],
                "advanced": true
            }
        },
        {
            "id": 16,
            "module": "openai-gpt-3:CreateCompletion",
            "version": 1,
            "parameters": {
                "__IMTCONN__": 1427740
            },
            "mapper": {
                "model": "chatgpt-4o-latest",
                "top_p": "1",
                "select": "chat",
                "messages": [
                    {
                        "role": "user",
                        "content": "Create an image illustrating the paragraph: {{10.result}} in a {style}\n\n{style} = Photorealistic\n\nIMPORTANT: Provide only the prompt, nothing else. No introduction, special characters, or conclusion.",
                        "imageDetail": "auto"
                    }
                ],
                "max_tokens": "2048",
                "temperature": "1",
                "n_completions": "1",
                "response_format": "text"
            },
            "metadata": {
                "designer": {
                    "x": 600,
                    "y": 150
                },
                "restore": {
                    "expect": {
                        "stop": {
                            "mode": "chose"
                        },
                        "model": {
                            "mode": "chose",
                            "label": "chatgpt-4o-latest (system)"
                        },
                        "select": {
                            "label": "Create a Chat Completion (GPT and o1 models)"
                        },
                        "messages": {
                            "mode": "chose",
                            "items": [
                                {
                                    "role": {
                                        "mode": "chose",
                                        "label": "User"
                                    },
                                    "imageDetail": {
                                        "mode": "chose",
                                        "label": "Auto"
                                    },
                                    "imageInputType": {
                                        "mode": "chose",
                                        "label": "Empty"
                                    }
                                }
                            ]
                        },
                        "logit_bias": {
                            "mode": "chose"
                        },
                        "response_format": {
                            "mode": "chose",
                            "label": "Text"
                        },
                        "additionalParameters": {
                            "mode": "chose"
                        }
                    },
                    "parameters": {
                        "__IMTCONN__": {
                            "data": {
                                "scoped": "true",
                                "connection": "openai-gpt-3"
                            },
                            "label": "@Thibault"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "__IMTCONN__",
                        "type": "account:openai-gpt-3",
                        "label": "Connection",
                        "required": true
                    }
                ],
                "expect": [
                    {
                        "name": "select",
                        "type": "select",
                        "label": "Select Method",
                        "required": true,
                        "validate": {
                            "enum": [
                                "chat",
                                "prompt"
                            ]
                        }
                    },
                    {
                        "name": "temperature",
                        "type": "number",
                        "label": "Temperature",
                        "validate": {
                            "max": 2,
                            "min": 0
                        }
                    },
                    {
                        "name": "top_p",
                        "type": "number",
                        "label": "Top P",
                        "validate": {
                            "max": 1,
                            "min": 0
                        }
                    },
                    {
                        "name": "n_completions",
                        "type": "number",
                        "label": "Number"
                    },
                    {
                        "name": "frequency_penalty",
                        "type": "number",
                        "label": "Frequency Penalty",
                        "validate": {
                            "max": 2,
                            "min": -2
                        }
                    },
                    {
                        "name": "presence_penalty",
                        "type": "number",
                        "label": "Presence Penalty",
                        "validate": {
                            "max": 2,
                            "min": -2
                        }
                    },
                    {
                        "name": "logit_bias",
                        "spec": {
                            "name": "value",
                            "spec": [
                                {
                                    "name": "token",
                                    "type": "text",
                                    "label": "Token ID",
                                    "required": true
                                },
                                {
                                    "name": "probability",
                                    "type": "number",
                                    "label": "Probability",
                                    "required": true,
                                    "validate": {
                                        "max": 100,
                                        "min": -100
                                    }
                                }
                            ],
                            "type": "collection",
                            "label": "Token Probability"
                        },
                        "type": "array",
                        "label": "Token Probability"
                    },
                    {
                        "name": "seed",
                        "type": "integer",
                        "label": "Seed"
                    },
                    {
                        "name": "stop",
                        "spec": {
                            "name": "value",
                            "type": "text",
                            "label": "Stop Sequence"
                        },
                        "type": "array",
                        "label": "Stop Sequences",
                        "validate": {
                            "maxItems": 4
                        }
                    },
                    {
                        "name": "additionalParameters",
                        "spec": {
                            "name": "value",
                            "spec": [
                                {
                                    "name": "key",
                                    "type": "text",
                                    "label": "Parameter Name",
                                    "required": true
                                },
                                {
                                    "name": "type",
                                    "type": "select",
                                    "label": "Input Type",
                                    "options": [
                                        {
                                            "label": "Text",
                                            "value": "text",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "text",
                                                    "label": "Parameter Value"
                                                }
                                            ],
                                            "default": true
                                        },
                                        {
                                            "label": "Number",
                                            "value": "number",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "number",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        },
                                        {
                                            "label": "Boolean",
                                            "value": "boolean",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "boolean",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        },
                                        {
                                            "label": "Date",
                                            "value": "date",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "date",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        },
                                        {
                                            "label": "Any",
                                            "value": "any",
                                            "nested": [
                                                {
                                                    "name": "value",
                                                    "type": "any",
                                                    "label": "Parameter Value"
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "type": "collection",
                            "label": "Input Parameter"
                        },
                        "type": "array",
                        "label": "Other Input Parameters"
                    },
                    {
                        "name": "model",
                        "type": "select",
                        "label": "Model",
                        "required": true
                    },
                    {
                        "name": "max_tokens",
                        "type": "uinteger",
                        "label": "Max Completion Tokens"
                    },
                    {
                        "name": "messages",
                        "spec": {
                            "name": "value",
                            "spec": [
                                {
                                    "name": "role",
                                    "type": "select",
                                    "label": "Role",
                                    "options": {
                                        "store": [
                                            {
                                                "label": "System",
                                                "value": "system",
                                                "nested": [
                                                    {
                                                        "help": "Text content of the message on behalf of the selected __Role__.",
                                                        "name": "content",
                                                        "type": "text",
                                                        "label": "Text Content"
                                                    }
                                                ]
                                            },
                                            {
                                                "label": "User",
                                                "value": "user",
                                                "nested": [
                                                    {
                                                        "help": "Text content of the message on behalf of the selected __Role__.",
                                                        "name": "content",
                                                        "type": "text",
                                                        "label": "Text Content"
                                                    },
                                                    {
                                                        "name": "imageInputType",
                                                        "type": "select",
                                                        "label": "Image Input Type",
                                                        "options": [
                                                            {
                                                                "label": "URL",
                                                                "value": "url",
                                                                "nested": [
                                                                    {
                                                                        "help": "Make sure to use a publically accessible URL.\nYou can test if your image is publically accessible by opening the link in an incognito tab.",
                                                                        "name": "imageUrl",
                                                                        "type": "url",
                                                                        "label": "Image URL"
                                                                    }
                                                                ]
                                                            },
                                                            {
                                                                "label": "Image File",
                                                                "value": "file",
                                                                "nested": [
                                                                    {
                                                                        "name": "imageFile",
                                                                        "spec": [
                                                                            {
                                                                                "help": "Accepted extensions: `.jpg`, `.jpeg`, `.png`, `.webp` and `.gif`.",
                                                                                "name": "imageFilename",
                                                                                "type": "filename",
                                                                                "label": "Image Filename",
                                                                                "semantic": "file:name",
                                                                                "extension": [
                                                                                    "jpg",
                                                                                    "jpeg",
                                                                                    "png",
                                                                                    "webp",
                                                                                    "gif"
                                                                                ]
                                                                            },
                                                                            {
                                                                                "name": "imageData",
                                                                                "type": "buffer",
                                                                                "label": "Image Data",
                                                                                "semantic": "file:data"
                                                                            }
                                                                        ],
                                                                        "type": "collection",
                                                                        "label": "Image"
                                                                    }
                                                                ]
                                                            }
                                                        ],
                                                        "mappable": false
                                                    },
                                                    {
                                                        "name": "imageDetail",
                                                        "type": "select",
                                                        "label": "Image Detail",
                                                        "options": [
                                                            {
                                                                "label": "Auto",
                                                                "value": "auto",
                                                                "default": true
                                                            },
                                                            {
                                                                "label": "High",
                                                                "value": "high"
                                                            },
                                                            {
                                                                "label": "Low",
                                                                "value": "low"
                                                            }
                                                        ],
                                                        "advanced": true
                                                    }
                                                ]
                                            },
                                            {
                                                "label": "Assistant",
                                                "value": "assistant",
                                                "nested": [
                                                    {
                                                        "help": "Text content of the message on behalf of the selected __Role__.",
                                                        "name": "content",
                                                        "type": "text",
                                                        "label": "Text Content"
                                                    }
                                                ]
                                            }
                                        ]
                                    },
                                    "required": true
                                }
                            ],
                            "type": "collection",
                            "label": "Message"
                        },
                        "type": "array",
                        "label": "Messages",
                        "required": true
                    },
                    {
                        "name": "response_format",
                        "type": "select",
                        "label": "Response Format",
                        "validate": {
                            "enum": [
                                "text",
                                "json_object"
                            ]
                        }
                    }
                ],
                "interface": [
                    {
                        "name": "result",
                        "type": "any",
                        "label": "Result"
                    },
                    {
                        "name": "id",
                        "type": "text",
                        "label": "ID"
                    },
                    {
                        "name": "object",
                        "type": "text",
                        "label": "Object"
                    },
                    {
                        "name": "created",
                        "type": "date",
                        "label": "Created"
                    },
                    {
                        "name": "model",
                        "type": "text",
                        "label": "Model"
                    },
                    {
                        "name": "choices",
                        "spec": {
                            "spec": [
                                {
                                    "name": "text",
                                    "type": "text",
                                    "label": "Text"
                                },
                                {
                                    "name": "index",
                                    "type": "number",
                                    "label": "Index"
                                },
                                {
                                    "name": "logprobs",
                                    "type": "text",
                                    "label": "Log Probs"
                                },
                                {
                                    "name": "finish_reason",
                                    "type": "text",
                                    "label": "Finish Reason"
                                },
                                {
                                    "name": "message",
                                    "spec": [
                                        {
                                            "name": "role",
                                            "type": "text",
                                            "label": "Role"
                                        },
                                        {
                                            "name": "content",
                                            "type": "text",
                                            "label": "Content"
                                        },
                                        {
                                            "name": "refusal",
                                            "type": "text",
                                            "label": "Refusal"
                                        }
                                    ],
                                    "type": "collection",
                                    "label": "Message"
                                }
                            ],
                            "type": "collection"
                        },
                        "type": "array",
                        "label": "Choices"
                    },
                    {
                        "name": "usage",
                        "spec": [
                            {
                                "name": "prompt_tokens",
                                "type": "number",
                                "label": "Prompt Tokens"
                            },
                            {
                                "name": "completion_tokens",
                                "type": "text",
                                "label": "Completion Tokens"
                            },
                            {
                                "name": "total_tokens",
                                "type": "number",
                                "label": "Total Tokens"
                            },
                            {
                                "name": "prompt_tokens_details",
                                "spec": [
                                    {
                                        "name": "cached_tokens",
                                        "type": "uinteger",
                                        "label": "Cached Tokens"
                                    },
                                    {
                                        "name": "text_tokens",
                                        "type": "uinteger",
                                        "label": "Text Tokens"
                                    },
                                    {
                                        "name": "image_tokens",
                                        "type": "uinteger",
                                        "label": "Image Tokens"
                                    },
                                    {
                                        "name": "audio_tokens",
                                        "type": "uinteger",
                                        "label": "Audio Tokens"
                                    }
                                ],
                                "type": "collection",
                                "label": "Prompt Tokens Details"
                            },
                            {
                                "name": "completion_tokens_details",
                                "spec": [
                                    {
                                        "name": "reasoning_tokens",
                                        "type": "uinteger",
                                        "label": "Reasoning Tokens"
                                    },
                                    {
                                        "name": "text_tokens",
                                        "type": "uinteger",
                                        "label": "Text Tokens"
                                    },
                                    {
                                        "name": "audio_tokens",
                                        "type": "uinteger",
                                        "label": "Audio Tokens"
                                    }
                                ],
                                "type": "collection",
                                "label": "Completion Tokens Details"
                            }
                        ],
                        "type": "collection",
                        "label": "Usage"
                    },
                    {
                        "name": "system_fingerprint",
                        "type": "text",
                        "label": "System Fingerprint"
                    }
                ]
            }
        },
        {
            "id": 15,
            "module": "http:ActionSendData",
            "version": 3,
            "parameters": {
                "handleErrors": true,
                "useNewZLibDeCompress": true
            },
            "mapper": {
                "url": "https://fal.run/fal-ai/flux-pro/v1.1",
                "serializeUrl": false,
                "method": "post",
                "headers": [
                    {
                        "name": "Authorization",
                        "value": ""
                    }
                ],
                "qs": [],
                "bodyType": "raw",
                "parseResponse": true,
                "authUser": "",
                "authPass": "",
                "timeout": "",
                "shareCookies": false,
                "ca": "",
                "rejectUnauthorized": true,
                "followRedirect": true,
                "useQuerystring": false,
                "gzip": true,
                "useMtls": false,
                "contentType": "application/json",
                "data": "{\n    \"prompt\": \"{{replace(16.result; \"\"\"\"; emptystring)}}\",\n    \"image_size\": {\n        \"width\": 1280,\n        \"height\": 400\n    },\n    \"num_inference_steps\": 28,\n    \"guidance_scale\": 3.5,\n    \"num_images\": 1,\n    \"enable_safety_checker\": false,\n    \"output_format\": \"jpeg\"\n}",
                "followAllRedirects": false
            },
            "metadata": {
                "designer": {
                    "x": 900,
                    "y": 150
                },
                "restore": {
                    "expect": {
                        "method": {
                            "mode": "chose",
                            "label": "POST"
                        },
                        "headers": {
                            "mode": "chose",
                            "items": [
                                null
                            ]
                        },
                        "qs": {
                            "mode": "chose"
                        },
                        "bodyType": {
                            "label": "Raw"
                        },
                        "contentType": {
                            "label": "JSON (application/json)"
                        }
                    }
                },
                "parameters": [
                    {
                        "name": "handleErrors",
                        "type": "boolean",
                        "label": "Evaluate all states as errors (except for 2xx and 3xx )",
                        "required": true
                    },
                    {
                        "name": "useNewZLibDeCompress",
                        "type": "hidden"
                    }
                ],
                "expect": [
                    {
                        "name": "url",
                        "type": "url",
                        "label": "URL",
                        "required": true
                    },
                    {
                        "name": "serializeUrl",
                        "type": "boolean",
                        "label": "Serialize URL",
                        "required": true
                    },
                    {
                        "name": "method",
                        "type": "select",
                        "label": "Method",
                        "required": true,
                        "validate": {
                            "enum": [
                                "get",
                                "head",
                                "post",
                                "put",
                                "patch",
                                "delete",
                                "options"
                            ]
                        }
                    },
                    {
                        "name": "headers",
                        "type": "array",
                        "label": "Headers",
                        "spec": [
                            {
                                "name": "name",
                                "label": "Name",
                                "type": "text",
                                "required": true
                            },
                            {
                                "name": "value",
                                "label": "Value",
                                "type": "text"
                            }
                        ]
                    },
                    {
                        "name": "qs",
                        "type": "array",
                        "label": "Query String",
                        "spec": [
                            {
                                "name": "name",
                                "label": "Name",
                                "type": "text",
                                "required": true
                            },
                            {
                                "name": "value",
                                "label": "Value",
                                "type": "text"
                            }
                        ]
                    },
                    {
                        "name": "bodyType",
                        "type": "select",
                        "label": "Body type",
                        "validate": {
                            "enum": [
                                "raw",
                                "x_www_form_urlencoded",
                                "multipart_form_data"
                            ]
                        }
                    },
                    {
                        "name": "parseResponse",
                        "type": "boolean",
                        "label": "Parse response",
                        "required": true
                    },
                    {
                        "name": "authUser",
                        "type": "text",
                        "label": "User name"
                    },
                    {
                        "name": "authPass",
                        "type": "password",
                        "label": "Password"
                    },
                    {
                        "name": "timeout",
                        "type": "uinteger",
                        "label": "Timeout",
                        "validate": {
                            "max": 300,
                            "min": 1
                        }
                    },
                    {
                        "name": "shareCookies",
                        "type": "boolean",
                        "label": "Share cookies with other HTTP modules",
                        "required": true
                    },
                    {
                        "name": "ca",
                        "type": "cert",
                        "label": "Self-signed certificate"
                    },
                    {
                        "name": "rejectUnauthorized",
                        "type": "boolean",
                        "label": "Reject connections that are using unverified (self-signed) certificates",
                        "required": true
                    },
                    {
                        "name": "followRedirect",
                        "type": "boolean",
                        "label": "Follow redirect",
                        "required": true
                    },
                    {
                        "name": "useQuerystring",
                        "type": "boolean",
                        "label": "Disable serialization of multiple same query string keys as arrays",
                        "required": true
                    },
                    {
                        "name": "gzip",
                        "type": "boolean",
                        "label": "Request compressed content",
                        "required": true
                    },
                    {
                        "name": "useMtls",
                        "type": "boolean",
                        "label": "Use Mutual TLS",
                        "required": true
                    },
                    {
                        "name": "contentType",
                        "type": "select",
                        "label": "Content type",
                        "validate": {
                            "enum": [
                                "text/plain",
                                "application/json",
                                "application/xml",
                                "text/xml",
                                "text/html",
                                "custom"
                            ]
                        }
                    },
                    {
                        "name": "data",
                        "type": "buffer",
                        "label": "Request content"
                    },
                    {
                        "name": "followAllRedirects",
                        "type": "boolean",
                        "label": "Follow all redirect",
                        "required": true
                    }
                ]
            }
        },
        {
            "id": 24,
            "module": "builtin:BasicRouter",
            "version": 1,
            "mapper": null,
            "metadata": {
                "designer": {
                    "x": 1200,
                    "y": 150
                }
            },
            "routes": [
                {
                    "flow": [
                        {
                            "id": 4,
                            "module": "google-docs:addAnImageToADocument",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 1998737
                            },
                            "mapper": {
                                "uri": "{{15.data.images[].url}}",
                                "choose": "dropdown",
                                "select": "document",
                                "document": "/1z4f7KFGYd5sIgfMGhmxX7nOAnBVBbH0f7_O9w6Tm_MA",
                                "destination": "drive"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 1500,
                                    "y": 0
                                },
                                "restore": {
                                    "expect": {
                                        "choose": {
                                            "label": "By Dropdown"
                                        },
                                        "select": {
                                            "label": "By appending to the document"
                                        },
                                        "document": {
                                            "mode": "chose",
                                            "path": [
                                                "Livre blanc"
                                            ]
                                        },
                                        "destination": {
                                            "label": "My Drive"
                                        }
                                    },
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "data": {
                                                "scoped": "true",
                                                "connection": "google"
                                            },
                                            "label": "@Thibault (hello@ottho.fr)"
                                        }
                                    }
                                },
                                "parameters": [
                                    {
                                        "name": "__IMTCONN__",
                                        "type": "account:google",
                                        "label": "Connection",
                                        "required": true
                                    }
                                ],
                                "expect": [
                                    {
                                        "name": "choose",
                                        "type": "select",
                                        "label": "Select a Document",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "mapping",
                                                "dropdown"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "destination",
                                        "type": "select",
                                        "label": "Choose a Drive",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "drive",
                                                "share",
                                                "team"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "document",
                                        "type": "file",
                                        "label": "Document ID",
                                        "required": true
                                    },
                                    {
                                        "name": "select",
                                        "type": "select",
                                        "label": "Insert an Image",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "location",
                                                "document",
                                                "segment"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "uri",
                                        "type": "url",
                                        "label": "Image URL",
                                        "required": true
                                    },
                                    {
                                        "name": "height_magnitude",
                                        "type": "number",
                                        "label": "Height Magnitude in Points"
                                    },
                                    {
                                        "name": "width_magnitude",
                                        "type": "number",
                                        "label": "Width Magnitude in Points"
                                    }
                                ]
                            }
                        },
                        {
                            "id": 13,
                            "module": "google-docs:appendADocument",
                            "version": 1,
                            "parameters": {
                                "__IMTCONN__": 1998737
                            },
                            "mapper": {
                                "text": "{{10.choices[].message.content}}",
                                "choose": "dropdown",
                                "select": "document",
                                "document": "/1z4f7KFGYd5sIgfMGhmxX7nOAnBVBbH0f7_O9w6Tm_MA",
                                "destination": "drive"
                            },
                            "metadata": {
                                "designer": {
                                    "x": 1840,
                                    "y": 22
                                },
                                "restore": {
                                    "expect": {
                                        "choose": {
                                            "label": "By Dropdown"
                                        },
                                        "select": {
                                            "label": "By appending to the body of document"
                                        },
                                        "document": {
                                            "path": [
                                                "Livre blanc"
                                            ]
                                        },
                                        "destination": {
                                            "label": "My Drive"
                                        }
                                    },
                                    "parameters": {
                                        "__IMTCONN__": {
                                            "data": {
                                                "scoped": "true",
                                                "connection": "google"
                                            },
                                            "label": "@Thibault (hello@ottho.fr)"
                                        }
                                    }
                                },
                                "parameters": [
                                    {
                                        "name": "__IMTCONN__",
                                        "type": "account:google",
                                        "label": "Connection",
                                        "required": true
                                    }
                                ],
                                "expect": [
                                    {
                                        "name": "choose",
                                        "type": "select",
                                        "label": "Select a Document",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "mapping",
                                                "dropdown"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "destination",
                                        "type": "select",
                                        "label": "Choose a Drive",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "drive",
                                                "share",
                                                "team"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "document",
                                        "type": "file",
                                        "label": "Document ID",
                                        "required": true
                                    },
                                    {
                                        "name": "select",
                                        "type": "select",
                                        "label": "Insert a Paragraph",
                                        "required": true,
                                        "validate": {
                                            "enum": [
                                                "location",
                                                "document",
                                                "segment"
                                            ]
                                        }
                                    },
                                    {
                                        "name": "text",
                                        "type": "text",
                                        "label": "Appended Text",
                                        "required": true
                                    }
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "metadata": {
        "instant": false,
        "version": 1,
        "scenario": {
            "roundtrips": 1,
            "maxErrors": 3,
            "autoCommit": true,
            "autoCommitTriggerLast": true,
            "sequential": false,
            "slots": null,
            "confidential": false,
            "dataloss": false,
            "dlq": false,
            "freshVariables": false
        },
        "designer": {
            "orphans": [
                [
                    {
                        "id": 1,
                        "module": "google-docs:getADocument",
                        "version": 1,
                        "parameters": {
                            "__IMTCONN__": 1998737
                        },
                        "mapper": {
                            "filter": "image",
                            "select": "dropdown",
                            "document": "/1z4f7KFGYd5sIgfMGhmxX7nOAnBVBbH0f7_O9w6Tm_MA",
                            "destination": "drive",
                            "includeTabsContent": false
                        },
                        "metadata": {
                            "designer": {
                                "x": -281,
                                "y": -267,
                                "messages": [
                                    {
                                        "category": "link",
                                        "severity": "warning",
                                        "message": "The module is not connected to the data flow."
                                    }
                                ]
                            },
                            "restore": {
                                "expect": {
                                    "filter": {
                                        "label": "Image"
                                    },
                                    "select": {
                                        "label": "By Dropdown"
                                    },
                                    "document": {
                                        "path": [
                                            "Livre blanc"
                                        ]
                                    },
                                    "destination": {
                                        "label": "My Drive"
                                    }
                                },
                                "parameters": {
                                    "__IMTCONN__": {
                                        "data": {
                                            "scoped": "true",
                                            "connection": "google"
                                        },
                                        "label": "@Thibault (hello@ottho.fr)"
                                    }
                                }
                            },
                            "parameters": [
                                {
                                    "name": "__IMTCONN__",
                                    "type": "account:google",
                                    "label": "Connection",
                                    "required": true
                                }
                            ],
                            "expect": [
                                {
                                    "name": "select",
                                    "type": "select",
                                    "label": "Get Content of a Document",
                                    "required": true,
                                    "validate": {
                                        "enum": [
                                            "map",
                                            "dropdown"
                                        ]
                                    }
                                },
                                {
                                    "name": "includeTabsContent",
                                    "type": "boolean",
                                    "label": "Include Tabs Content",
                                    "required": true
                                },
                                {
                                    "name": "filter",
                                    "type": "select",
                                    "label": "Filter",
                                    "required": true,
                                    "validate": {
                                        "enum": [
                                            "image",
                                            "drawing",
                                            "chart"
                                        ]
                                    }
                                },
                                {
                                    "name": "destination",
                                    "type": "select",
                                    "label": "Choose a Drive",
                                    "required": true,
                                    "validate": {
                                        "enum": [
                                            "drive",
                                            "share",
                                            "team"
                                        ]
                                    }
                                },
                                {
                                    "name": "document",
                                    "type": "file",
                                    "label": "Document ID",
                                    "required": true
                                }
                            ]
                        }
                    },
                    {
                        "id": 7,
                        "module": "perplexity-ai:createAChatCompletion",
                        "version": 1,
                        "parameters": {
                            "__IMTCONN__": 2932101
                        },
                        "mapper": {
                            "model": "llama-3.1-sonar-large-128k-online",
                            "messages": [
                                {
                                    "role": "user",
                                    "content": "Based on the following theme, suggest a white paper table of contents on the topic {{1.text}} in 10 points.\n\nAlways write in French. \n\nDo not use markdown-style formatting in your response. Separate the titles with line breaks.\n"
                                }
                            ],
                            "max_tokens": "2000"
                        },
                        "metadata": {
                            "designer": {
                                "x": -30,
                                "y": -259
                            },
                            "restore": {
                                "expect": {
                                    "model": {
                                        "mode": "chose",
                                        "label": "llama-3.1-sonar-large-128k-online"
                                    },
                                    "messages": {
                                        "mode": "chose",
                                        "items": [
                                            {
                                                "role": {
                                                    "mode": "chose",
                                                    "label": "User"
                                                }
                                            }
                                        ]
                                    },
                                    "return_images": {
                                        "mode": "chose"
                                    },
                                    "search_domain_filter": {
                                        "mode": "chose"
                                    },
                                    "search_recency_filter": {
                                        "mode": "chose",
                                        "label": "Empty"
                                    },
                                    "return_related_questions": {
                                        "mode": "chose"
                                    }
                                },
                                "parameters": {
                                    "__IMTCONN__": {
                                        "data": {
                                            "scoped": "true",
                                            "connection": "perplexity-ai"
                                        },
                                        "label": "My Perplexity connection"
                                    }
                                }
                            },
                            "parameters": [
                                {
                                    "name": "__IMTCONN__",
                                    "type": "account:perplexity-ai",
                                    "label": "Connection",
                                    "required": true
                                }
                            ],
                            "expect": [
                                {
                                    "name": "model",
                                    "type": "select",
                                    "label": "Model",
                                    "required": true
                                },
                                {
                                    "name": "messages",
                                    "spec": [
                                        {
                                            "name": "content",
                                            "type": "text",
                                            "label": "Content",
                                            "required": true
                                        },
                                        {
                                            "name": "role",
                                            "type": "select",
                                            "label": "Role",
                                            "options": [
                                                {
                                                    "label": "User",
                                                    "value": "user"
                                                },
                                                {
                                                    "label": "Assistant",
                                                    "value": "assistant"
                                                },
                                                {
                                                    "label": "System",
                                                    "value": "system"
                                                }
                                            ],
                                            "required": true
                                        }
                                    ],
                                    "type": "array",
                                    "label": "Messages",
                                    "required": true
                                },
                                {
                                    "name": "max_tokens",
                                    "type": "number",
                                    "label": "Max Tokens"
                                },
                                {
                                    "name": "temperature",
                                    "type": "number",
                                    "label": "Temperature",
                                    "validate": {
                                        "max": 1.999,
                                        "min": 0
                                    }
                                },
                                {
                                    "name": "top_p",
                                    "type": "number",
                                    "label": "Top P",
                                    "validate": {
                                        "max": 1,
                                        "min": 0
                                    }
                                },
                                {
                                    "name": "top_k",
                                    "type": "number",
                                    "label": "Top K",
                                    "validate": {
                                        "max": 2048,
                                        "min": 0
                                    }
                                },
                                {
                                    "name": "presence_penalty",
                                    "type": "number",
                                    "label": "Presence Penalty",
                                    "validate": {
                                        "max": 2,
                                        "min": -2
                                    }
                                },
                                {
                                    "name": "frequency_penalty",
                                    "type": "number",
                                    "label": "Frequency Penalty",
                                    "validate": {
                                        "min": 0
                                    }
                                },
                                {
                                    "name": "search_domain_filter",
                                    "spec": {
                                        "name": "value",
                                        "type": "text"
                                    },
                                    "type": "array",
                                    "label": "Search Domain Filter"
                                },
                                {
                                    "name": "search_recency_filter",
                                    "type": "select",
                                    "label": "Search Recency Filter",
                                    "validate": {
                                        "enum": [
                                            "month",
                                            "week",
                                            "day",
                                            "hour"
                                        ]
                                    }
                                },
                                {
                                    "name": "return_images",
                                    "type": "boolean",
                                    "label": "Return Images"
                                },
                                {
                                    "name": "return_related_questions",
                                    "type": "boolean",
                                    "label": "Return Related Questions"
                                }
                            ]
                        }
                    },
                    {
                        "id": 11,
                        "module": "google-docs:appendADocument",
                        "version": 1,
                        "parameters": {
                            "__IMTCONN__": 1998737
                        },
                        "mapper": {
                            "text": "{{7.choices[].message.content}}",
                            "choose": "dropdown",
                            "select": "document",
                            "document": "/1z4f7KFGYd5sIgfMGhmxX7nOAnBVBbH0f7_O9w6Tm_MA",
                            "destination": "drive"
                        },
                        "metadata": {
                            "designer": {
                                "x": 233,
                                "y": -255
                            },
                            "restore": {
                                "expect": {
                                    "choose": {
                                        "label": "By Dropdown"
                                    },
                                    "select": {
                                        "label": "By appending to the body of document"
                                    },
                                    "document": {
                                        "path": [
                                            "Livre blanc"
                                        ]
                                    },
                                    "destination": {
                                        "label": "My Drive"
                                    }
                                },
                                "parameters": {
                                    "__IMTCONN__": {
                                        "data": {
                                            "scoped": "true",
                                            "connection": "google"
                                        },
                                        "label": "@Thibault (hello@ottho.fr)"
                                    }
                                }
                            },
                            "parameters": [
                                {
                                    "name": "__IMTCONN__",
                                    "type": "account:google",
                                    "label": "Connection",
                                    "required": true
                                }
                            ],
                            "expect": [
                                {
                                    "name": "choose",
                                    "type": "select",
                                    "label": "Select a Document",
                                    "required": true,
                                    "validate": {
                                        "enum": [
                                            "mapping",
                                            "dropdown"
                                        ]
                                    }
                                },
                                {
                                    "name": "destination",
                                    "type": "select",
                                    "label": "Choose a Drive",
                                    "required": true,
                                    "validate": {
                                        "enum": [
                                            "drive",
                                            "share",
                                            "team"
                                        ]
                                    }
                                },
                                {
                                    "name": "document",
                                    "type": "file",
                                    "label": "Document ID",
                                    "required": true
                                },
                                {
                                    "name": "select",
                                    "type": "select",
                                    "label": "Insert a Paragraph",
                                    "required": true,
                                    "validate": {
                                        "enum": [
                                            "location",
                                            "document",
                                            "segment"
                                        ]
                                    }
                                },
                                {
                                    "name": "text",
                                    "type": "text",
                                    "label": "Appended Text",
                                    "required": true
                                }
                            ]
                        }
                    }
                ]
            ]
        },
        "zone": "eu1.make.com"
    }
}
<!---
zitouniislam24/zitouniislam24 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.

