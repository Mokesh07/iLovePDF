import streamlit as st
from PyPDF2 import PdfMerger
import os


def merge_pdfs(pdf_files, output_path):
    with PdfMerger() as merger:
        for pdf in pdf_files:
            merger.append(pdf)
        merger.write(output_path)


def merge_pdfs_page():
    st.markdown("# Merge PDFs")
    st.sidebar.markdown("# Merge PDFs")
    uploaded_files = st.file_uploader("Upload PDF files", type=["pdf"], accept_multiple_files=True)

    if uploaded_files:
        file_names = [pdf.name for pdf in uploaded_files]
        ordered_file_names = st.multiselect("Reorder PDFs", file_names, default=file_names)
        ordered_files = [next(pdf for pdf in uploaded_files if pdf.name == name) for name in ordered_file_names]

        if st.button("Merge and Download"):
            merged_pdf_path = "merged_output.pdf"
            merge_pdfs(ordered_files, merged_pdf_path)

            with open(merged_pdf_path, "rb") as file:
                st.download_button(
                    label="Download Merged PDF",
                    data=file,
                    file_name="merged_output.pdf",
                    mime="application/pdf"
                )
            os.remove(merged_pdf_path)  # Cleanup after download


def split_pdfs_page():
    st.markdown("# Split PDFs")
    st.sidebar.markdown("# Split PDFs")
    st.write("Feature coming soon...")


def main():
    st.set_page_config(page_title="PDF Tools", layout="wide")
    st.sidebar.title("Navigation")
    with st.sidebar.expander("Tools", expanded=True):
        selected_page = st.radio("Select a tool", ["Merge PDFs", "Split PDFs"])

    if selected_page == "Merge PDFs":
        merge_pdfs_page()
    elif selected_page == "Split PDFs":
        split_pdfs_page()

main()
