# RAG_ChromaDB_llama3.2

Data: pdf can be downloaded from - https://openstax.org/details/books/concepts-biology

RAG pipeline code will parse two chapters (4 & 5) from the pdf and create a concatenated string.

System design document shows the overall architecture.


Overview:

I have developed this RAG pipeline without existing frameworks (langchain or llamaindex). This pipeline has been built using below components:
●	Data - Chapter 4 & 5 from the Concpets of Biology (WEB) pdf
●	Embedding model - all-MiniLM-L6-v2
●	Vector database - ChromaDB
●	LLM - llama-3.2-1 B-Instruct 

Assumptions:

●	Picked-up latest llama 3.2 1 B instruct model to optimize for compute while trading off a bit on the accuracy of the output
●	BLEU/ROUGE score calculation not required
●	Human centric assessment of model output is feasible given the limited content
●	We do not need to generate embedding of images present in the book
●	Space-Time complexity has not been dealt with in this design

Open items:

●	Semantic search in Chromadb is not very accurate. In case of out of syllabus question the semantic search is still producing some sources from data which had to be dealt with while publishing the response
●	Overlapping in chunking function to be added for better context awareness
●	Duplication check on Chromadb to be implemented to ensure same embeddings do not get uploaded in it
●	It will treat every question independently because historical conversation per session is yet to be added
●	In case of out of syllabus question the semantic search is still producing some sources from data which had to be dealt with while publishing the response
●	Warning while executing functions need to be tackled for robustness

Improvement areas/Next Steps:

●	Test different embedding models to check for better accuracy
●	Implement BM-25 for semantic search rather than using default HNSW algo
●	LLM model can be quantized to reduce the overall compute requirement
●	Hyperparameter tuning such as learning rate, batch size per device and #epochs
●	Fine-tune the LLM based on specific content (Biology in our case)
●	Use LLM itself to compare the Ground Truth with Actual Response
●	Make the Q&A multi-modal by adding search by image option
●	Deploy to cloud with user authentication to serve parallel sessions

Refrences 

https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct
https://python.langchain.com/docs/tutorials/pdf_qa/
https://www.youtube.com/watch?v=2TJxpyO3ei4
https://stackoverflow.com/questions/69609401/suppress-huggingface-logging-warning-setting-pad-token-id-to-eos-token-id
https://www.datacamp.com/tutorial/fine-tuning-llama-3-2
https://huggingface.co/blog/ImranzamanML/fine-tuning-1b-llama-32-a-comprehensive-article
https://www.youtube.com/watch?v=ABNxNFPqIGQ
