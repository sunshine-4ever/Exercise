
import os
from PIL import Image

def Combine(sig_path):
    # 添加母图
    a0 = Image.open("C:/Users/acer/Desktop/0.jpg")
    # 添加子图
    a1 = Image.open(sig_path)#子图文件名
    # 获取图片的宽高
    a0_w, a0_h =a0.size#获取被放图片的大小（母图）
    a1_w,a1_h=a1.size#获取小图的大小（子图）
    
    #子图宽和高都不能超过母图，如果超过，将子图的尺度赋给母图，并将母图另一边等比例缩放
    if a1_w/a1_h>=26/18:
        a2_w=a1_w
        a2_h=18/26*a2_w
    else:
        a2_h=a1_h    
        a2_w=26/18*a2_h
           
    # 重新设置母图的尺寸
    a3=a0.resize((int(a2_w),int(a2_h)),Image.ANTIALIAS)
    w0,h0=a3.size
    # 设置子图的位置
    w = int((w0-a1_w) / 2)
    h = int((h0-a1_h) / 2)
    
    # 粘贴图片
    a3.paste(a1, (w, h), mask=None)
    return a3


#只需将图片文件夹路径粘贴到此处即可
path='C:/Users/acer/Desktop/2007'


# 创建整理后的图片位置文件夹
os.makedirs(path+'/new')
# 获得图片文件夹内每张图片，循环依次处理
names=os.listdir(path)
for item in names:
    # 获得图片路径并调用处理函数合成图片
    sig_path=path+'/'+item
    img_new=Combine(sig_path)
    # 保存图片
    save_path=path+'/new/'+item
    img_new.save(save_path)
    print(item)
print('done')
