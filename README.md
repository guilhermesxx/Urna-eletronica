import tkinter as tk
import winsound  

class UrnaEletronica:
    def __init__(self, root):
        self.root = root
        self.root.title("Urna Eletrônica")
        self.root.geometry("300x300")
        self.root.configure(bg='black')

       
        self.votos = {'Chapa do Guimarães': 0, 'SO NO PELO FC': 0, 'PGG': 0}

        
        tk.Label(root, text="Escolha uma chapa para votar:", bg='black', fg='white').pack(pady=10)

       
        self.botao_chapa1 = tk.Button(root, text="Chapa do Guimarães", command=lambda: self.votar('Chapa do Guimarães'), bg='white', fg='black')
        self.botao_chapa1.pack(pady=5)

        self.botao_chapa2 = tk.Button(root, text="SO NO PELO FC", command=lambda: self.votar('SO NO PELO FC'), bg='white', fg='black')
        self.botao_chapa2.pack(pady=5)

        self.botao_chapa3 = tk.Button(root, text="PGG", command=lambda: self.votar('PGG'), bg='white', fg='black')
        self.botao_chapa3.pack(pady=5)

        self.botao_resultado = tk.Button(root, text="Ver Resultado", command=self.mostrar_resultado, bg='white', fg='black')
        self.botao_resultado.pack(pady=10)

        self.botao_sair = tk.Button(root, text="Sair", command=root.quit, bg='white', fg='black')
        self.botao_sair.pack(pady=10)

    def votar(self, chapa):
        self.votos[chapa] += 1
        winsound.Beep(1000, 500) 

    def mostrar_resultado(self):
        total_votos = sum(self.votos.values())
        resultado = "\n".join(f"{chapa}: {voto} votos" for chapa, voto in self.votos.items())
        resultado += "\n\nTotal de votos: " + str(total_votos)
        
        janela_resultado = tk.Toplevel(self.root)
        janela_resultado.title("Resultado")
        janela_resultado.configure(bg='black')
        tk.Label(janela_resultado, text=resultado, bg='black', fg='white').pack(padx=10, pady=10)

root = tk.Tk()
app = UrnaEletronica(root)
root.mainloop()
