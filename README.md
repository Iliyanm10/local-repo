## AI Teaching Assistant for NLP Courses

An AI-powered teaching assistant leveraging **Retrieval-Augmented Generation (RAG)** to answer course-specific questions for SEP 775: Computational Natural Language Processing at McMaster University.


## 📖 Project Overview

This project combines **dense retrieval** (DPR), **FAISS similarity search**, and **T5 text generation** to create an interactive AI assistant. It retrieves course-specific information from a vector database and generates context-aware answers to student queries, mimicking a human teaching assistant.

**Key Features**:
The system works as follows:

1. **Context Encoding:**  It uses a DPR context encoder to generate embeddings for context passages from a text document. These embeddings capture the semantic meaning of the passages.
2. **Question Encoding:** Similarly, a DPR question encoder generates embeddings for user questions.
3. **Similarity Search:** When a user asks a question, the system finds the most similar context passages in the database based on the embeddings of the question and context passages. FAISS (Facebook AI Similarity Search) is used for efficient similarity search.
4. **Query Generation:** The system generates a refined query based on the initial question and the retrieved context. This uses a T5 model to rephrase the question to be more specific to the context.
5. **Answer Extraction:** The relevant context passage(s) are then used to extract the answer to the question.


## 🛠️ Installation

**Prerequisites**
- Python ≥ 3.8
- GPU recommended for faster inference

**Dependencies**
```bash
pip install torch transformers datasets faiss-cpu sentence-transformers
```


## 📂 Dataset

The dataset contains **33 question-answer pairs** in a modified SQuAD format for NLP course content. Each entry includes:
- 'id': Unique identifier
- 'context': Course material paragraph
- 'negative_context': Distractor passages
- 'question': Student query
- 'answers': Correct answers

**Example Structure**:
```python
Dataset({
    features: ['id', 'title', 'context', 'negative_context', 'question', 'answers'],
    num_rows: 33
})
```


## 🤖 Model Architecture

### RAG Pipeline Components
1. **Retriever**:
   - **DPR** (Dense Passage Retrieval): Encodes queries/docs into vectors.
   - **FAISS**: Efficient similarity search for top-k relevant contexts.

2. **Generator**:
   - **T5 (din0s/t5-base-msmarco-nlgen-ob)**: Fine-tuned on MS MARCO for open-ended QA.



## 🚀 Setup

## Step 1: Install Dependencies:
bash pip install torch transformers datasets transformers[torch] faiss-cpu faiss-gpu


## Step 2: Prepare Dataset:
Require a text file (e.g., `TA_dataset_Final.txt`) containing your context data. Each line of the file should be a JSON object with the following structure:

json { "id": "unique_id", "title": "title_of_passage", "context": "the_context_passage_text", "question": "the_question", "answers": ["list_of_answers"], "negative_context": ["list_of_irrelevant_context_passages"] }

 
## Step 3: Run the Code:
Execute the Python script that contains the code for loading the models, building the context database, and answering questions.


### Step 4: Query the AI Assistant
```python
questions = [
    "How many units is SEP 775 course?",
]

for question in questions:
    generate_question_embedding(question)
```

**Sample Output**:
```
Question: How many units is SEP 775 course?
Generate Answer: SEP 775 course is 3 units.
```


## 🚀 Usage

1. **Ask a Question:**
Provide a question as input to the `generate_question_embedding` function. 

2. **Get the Answer:**
The system will retrieve the most relevant context passage(s) and it will extract the answer directly.


## 📊 Results

### Example Responses
| Question | Generated Answer |
|----------|------------------|
| "Prerequisites for SEP 775?" | "Students must complete SEP 740 or SEP 788/789." |
| "Role of POS tagging?" | "Helps understand syntactic structure for parsing and NER." |

**Limitations**:
- Occasional inaccuracies in generated responses.
- Small dataset size (33 entries) limits coverage.


## 📚 References
- [AWS: Retrieval-Augmented Generation Explained](https://aws.amazon.com/what-is/retrieval-augmented-generation/)
- [T5 Paper](https://arxiv.org/abs/1910.10683)
- [FAISS Documentation](https://faiss.ai/)


## 👥 Contributors
- **Abhishek Gambhir** - 400546232
- **Nan Zhao** - 000370242
- **Iliyan Moosani** - 400587184  
*Supervised by Dr. Hamidreza Mahyar*

*McMaster University, 2025*
