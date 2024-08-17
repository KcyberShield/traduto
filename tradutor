import tkinter as tk
from tkinter import ttk
from googletrans import LANGUAGES, Translator

class TranslatorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Translator App")
        self.root.configure(bg='#263238')  # Define o fundo da janela como uma tonalidade de azul escuro

        # Estilo para botões e labels
        self.style = ttk.Style()
        self.style.configure('TButton', foreground='white', background='#4CAF50')
        self.style.configure('TLabel', foreground='#2196F3', background='#263238')

        # Interface gráfica
        self.label_input = ttk.Label(self.root, text="Digite o texto:", style='TLabel')
        self.label_input.grid(row=0, column=0, padx=10, pady=10, sticky=tk.W)

        self.text_input = tk.Text(self.root, height=5, width=50, wrap=tk.WORD, fg='#2196F3')  # Define o texto como azul
        self.text_input.grid(row=1, column=0, columnspan=3, padx=10, pady=10)

        self.label_lang = ttk.Label(self.root, text="Idioma de destino:", style='TLabel')
        self.label_lang.grid(row=2, column=0, padx=10, pady=10, sticky=tk.W)

        # Adicionar botões para os principais idiomas
        self.lang_buttons_frame = tk.Frame(self.root, bg='#263238')
        self.lang_buttons_frame.grid(row=2, column=1, padx=10, pady=10, sticky=tk.W)

        self.main_languages = {
            "Português": "pt",
            "Inglês": "en",
            "Espanhol": "es",
            "Russo": "ru",
            "Japonês": "ja",
            "Chinês": "zh-cn"
        }

        self.selected_language = tk.StringVar()
        self.lang_buttons = {}
        for lang, code in self.main_languages.items():
            btn = tk.Button(self.lang_buttons_frame, text=lang, command=lambda l=lang: self.set_selected_language(l), fg='white', bg='#4CAF50')
            btn.pack(side=tk.LEFT, padx=5)
            self.lang_buttons[lang] = btn

        self.label_output = ttk.Label(self.root, text="Texto traduzido:", style='TLabel')
        self.label_output.grid(row=4, column=0, padx=10, pady=10, sticky=tk.W)

        self.translated_text = tk.Text(self.root, height=5, width=50, wrap=tk.WORD, fg='#2196F3')  # Define o texto como azul
        self.translated_text.grid(row=5, column=0, columnspan=3, padx=10, pady=10)

        # Carregar idioma salvo
        self.load_selected_language()

    def set_selected_language(self, language):
        self.selected_language.set(language)
        self.save_selected_language(language)

        for lang, btn in self.lang_buttons.items():
            if lang == language:
                btn.configure(bg='green')
            else:
                btn.configure(bg='#4CAF50')

        # Traduzir texto imediatamente após a seleção do idioma
        self.translate_text()

    def save_selected_language(self, language):
        with open('selected_language.txt', 'w') as f:
            f.write(language)

    def load_selected_language(self):
        try:
            with open('selected_language.txt', 'r') as f:
                language = f.read().strip()
                if language:
                    self.selected_language.set(language)
                    for lang, btn in self.lang_buttons.items():
                        if lang == language:
                            btn.configure(bg='green')
                        else:
                            btn.configure(bg='#4CAF50')
        except FileNotFoundError:
            pass

    def translate_text(self):
        text = self.text_input.get("1.0", tk.END).strip()
        selected_language = self.selected_language.get()

        if text and selected_language:
            dest_lang_code = self.main_languages[selected_language]
            translator = Translator()
            translated = translator.translate(text, dest=dest_lang_code)
            self.translated_text.delete("1.0", tk.END)
            self.translated_text.insert(tk.END, translated.text)

def main():
    root = tk.Tk()

    app = TranslatorApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()
