# PDF Locker Script

This Python script allows you to lock a PDF file with a password using the `PyPDF2` library. The script prompts the user for the path to the PDF file and a password, then encrypts the PDF with the provided password.

## Prerequisites

Before running the script, ensure you have the following libraries installed:

- `PyPDF2`
- `getpass`
- `colorama`

You can install them using `pip`:

```bash
pip install PyPDF2 getpass colorama
```

## Script Explanation

Here's a breakdown of the script:

1. **Import Libraries**: The necessary libraries are imported. `getpass` is used to securely get the password from the user, and `colorama` is used for colored terminal output.

2. **Initialize Colorama**: Colorama is initialized to allow colored text in the terminal.

3. **Function to Lock PDF**: 
    - `lock_pdf(input_file, password)`: This function takes the path to the PDF file and the password as arguments.
    - It opens the PDF file in read mode and creates a PDF reader object.
    - A PDF writer object is created, and all pages from the reader are added to the writer.
    - The writer encrypts the PDF with the provided password and writes the encrypted content back to the original file.

4. **Get User Input**: The script prompts the user to enter the path to the PDF file and the password to lock the PDF. The `getpass` function ensures the password is not displayed on the screen.

5. **Lock the PDF**: The script calls the `lock_pdf` function to encrypt the PDF with the provided password and notifies the user upon completion.

## Usage

Run the script using a Python interpreter. You will be prompted to enter the path to the PDF file and the password. The script will then lock the PDF with the provided password.

```python
# Import the necessary libraries
import PyPDF2, getpass # getpass is for getting password with some level of security
from colorama import Fore, init

# Initialize colorama for colored output
init()

# Function to lock pdf
def lock_pdf(input_file, password):
   with open(input_file, 'rb') as file:
       # Create a PDF reader object
       pdf_reader = PyPDF2.PdfReader(file)
       # Create a PDF writer object
       pdf_writer = PyPDF2.PdfWriter()
       # Add all pages to the writer
       for page_num in range(len(pdf_reader.pages)):
           pdf_writer.add_page(pdf_reader.pages[page_num])
       # Encrypt the PDF with the provided password
       pdf_writer.encrypt(password)
       # Write the encrypted content back to the original file
       with open(input_file, 'wb') as output_file:
           pdf_writer.write(output_file)
           
# Get user input
input_pdf = input("Enter the path to the PDF file: ")
password = getpass.getpass("Enter the password to lock the PDF: ")

# Lock the PDF using PyPDF2
print(f'{Fore.GREEN}[!] Please hold on for a few seconds..')
lock_pdf(input_pdf, password)

# Let the user know it's done
print(f"{Fore.GREEN}[+] PDF locked successfully.")
```

## Notes

- Ensure you have write permissions for the PDF file you are trying to lock.
- The script overwrites the original PDF file with the encrypted version.

By following the above instructions and script, you can securely lock your PDF files with a password.
