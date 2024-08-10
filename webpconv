import os
import tkinter as tk
from tkinter import Label
from PIL import Image
from tkinterdnd2 import DND_FILES, TkinterDnD

class ImageConverterGUI(TkinterDnD.Tk):
    def __init__(self):
        super().__init__()

        self.title("Image to WebP Converter")
        self.geometry("400x200")
        self.configure(bg="#f0f0f0")

        self.label = Label(self, text="Drag and Drop Image Files Here", bg="#f0f0f0")
        self.label.pack(expand=1, fill='both')

        # Enable dropping files onto the label
        self.label.drop_target_register(DND_FILES)
        self.label.dnd_bind('<<Drop>>', self.handle_drop)

    def handle_drop(self, event):
        files = self.split_files(event.data)
        for file_path in files:
            self.convert_to_webp(file_path)

    def split_files(self, file_list):
        # Handle multiple files dropped at once
        if self.tk.splitlist(file_list):
            return [f.strip('{').strip('}') for f in self.tk.splitlist(file_list)]
        else:
            return [file_list]

    def convert_to_webp(self, file_path):
        try:
            img = Image.open(file_path)
            base_name = os.path.basename(file_path)
            name_without_ext = os.path.splitext(base_name)[0]
            save_path = os.path.join(os.path.dirname(file_path), f"{name_without_ext}.webp")
            img.save(save_path, 'WEBP')
            self.label.config(text=f"Converted and saved: {save_path}")
        except Exception as e:
            self.label.config(text=f"Error converting {file_path}: {str(e)}")

if __name__ == "__main__":
    app = ImageConverterGUI()
    app.mainloop()
