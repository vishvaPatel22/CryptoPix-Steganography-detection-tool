import tkinter as tk 
from tkinter import filedialog, messagebox
from PIL import Image
import stepic

#Function for hide message on image
def encode():
    path = filedialog.askopenfilename(filetypes=[("Image files", "*.png")])

    if not path:
        return
    Img=Image.open(path)
    secretMessage="Attack at 8 p.m"
    steImg=stepic.encode(Img,secretMessage.encode())
    steImg.save("img.png")

    tk.messagebox.showinfo("Message","succesfully saved encoded Image.")
 
#Function for reveal message in image       
def decode():
    path = filedialog.askopenfilename(filetypes=[("Image files", "*.png")])
    if not path:
        return
  
    Img=Image.open(path)
    secretMessage=stepic.decode(Img).decode()
    tk.messagebox.showinfo("Message",f"secret message is: {secretMessage}")
    
#GUI 
root=tk.Tk()
root.title('CryptoPix')
root.geometry("200x200")               
root.configure(bg="#eed9b5")           

label=tk.Label(root,text='Welcome to CryptoPix !!',font=("Helvetica", 16, "bold"),
    fg="#4b1e00",
    bg="#d7cc88")
label.pack(pady=20)
btn1=tk.Button(root,text="Hide a message on Image",font=("Arial", 12),
    bg="#4b1e00",
    fg="#d7cc88",command=encode)
btn1.pack(pady=10, ipadx=10, ipady=15)

btn2=tk.Button(root,text="Reveal a message on Image",font=("Arial", 12),
    bg="#4b1e00",
    fg="#d7cc88",command=decode)
btn2.pack(pady=10, ipadx=10, ipady=15)

root.mainloop()
