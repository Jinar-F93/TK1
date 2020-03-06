from tkinter import *
from tkinter import ttk
from dataa import Database
from tkinter import messagebox
dataa = Database("book2.db")

win = Tk()
win.title('Final project')
win.geometry('500x300')


def vieww():
    list1.delete(0,'end')
    for result in dataa.show():
        list1.insert('end',result)


def add():
    #if Name_text.get()=='' or Last_name_text.get()=='' or Age_text.get()=='' or Id_information_text.get()=='':
        #messagebox.showwarning('empty','please fill all the places')

    dataa.insert(Name_text.get(), Last_name_text.get(), Age_text.get(), Id_information_text.get())
    list1.delete(0,'end')
    list1.insert('end', (Name_text.get(), Last_name_text.get(), Age_text.get(), Id_information_text.get()))
    clear_display()

def select_item(event):
    try:
        global selected_item
        index = list1.curselection()[0]
        selected_item = list1.get(index)

        en1.delete(0,'end')
        en1.insert('end',selected_item[1])
        en2.delete(0, 'end')
        en2.insert('end', selected_item[2])
        en3.delete(0, 'end')
        en3.insert('end', selected_item[3])
        en4.delete(0, 'end')
        en4.insert('end', selected_item[4])
    except IndexError:
        pass

def up():
    dataa.update(selected_item[0],Name_text.get(), Last_name_text.get(), Age_text.get(), Id_information_text.get())
    vieww()

def clear_display():
    en1.delete(0,'end')
    en2.delete(0,'end')
    en3.delete(0,'end')
    en4.delete(0,'end')

def cl():
    dataa.remove(selected_item[0])



Name_text = StringVar()
en1 = ttk.Entry(win,textvariable = Name_text,width = 20)
en1.place(relx = 0.05, rely = 0.05,x = 30 ,anchor = 'nw')
lb1 = ttk.Label(win, text = 'Name',font = ('Arial',8,'bold'))
lb1.place(relx = 0.05, rely = 0.05 ,x = -10,anchor = 'nw')


Last_name_text = StringVar()
en2 = ttk.Entry(win,textvariable = Last_name_text,width = 20)
en2.place(relx = 0.5 ,rely = 0.05, x = -15,anchor = 'nw')
lb2 = ttk.Label(win , text = 'Family',font = ('Arial',8,'bold'))
lb2.place(relx = 0.5 ,rely = 0.05, x = -60,anchor = 'nw')


Id_information_text = StringVar()
en3 = ttk.Entry(win ,textvariable = Id_information_text, width = 20)
en3.place(relx = 0.05 ,rely = 0.05,x = 30,y = 50, anchor = 'nw')
lb3 = ttk.Label(win,text = 'Id',font = ('mitra',8,'bold'))
lb3.place(relx = 0.05 ,rely = 0.05,x = -10,y = 50, anchor = 'nw')


Age_text = StringVar()
en4 = ttk.Entry(win,textvariable = Age_text,width = 20)
en4.place(relx = 0.5 ,rely = 0.05, x = -15,y = 50,anchor = 'nw')
lb4 = ttk.Label(win , text = 'Age',font = ('mitra',8,'bold'))
lb4.place(relx = 0.5 ,rely = 0.05, x = -60,y = 50,anchor = 'nw')

list1 = Listbox(win, width=35, height=10 , border = 2)
list1.place(x=50, y=120)

sc = Scrollbar(win )
sc.pack(side = 'right', fill = 'y')

list1.configure(yscrollcommand=sc.set)
sc.config(command=list1.yview)

list1.bind("<<Listbox select>>", select_item)


but1 = ttk.Button(win,text = 'Show',command= vieww)
but1.place(relx = 0.5 ,rely = 0.05, x = 150,y = 100,anchor = 'nw')

but2 = ttk.Button(win, text = 'Insert',command = add)
but2.place(relx = 0.5 ,rely = 0.05, x = 150,y = 150,anchor = 'nw')

but3 = ttk.Button(win, text = 'Update',command = up)
but3.place(relx = 0.5 ,rely = 0.05, x = 150,y = 200,anchor = 'nw')

but4 = ttk.Button(win, text = 'Clear',command = cl)
but4.place(relx = 0.5 ,rely = 0.05, x = 150,y = 250,anchor = 'nw')



win.mainloop()
