Innovative Workflows in Large Language Models (LLMs)
DePaul University, Chicago, IL
Research Report by Adithya Harsha
1. Introduction
The AGENTIC RAG (Retrieval-Augmented Generation) Workflow is a structured approach integrating AI-driven retrieval and generation mechanisms. It enhances accuracy, efficiency, and contextual understanding in conversational AI systems. This report provides an in-depth analysis of the workflow, its components, applications, challenges, and optimization strategies.

2. Workflow Overview
The AGENTIC RAG Workflow consists of key components responsible for query processing, retrieval, refinement, and output generation.

Table 1: Core Components of AGENTIC RAG Workflow
Component	Functionality	Technology Used
My_AI_Assistant	Initiates interactions with the user	LangChain
Vector_Retriever	Retrieves relevant documents from the database	ChromaDB
Query_Rewriter	Refines ambiguous or complex queries	LLM-based Rewriting
Output_Generator	Generates final responses based on retrieved documents	Groq LLM
4. Key Technical Implementations
4.1 Embedding and Retrieval Mechanism
Chunk Splitting: Text is split into smaller pieces for efficient retrieval.
Vector Storage: Documents are stored in ChromaDB for fast access.
python
Copy
Edit
text_splitter = RecursiveCharacterTextSplitter.from_tiktoken_encoder(chunk_size=100, chunk_overlap=5)
chunks = text_splitter.split_documents([doc])
vectorstore = Chroma.from_documents(documents=chunks, embedding=embeddings)
4.2 Conditional Logic for Query Processing
The system determines if retrieved documents are relevant before proceeding to response generation.
python
Copy
Edit
def grade_documents(state):
    prompt = PromptTemplate(
        template="""You are a grader. Is the document relevant to the question?
        Document: {context}
        Question: {question}
        Answer 'yes' or 'no'.""",
        input_variables=["context", "question"]
    )
    score = prompt | llm
    return "Output_Generator" if score == "yes" else "Query_Rewriter"
Table 2: Query Processing Paths
Query Type	Processing Path	Output Stage
Clear Query	Direct retrieval → Generation	Final Response
Ambiguous Query	Refinement → Retrieval → Generation	Query Rewritten
Low Relevance	Re-retrieval → New Processing	Adjusted Response
5. Applications of AGENTIC RAG Workflow
5.1 Education
Automated Grading: AI can analyze student answers and grade assignments.
Interactive Learning: The system can act as a real-time tutor for students.
5.2 Healthcare
Medical Article Retrieval: AI fetches the most relevant research articles.
Decision Support Systems: Doctors can use AI-driven insights for better decision-making.
5.3 Business Intelligence
Trend Identification: AI analyzes large datasets to discover market trends.
Semantic Search: Business reports and insights can be retrieved more effectively.
Table 3: Industry-Specific Applications
Industry	Use Case	Benefit
Education	AI tutoring and grading	Faster learning
Healthcare	Medical research retrieval	Accurate diagnosis
Customer Support	Automated FAQ handling	Faster response time
Business	Market analysis	Data-driven insights
6. Advanced Features
6.1 Query Refinement
The system can automatically rephrase vague queries to improve retrieval accuracy.

python
Copy
Edit
def rewrite_query(state):
    question = state['messages'][0].content
    refined_question = llm.invoke([f"Refine this question: {question}"])
    return refined_question.content
6.2 Tool Integration
Currency Conversion: Real-time currency exchange rate retrieval.
Weather Updates: Provides real-time weather forecasts.
Live Data Fetching: AI integrates with APIs to fetch dynamic data.
7. Training and Model Optimization
7.1 Research-Based Model Tuning
Training and fine-tuning the models were influenced by research papers:

Agent: A Survey of Recent Advances in Agent-Oriented Programming
AGENTIC: The Evolution of Autonomous Agent Architectures
Table 4: Model Optimization Strategies
Optimization Technique	Benefit
Fine-tuning on domain data	Improved contextual relevance
Optimized chunk size	Faster retrieval performance
Query intent detection	More precise responses
8. Challenges and Solutions
8.1 Handling Ambiguous Queries
Challenge: Users may input unclear questions.
Solution: AI-driven query refinement enhances clarity.
8.2 System Latency
Challenge: Large LLMs can introduce processing delays.
Solution: Optimized chunk storage and retrieval reduce response time.
8.3 Scalability Issues
Challenge: Supporting multiple users simultaneously.
Solution: Parallel processing and load balancing improve scalability.
Table 5: Challenges and Recommended Solutions
Challenge	Solution
Ambiguous Queries	Query Refinement with LLM
Latency Issues	Faster embeddings and chunking
Scalability Concerns	Load balancing with cloud systems
9. Performance Evaluation
Query Processing Metrics
User Query Token Usage: 1039 tokens
Tool Call Processing Time: 0.156 sec
AI Response Time: 0.116 sec
Total Time Taken: 0.189 sec
Total Tokens Processed: 1125
10. Conclusion
The AGENTIC RAG Workflow provides an intelligent, scalable, and optimized approach to AI-driven retrieval and generation. With continuous improvements in model fine-tuning, response accuracy, and system efficiency, this workflow can be applied across various industries to enhance automated decision-making and user interactions.
