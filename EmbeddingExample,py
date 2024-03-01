# Import necessary libraries
import pdfplumber
import nltk

# Ensure you've downloaded the NLTK tokenizers
nltk.download('punkt')

# Function to tokenize text and split into chunks
def split_text_into_chunks(text, chunk_size=500, overlap=50):
    # Tokenize the text
    tokens = nltk.word_tokenize(text)
    
    # Initialize variables to store chunks
    chunks = []
    current_chunk = []
    current_size = 0
    
    for token in tokens:
        current_chunk.append(token)
        current_size += 1
        
        if current_size >= chunk_size:
            chunks.append(' '.join(current_chunk))
            # Start the next chunk with the overlap from the previous chunk
            current_chunk = current_chunk[-overlap:]
            current_size = len(current_chunk)
    
    # Add the last chunk if it has content
    if current_chunk:
        chunks.append(' '.join(current_chunk))
    
    return chunks

# Main function to process the PDF and split it into chunks
def process_pdf(file_path):
    full_text = ''
    with pdfplumber.open(file_path) as pdf:
        for page in pdf.pages:
            page_text = page.extract_text()
            if page_text:
                full_text += page_text + ' '
    
    chunks = split_text_into_chunks(full_text)
    print(f"Total number of chunks: {len(chunks)}")

# Replace 'your_pdf_path_here.pdf' with the actual path to your Dracula PDF
process_pdf("Dracula+by+Bram+Stoker.pdf")
