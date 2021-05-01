# IMAGE-EDITOR
from tkinter import *
from PIL import ImageTk, Image, ImageFilter
from tkinter import filedialog
import tkinter.messagebox as tmg

rot = 1
flipp = 1


def harry(event):
    pass


def open_img():
    pass


def remove():
    pass


def rotate():
    pass


class imageedi:
    def __init__(self):
        self.root = Tk()
        self.root.title('IMAGE EDITOR')
        self.root.geometry("1240x660")
        self.root.iconbitmap('Prey-logo-1-icon.ico')
        self.root.resizable(width=False, height=False)
        self.imgg = Image.open("INV_Photo_Editing_Feature-810.jpg")
        self.img = self.imgg.resize((1240, 660))
        self.img = ImageTk.PhotoImage(self.img)
        self.my_canvas = Canvas(self.root)
        self.my_canvas.place(x=0, y=0, relheight=1, relwidth=1)
        self.my_canvas.create_image(0, 0, image=self.img, anchor="nw")
        self.b1 = Button(self.root, text='START EXPLORING', bg='red', command=self.mainpg, height=1, width=20,
                         font="Helvetica 16 bold")
        self.b1.place(x=800, y=200)
        self.root.bind('<Button-1>', harry)
        self.root.mainloop()

    def filt(self, filte):
        global saveimg
        self.fimg = Image.open(self.open_image(1))
        self.fimg = self.fimg.resize((500, 500))
        self.fimg = self.fimg.filter(filte)
        saveimg = self.fimg.copy()
        self.fimg = ImageTk.PhotoImage(self.fimg)
        self.panel = Label(self.root, image=self.fimg)
        self.panel.image = self.fimg
        self.panel.place(x=700, y=50)

    def orgim(self):
        global saveimg
        self.orgi = Image.open(self.filex)
        self.orgi = self.orgi.resize((500, 500))
        saveimg = self.orgi.copy()
        self.orgi = ImageTk.PhotoImage(self.orgi)
        self.panel = Label(self.root, image=self.orgi)
        self.panel.image = self.orgi
        self.panel.place(x=700, y=50)

    def mainpg(self, main=0):
        global saveimg
        self.my_canvas.delete("all")
        self.b1.place_forget()
        self.imgg1 = Image.open('projpyim2.jpg')
        self.img1 = self.imgg1.resize((1240, 660), Image.ANTIALIAS)
        self.img1 = ImageTk.PhotoImage(self.img1)
        self.my_canvas = Canvas(self.root)
        self.my_canvas.place(x=0, y=0, relheight=1, relwidth=1)
        self.my_canvas.create_image(0, 0, image=self.img1, anchor="nw")
        self.my_canvas.create_rectangle(700, 50, 1200, 550, fill="")
        self.my_canvas.place()
        if (main == 0):
            self.uploadbut = Button(self.root, text='UPLOAD IMAGE', command=self.open_image, height=2, width=12,
                                    font="Helvetica 10 bold")
            self.uploadbut.place(x=926, y=264)
        elif (main == 1):
            self.open_image(2)
        elif (main == 2):
            self.uploadbut = Button(self.root, text='UPLOAD IMAGE', command=self.open_image, height=2, width=12,
                                    font="Helvetica 10 bold")
            self.uploadbut.place(x=926, y=264)
            saveimg = 0
        self.f1 = Image.open('filterimageicon.jpg')
        self.f1 = self.f1.resize((85, 85), Image.ANTIALIAS)
        self.f1 = ImageTk.PhotoImage(self.f1)
        self.filterbut = Button(self.root, text='FILTER', image=self.f1, command=self.filpage, height=100, width=90,
                                font="Helvetica 10 bold", compound=TOP)
        self.filterbut.place(x=400, y=300)
        self.f2 = Image.open('rotateimageicon.jpg')
        self.f2 = self.f2.resize((85, 85), Image.ANTIALIAS)
        self.f2 = ImageTk.PhotoImage(self.f2)
        self.rotatebut = Button(self.root, text='ROTATE', image=self.f2, command=self.rotate, height=100, width=90,
                                font="Helvetica 10 bold", compound=TOP)
        self.rotatebut.place(x=400, y=118)
        self.f3 = Image.open('flipimageicon.png')
        self.f3 = self.f3.resize((85, 85), Image.ANTIALIAS)
        self.f3 = ImageTk.PhotoImage(self.f3)
        self.flipbut = Button(self.root, text='FLIP', image=self.f3, command=self.fliip, height=100, width=90,
                              font="Helvetica 10 bold", compound=TOP)
        self.flipbut.place(x=200, y=118)
        self.f4 = Image.open('saveimage.png')
        self.f4 = self.f4.resize((85, 85), Image.ANTIALIAS)
        self.f4 = ImageTk.PhotoImage(self.f4)
        self.savebut = Button(self.root, text='SAVE', image=self.f4, command=self.save, height=100, width=90,
                              font="Helvetica 10 bold", compound=TOP)
        self.savebut.place(x=200, y=300)
        self.removebut = Button(self.root, text='REMOVE IMAGE', command=lambda: self.mainpg(2), height=1, width=12,
                                font="Helvetica 10 bold", compound=TOP)
        self.removebut.place(x=1000, y=600)

    def filpage(self):
        try:
            self.v = Image.open(self.open_image(1))
            self.v = self.v.resize((90, 90), Image.ANTIALIAS)
            self.orgimg = ImageTk.PhotoImage(self.v)
            self.orgbut = Button(self.root, text="ORIGINAL", image=self.orgimg, command=self.orgim, height=110,
                                 width=100, compound=TOP)
            self.orgbut.place(x=70, y=130)
            self.blurimg = self.v.filter(ImageFilter.BLUR)
            self.blurimg = ImageTk.PhotoImage(self.blurimg)
            self.my_canvas.delete("all")
            self.uploadbut.place_forget()
            self.savebut.place_forget()
            self.filterbut.place_forget()
            self.rotatebut.place_forget()
            self.flipbut.place_forget()
            self.removebut.place_forget()
            self.blurbut = Button(self.root, text="BLUR", image=self.blurimg,
                                  command=lambda: self.filt(ImageFilter.BLUR), height=110, width=100, compound=TOP)
            self.blurbut.place(x=180, y=130)
            self.contourimg = self.v.filter(ImageFilter.CONTOUR)
            self.contourimg = ImageTk.PhotoImage(self.contourimg)
            self.contourbut = Button(self.root, text="CONTOUR", image=self.contourimg,
                                     command=lambda: self.filt(ImageFilter.CONTOUR), height=110, width=100,
                                     compound=TOP)
            self.contourbut.place(x=290, y=130)
            self.detailimg = self.v.filter(ImageFilter.DETAIL)
            self.detailimg = ImageTk.PhotoImage(self.detailimg)
            self.detailbut = Button(self.root, text="DETAIL", image=self.detailimg,
                                    command=lambda: self.filt(ImageFilter.DETAIL), height=110, width=100, compound=TOP)
            self.detailbut.place(x=400, y=130)
            self.edgeeimg = self.v.filter(ImageFilter.EDGE_ENHANCE)
            self.edgeeimg = ImageTk.PhotoImage(self.edgeeimg)
            self.edgeebut = Button(self.root, text="EDGE_ENHANCE", image=self.edgeeimg,
                                   command=lambda: self.filt(ImageFilter.EDGE_ENHANCE), height=110, width=100,
                                   compound=TOP)
            self.edgeebut.place(x=510, y=130)
            self.edgeemimg = self.v.filter(ImageFilter.EDGE_ENHANCE_MORE)
            self.edgeemimg = ImageTk.PhotoImage(self.edgeemimg)
            self.edgeembut = Button(self.root, text="M_EDGE_ENHANCE", image=self.edgeemimg,
                                    command=lambda: self.filt(ImageFilter.EDGE_ENHANCE_MORE), height=110, width=100,
                                    compound=TOP)
            self.edgeembut.place(x=70, y=250)
            self.embossimg = self.v.filter(ImageFilter.EMBOSS)
            self.embossimg = ImageTk.PhotoImage(self.embossimg)
            self.embossbut = Button(self.root, text="CONTOUR", image=self.embossimg,
                                    command=lambda: self.filt(ImageFilter.EMBOSS), height=110, width=100, compound=TOP)
            self.embossbut.place(x=180, y=250)
            self.fedgeimg = self.v.filter(ImageFilter.FIND_EDGES)
            self.fedgeimg = ImageTk.PhotoImage(self.fedgeimg)
            self.fedgebut = Button(self.root, text="FIND_EDGES", image=self.fedgeimg,
                                   command=lambda: self.filt(ImageFilter.FIND_EDGES), height=110, width=100,
                                   compound=TOP)
            self.fedgebut.place(x=290, y=250)
            self.smoothimg = self.v.filter(ImageFilter.SMOOTH)
            self.smoothimg = ImageTk.PhotoImage(self.smoothimg)
            self.smoothbut = Button(self.root, text="SMOOTH", image=self.smoothimg,
                                    command=lambda: self.filt(ImageFilter.SMOOTH), height=110, width=100, compound=TOP)
            self.smoothbut.place(x=400, y=250)
            self.smoothmimg = self.v.filter(ImageFilter.SMOOTH_MORE)
            self.smoothmimg = ImageTk.PhotoImage(self.smoothmimg)
            self.smoothmbut = Button(self.root, text="M_SMOOTH", image=self.smoothmimg,
                                     command=lambda: self.filt(ImageFilter.SMOOTH_MORE), height=110, width=100,
                                     compound=TOP)
            self.smoothmbut.place(x=510, y=250)
            self.sharpenimg = self.v.filter(ImageFilter.SHARPEN)
            self.sharpenimg = ImageTk.PhotoImage(self.sharpenimg)
            self.sharpenbut = Button(self.root, text="SHARPEN", image=self.smoothmimg,
                                     command=lambda: self.filt(ImageFilter.SHARPEN), height=110, width=100,
                                     compound=TOP)
            self.sharpenbut.place(x=70, y=370)
            self.backimag = Image.open('backimgicon.png')
            self.backimg = self.backimag.resize((60, 60), Image.ANTIALIAS)
            self.backimg = ImageTk.PhotoImage(self.backimg)
            backbut = Button(self.root, text="BACK", image=self.backimg, command=lambda: self.mainpg(1), height=80,
                             width=80, compound=TOP)
            backbut.place(x=0, y=0)
        except:
            tmg.showinfo("Error", "PLEASE UPLOAD IMAGE TO EDIT")

    def open_image(self, tval=0):
        try:
            if (tval == 0):
                global saveimg
                self.filex = self.openfilename()
                self.img2 = Image.open(self.filex)
                self.img2 = self.img2.resize((500, 500))
                saveimg = self.img2.copy()
                self.img2 = ImageTk.PhotoImage(self.img2)
                self.panel = Label(self.root, image=self.img2)
                self.panel.image = self.img2
                self.panel.place(x=700, y=50)
            elif (tval == 1):
                return self.filex
            elif (tval == 2):
                self.img2 = saveimg.resize((500, 500))
                self.img2 = ImageTk.PhotoImage(self.img2)
                self.panel = Label(self.root, image=self.img2)
                self.panel.image = self.img2
                self.panel.place(x=700, y=50)
        except:
            pass

    def modifyiedimg(self, vmg, val):
        if (val == 0):
            pass
        elif (val == 1):
            pass

    def save(self):
        try:
            global saveimg
            savefile = filedialog.asksaveasfile(defaultextension=".jpg")
            saveimg.save(savefile)
        except:
            tmg.showinfo("Error", "PLEASE UPLOAD IMAGE TO EDIT")

    def fliip(self):
        try:
            global saveimg
            global flipp
            self.flip = saveimg.resize((500, 500))
            if (flipp % 3 == 0):
                saveimg = self.flip.copy()
            elif (flipp % 2 == 0):
                self.flip = self.flip.transpose(Image.FLIP_TOP_BOTTOM)
                saveimg = self.flip.copy()
            else:
                self.flip = self.flip.transpose(Image.FLIP_LEFT_RIGHT)
                saveimg = self.flip.copy()
            flipp = flipp + 1
            self.flip = ImageTk.PhotoImage(self.flip)
            self.panel = Label(self.root, image=self.flip)
            self.panel.image = self.flip
            self.panel.place(x=700, y=50)
        except:
            tmg.showinfo("Error", "PLEASE UPLOAD IMAGE TO EDIT")

    def rotate(self):
        try:
            global saveimg
            self.rotat = saveimg.resize((500, 500))
            self.rotat = self.rotat.rotate(90)
            saveimg = self.rotat.copy()
            self.rotat = ImageTk.PhotoImage(self.rotat)
            self.panel = Label(self.root, image=self.rotat)
            self.panel.image = self.rotat
            self.panel.place(x=700, y=50)
        except:
            tmg.showinfo("Error", "PLEASE UPLOAD IMAGE TO EDIT")

    def crop(self):
        pass

    def openfilename(self):
        self.filename = filedialog.askopenfilename(title='pen')
        return self.filename


if __name__ == '__main__':
    gu = imageedi()
