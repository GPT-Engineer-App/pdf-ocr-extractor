# pdf-ocr-extractor

below is code converting pdf to ocr with tesseract.exe, but my system saying file is not safe to run, can u change code and use another approch to convert pdf with ocr and save extract word to excel code is  "import fitz  # PyMuPDF
import pytesseract
from PIL import Image
import pandas as pd
import os

# Path to the PDF file
pdf_path = r'D:\TIMG\screenshot_1.pdf'

# Path to save the Excel file
excel_path = r'D:\TIMG\recognized_text.xlsx'

# Ensure Tesseract-OCR is installed and its path is set correctly
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'

def pdf_to_text(pdf_path):
    # Open the PDF file
    pdf_document = fitz.open(pdf_path)
    recognized_text = []

    # Iterate through each page
    for page_num in range(len(pdf_document)):
        page = pdf_document.load_page(page_num)
        pix = page.get_pixmap()
        img = Image.frombytes("RGB", [pix.width, pix.height], pix.samples)

        # Perform OCR on the image
        text = pytesseract.image_to_string(img)
        recognized_text.append(text)

    return recognized_text

def save_to_excel(text_list, excel_path):
    # Create a DataFrame
    df = pd.DataFrame({'Recognized Text': text_list})

    # Save the DataFrame to an Excel file
    df.to_excel(excel_path, index=False)

def main():
    # Perform OCR on the PDF
    recognized_text = pdf_to_text(pdf_path)

    # Print the recognized text
    for page_num, text in enumerate(recognized_text):
        print(f"Page {page_num + 1}:\n{text}\n")

    # Save the recognized text to an Excel file
    save_to_excel(recognized_text, excel_path)
    print(f"Recognized text saved to {excel_path}")

if __name__ == "__main__":
    main()"
 

## Collaborate with GPT Engineer

This is a [gptengineer.app](https://gptengineer.app)-synced repository 🌟🤖

Changes made via gptengineer.app will be committed to this repo.

If you clone this repo and push changes, you will have them reflected in the GPT Engineer UI.

## Tech stack

This project is built with React and Chakra UI.

- Vite
- React
- Chakra UI

## Setup

```sh
git clone https://github.com/GPT-Engineer-App/pdf-ocr-extractor.git
cd pdf-ocr-extractor
npm i
```

```sh
npm run dev
```

This will run a dev server with auto reloading and an instant preview.

## Requirements

- Node.js & npm - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
