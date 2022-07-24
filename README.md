from tkinter import *
from tkinter import messagebox
import mysql.connector
from datetime import date

root = Tk()
root.title("Library Management system")
root.geometry("600x600+800+800")

bookdetails = Button(root, text="Book details", font=("arial", 8, 'bold'), width = 12, command=member_add)
bookdetails.place(x=300, y=50)

memberdetails = Button(root, text="Member details", font=("arial", 8, 'bold'), width = 12, command=member_view)
bookdetails.place(x=300, y=100)

booksearch = Button(root, text="Search Book", font=("arial", 8, 'bold'), width = 12, command=member_view)
bookdetails.place(x=300, y=150)

bookissue = Button(root, text="Issue Book", font=("arial", 8, 'bold'), width = 12, command=member_update)
bookdetails.place(x=300, y=200)

bookreturn = Button(root, text="Return Book", font=("arial", 8, 'bold'), width = 12, command=member_delete)
bookdetails.place(x=300, y=250)

transaction = Button(root, text="Transaction", font=("arial", 8, 'bold'), width = 12, command=member_delete)
bookdetails.place(x=300, y=300)



class book_deatils():

new_root= Toplevel(root)
new_root.geometry("700x250")
new_root.title("NEW WINDOW")

#Hide the Main Window
#win.withdraw()

def book_add():
    bookid = b_id.get()
    title = b_title.get()
    author = b_author.get()
    status = b_status.get()

    if(bookid=="" or title=="" or author=="" or status==""):
        messagebox.showinfo("Add status", "All Field are required")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("insert into book(bookID,title,authors,status)values(%s,%s,%s,%s)", [b_id.get(), b_title.get(), b_author.get(), b_status.get()]) 
        con.commit()

        b_id.delete(0, 'end')
        b_title.delete(0, 'end')
        b_author.delete(0, 'end')
        b_status.delete(0, 'end')
        messagebox.showinfo("Insert status", "Book Added successfully")
        con.close()



def book_view():
    if(b_id.get() == ""):
        messagebox.showinfo("Fetch status", "ID is compolsary for fetch")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("select * from book where bookID= %s",[b_id.get()])
        rows = cursor.fetchall()

        b_id.delete(0, 'end')
        b_title.delete(0, 'end')
        b_author.delete(0, 'end')
        b_status.delete(0, 'end')

        for row in rows:
            b_title.insert(0, row[1])
            b_author.insert(0, row[2])
            b_status.insert(0, row[6])
        con.close()


def book_update():
    bookid = b_id.get()
    title = b_title.get()
    author = b_author.get()
    status = b_status.get()

    if(bookid=="" or title=="" or author=="" or status==""):
        messagebox.showinfo("Update status", "All Field are required")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("update member set(bookID,title,author,status)values(%s,%s,%s,%s)", [b_id.get(), b_title.get(), b_author.get(), b_status.get()])
        con.commit()

        b_id.delete(0, 'end')
        b_title.delete(0, 'end')
        b_author.delete(0, 'end')
        b_status.delete(0, 'end')
        messagebox.showinfo("Update status", "Book Updateed successfully")
        con.close()



def book_delete():   
    if(b_id.get() == ""):
        messagebox.showinfo("Delete status", "ID is compolsary for delete")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("delete from book where bookID= %s",[b_id.get()])
        con.commit()

        b_id.delete(0, 'end')
        b_title.delete(0, 'end')
        b_author.delete(0, 'end')
        b_status.delete(0, 'end')
        messagebox.showinfo("Delete status", "Book Deleted successfully")
        con.close()  



bookid = Label(root, text='Enter Book ID', font=('bold', 10))
bookid.place(x=20, y=30)

title = Label(root, text='Enter Book Title', font=('bold', 10))
title.place(x=20, y=60)

author = Label(root, text='Enter Author Name', font=('bold', 10))
author.place(x=20, y=90)

status = Label(root, text='Status (Avai/issued)', font=('bold', 10))
status.place(x=20, y=120)

b_id = Entry()
b_id.place(x=160, y=30)

b_title = Entry()
b_title.place(x=160, y=60)

b_author = Entry()
b_author.place(x=160, y=90)

b_status = Entry()
b_status.place(x=160, y=120)

