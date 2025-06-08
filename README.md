# Tkinteralfabeto
import tkinter as tk
from tkinter import messagebox

alfabeto = ['a', 'b', 'c', 'd', 'e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']

def criptografa(palavrinha, chave):
    criptograf = []
    for letra in palavrinha:
        if letra in alfabeto:
            i = alfabeto.index(letra)
            i_novinho = (i + chave) % 26
            criptograf.append(alfabeto[i_novinho])
        else:
            criptograf.append(letra) 
    return ''.join(criptograf)

def descriptografa(palavrinha, chave):
    descriptograf = []
    for letra in palavrinha:
        if letra in alfabeto:
            i = alfabeto.index(letra)
            i_novinho = (i - chave) % 26
            descriptograf.append(alfabeto[i_novinho])
        else:
            descriptograf.append(letra)
    return ''.join(descriptograf)

def executar():
    palavra = entrada_palavra.get().lower()
    try:
        chave = int(entrada_chave.get())
    except ValueError:
        messagebox.showerror("Erro", "A chave deve ser um número inteiro.")
        return

    if escolha.get() == 1:
        resultado = criptografa(palavra, chave)
        resultado_label.config(text=f"Criptografada: {resultado}")
    elif escolha.get() == 2:
        resultado = descriptografa(palavra, chave)
        resultado_label.config(text=f"Descriptografada: {resultado}")
    else:
        messagebox.showwarning("Opa", "Escolha uma opção válida.")


#tk
janela = tk.Tk()
janela.title("Criptografia")


escolha = tk.IntVar()
tk.Label(janela, text="Escolha a operação:").pack()
tk.Radiobutton(janela, text="Criptografar", variable=escolha, value=1).pack()
tk.Radiobutton(janela, text="Descriptografar", variable=escolha, value=2).pack()


tk.Label(janela, text="Digite a palavra:").pack()
entrada_palavra = tk.Entry(janela)
entrada_palavra.pack()


tk.Label(janela, text="Digite a chave (número):").pack()
entrada_chave = tk.Entry(janela)
entrada_chave.pack()


tk.Button(janela, text="Executar", command=executar).pack(pady=10)


resultado_label = tk.Label(janela, text="")
resultado_label.pack()

janela.mainloop()

