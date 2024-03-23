from PIL import Image,ImageFilter,ImageEnhance
# with Image.open("1a1673a4765e40156b02a9f0f5e3b49f.webp")as file:
#     #file.show()
#     print("Розмір фото:",file.size)
#     print("Формат фото:",file.format)
#     print("Колірна модель:",file.mode)
#     gray=file.convert("L")
#     gray.save("gray.webp")
#     blured=file.filter(ImageFilter.BLUR)
#     blured.save("blured.webp")
#     up=file.transpose(Image.ROTATE_180)
#     up.save("up.webp")
#     mirror=file.transpose(Image.FLIP_LEFT_RIGHT)
#     mirror.save("mirror.webp")
#     pic_contrast = ImageEnhance.Contrast(file)
#     pic_contrast = pic_contrast.enhance (1.5)
#     pic_contrast.save("pic_contrast.webp")
class ImageEditor:
    def __init__(self,name):
        self.name=name
        self.original=""
        self.files=[]
        self.counter=1
    def open(self):
        try:
            self.original=Image.open(self.name)
            self.files.append(self.original)
        except:
            print("Назва вказана не вірно!")
    def do_left(self):
        left=self.original.transpose(Image.ROTATE_90)
        self.files.append(left)
        new=self.name.split(".")
        left.save(new[0]+str(self.counter)+"."+new[1])
        self.counter+=1

    def do_cropped(self):
        box=(550,750,50,50)
        cropped=self.original.crop(box)
        self.files.append(cropped)
        new=self.name.split(".")
        cropped.save(new[0]+str(self.counter)+"."+new[1])
        self.counter+=1


image=ImageEditor("1a1673a4765e40156b02a9f0f5e3b49f.webp")
image.open()
image.do_left()
image.do_cropped()
for file in image.files:
    file.show()