bookddd = Button(root, text="Add Book", font=("arial", 8, 'bold'), width = 12, command=book_add)
bookview = Button(root, text="View Book", font=("arial", 8, 'bold'), width = 12, command=book_view)
bookupdate = Button(root, text="Update Book", font=("arial", 8, 'bold'), width = 12, command=book_update)
bookdelete = Button(root, text="Delete Book", font=("arial", 8, 'bold'), width = 12, command=book_delete)


bookddd.place(x=300, y=70)
bookview.place(x=400, y=70)
bookupdate.place(x=500, y=70)
bookdelete.place(x=600, y=70)


def member_add():
    idnumber = m_id.get()
    name = m_name.get()
    phone = m_phone.get()
    email = m_email.get()

    if(idnumber=="" or name=="" or phone=="" or email==""):
        messagebox.showinfo("Add status", "All Field are required")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("insert into member(memberID,Name,Phone,Email)values(%s,%s,%s,%s)", [m_id.get(), m_name.get(),m_phone.get(),m_email.get()]) 
        con.commit()

        m_id.delete(0, 'end')
        m_name.delete(0, 'end')
        m_phone.delete(0, 'end')
        m_email.delete(0, 'end')
        messagebox.showinfo("Insert status", "Member Added successfully")
        con.close()



def member_view():
    if(m_id.get() == ""):
        messagebox.showinfo("Fetch status", "ID is compolsary for fetch")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("select * from member where memberID= %s",[m_id.get()])
        rows = cursor.fetchall()

        m_id.delete(0, 'end')
        m_name.delete(0, 'end')
        m_phone.delete(0, 'end')
        m_email.delete(0, 'end')

        for row in rows:
            m_name.insert(0, row[1])
            m_phone.insert(0, row[2])
            m_email.insert(0, row[3])
        con.close()


def member_update():
    idnumber = m_id.get()
    name = m_name.get()
    phone = m_phone.get()
    email = m_email.get()

    if(idnumber=="" or name=="" or phone=="" or email==""):
        messagebox.showinfo("Update status", "All Field are required")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("update member set(memberID,Name,Phone,Email)values(%s,%s,%s,%s)", [m_id.get(), m_name.get(),m_phone.get(),m_email.get()])
        con.commit()

        m_id.delete(0, 'end')
        m_name.delete(0, 'end')
        m_phone.delete(0, 'end')
        m_email.delete(0, 'end')
        messagebox.showinfo("Update status", "Member Updateed successfully")
        con.close()



def member_delete():   
    if(m_id.get() == ""):
        messagebox.showinfo("Delete status", "ID is compolsary for delete")
    else:
        con = mysql.connector.connect(host='localhost', password='Aaru@19041997', user='root', database='library')
        cursor = con.cursor()
        cursor.execute("delete from member where memberID= %s",[m_id.get()])
        con.commit()

        m_id.delete(0, 'end')
        m_name.delete(0, 'end')
        m_phone.delete(0, 'end')
        m_email.delete(0, 'end')
        messagebox.showinfo("Delete status", "Member Deleted successfully")
        con.close()  



idnumber = Label(root, text='Enter Member ID', font=('bold', 10))
idnumber.place(x=20, y=180)

name = Label(root, text='Enter Member Name', font=('bold', 10))
name.place(x=20, y=210)

phone = Label(root, text='Enter Member Phone', font=('bold', 10))
phone.place(x=20, y=240)

email = Label(root, text='Enter Member Email ID', font=('bold', 10))
email.place(x=20, y=270)

m_id = Entry()
m_id.place(x=160, y=180)

m_name = Entry()
m_name.place(x=160, y=210)

m_phone = Entry()
m_phone.place(x=160, y=240)

m_email = Entry()
m_email.place(x=160, y=270)


memberddd = Button(root, text="Add Member", font=("arial", 8, 'bold'), width = 12, command=member_add)
memberview = Button(root, text="View Member", font=("arial", 8, 'bold'), width = 12, command=member_view)
memeberupdate = Button(root, text="Update Member", font=("arial", 8, 'bold'), width = 12, command=member_update)
memeberdelete = Button(root, text="Delete Member", font=("arial", 8, 'bold'), width = 12, command=member_delete)


memberddd.place(x=300, y=220)
memberview.place(x=400, y=220)
memeberupdate.place(x=500, y=220)
memeberdelete.place(x=600, y=220)



root.mainloop()
