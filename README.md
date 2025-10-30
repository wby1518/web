import tkinter as tk
import random
import threading
import time

def show_warm_tip():
    # 窗口大小
    window_width = 300
    window_height = 150
    
    # 获取屏幕尺寸，避免窗口超出屏幕
    root = tk.Tk()  # 临时获取屏幕尺寸用，之后会销毁
    screen_width = root.winfo_screenwidth()
    screen_height = root.winfo_screenheight()
    root.destroy()  # 销毁临时主窗口
    
    # 随机位置（确保窗口完全显示）
    x = random.randint(0, screen_width - window_width)
    y = random.randint(0, screen_height - window_height)
    
    # 创建子窗口（多线程中用Toplevel而非Tk）
    window = tk.Toplevel()
    window.title('温馨提示')
    window.geometry(f"{window_width}x{window_height}+{x}+{y}")
    
    # 提示文字
    tips = ['保持微笑', '顺顺利利', '别熬夜', '天冷了，多穿衣服', '多吃水果'，'想你了'，'烦恼消失','保持好心情','期待下一次见面','每天都要元气满满','别喝矿泉水了，用保温杯喝热水']
    tip = random.choice(tips)
    
    # 背景颜色（修复中文逗号）
    bg_colors = ['lightpink', 'skyblue', 'lightgreen', 'lavender', 'lightyellow','plum','coral','bisque','aquamarine','mistyrose','honeydew','lavenderblush','oldlace']
    bg = random.choice(bg_colors)
    
    # 创建标签（修复缺少的逗号）
    tk.Label(
        window,
        text=tip,
        bg=bg,
        font=('微软雅黑', 16),  # 这里添加了逗号
        width=30,
        height=3  
    ).pack()
    
    # 窗口置顶
    window.attributes('-topmost', True)
    window.mainloop()

if __name__ == "__main__":
    # 主线程创建一个主窗口（Tkinter要求必须有一个主窗口）
    main_window = tk.Tk()
    main_window.withdraw()  # 隐藏主窗口
    
    # 调整窗口数量（300个太多，改为20个测试）
    threads = []
    for i in range(20):
        t = threading.Thread(target=show_warm_tip)
        threads.append(t)
        t.start()
        time.sleep(0.05)  # 延长间隔，减少系统压力
    
    main_window.mainloop()
