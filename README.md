import tkinter as tk
from tkinter import filedialog

root = tk.Tk()
root.title("OCR控制界面")
root.geometry("1600x900+100+100")
root.config(bg="#F0F0F0")

def select_path(entry):
    path = filedialog.askdirectory() or filedialog.askopenfilename()
    if path:
        entry.delete(0, tk.END)
        entry.insert(0, path)

def add_language(interface):
    language_num = len(interface["languages"])
    if language_num < 10:
        language = {}
        language["language_label"] = tk.Label(interface["frame"], text="语种:", width=6, font=("Arial", 11), bg="#F0F0F0")
        language["language_label"].grid(row=language_num+1, column=6, sticky=tk.W)
        language["language"] = tk.StringVar(value="英语")
        language["language_option"] = tk.OptionMenu(interface["frame"], language["language"], "阿拉伯语", "丹麦语", "德语", "俄语", "法语", "芬兰语", "韩语", "荷兰语", "捷克语", "马来西亚语", "葡萄牙语", "日语", "瑞典语", "瑞士语", "斯洛伐克语", "泰语", "土耳其语", "西班牙语", "希腊语", "匈牙利语", "意大利语", "印地语", "印度尼西亚语", "英语", "中文繁体", "中文简体")
        language["language_option"].config(width=8, font=("Arial", 11), bg="#87CEFA")
        language["language_option"].grid(row=language_num+1, column=7, sticky=tk.W)
        language["blacklist_label"] = tk.Label(interface["frame"], text="黑名单:", width=6, font=("Arial", 11), bg="#F0F0F0")
        language["blacklist_label"].grid(row=language_num+1, column=8, sticky=tk.W)
        language["blacklist"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
        language["blacklist"].grid(row=language_num+1, column=9, sticky=tk.W)
        language["blacklist_button"] = tk.Button(interface["frame"], text="选择黑名单", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(language["blacklist"]))
        language["blacklist_button"].grid(row=language_num+1, column=10, sticky=tk.W)
        language["keyword_label"] = tk.Label(interface["frame"], text="关键词:", width=6, font=("Arial", 11), bg="#F0F0F0")
        language["keyword_label"].grid(row=language_num+1, column=11, sticky=tk.W)
        language["keyword"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
        language["keyword"].grid(row=language_num+1, column=12, sticky=tk.W)
        language["keyword_button"] = tk.Button(interface["frame"], text="选择关键词", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(language["keyword"]))
        language["keyword_button"].grid(row=language_num+1, column=13, sticky=tk.W)
        language["comment_label"] = tk.Label(interface["frame"], text="评论文本:", width=8, font=("Arial", 11), bg="#F0F0F0")
        language["comment_label"].grid(row=language_num+1, column=14, sticky=tk.W)
        language["comment"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
        language["comment"].grid(row=language_num+1, column=15, sticky=tk.W)
        language["comment_button"] = tk.Button(interface["frame"], text="选择评论文本", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(language["comment"]))
        language["comment_button"].grid(row=language_num+1, column=16, sticky=tk.W)
        language["delete_button"] = tk.Button(interface["frame"], text="删除语种", width=12, font=("Arial", 10), bg="#FF0000")
        language["delete_button"].grid(row=language_num+1, column=17, sticky=tk.W)
        language["delete_button"].config(command=lambda: delete_language(interface, language))
        interface["frame"].rowconfigure(language_num + 1, weight=1)
        interface["languages"].append(language)
        if language_num > 0:
            interface["languages"][language_num - 1]["delete_button"].grid_forget()

def delete_language(interface, language):
    if len(interface["languages"]) > 1:
        language["language_label"].destroy()
        language["language_option"].destroy()
        language["blacklist_label"].destroy()
        language["blacklist"].destroy()
        language["blacklist_button"].destroy()
        language["keyword_label"].destroy()
        language["keyword"].destroy()
        language["keyword_button"].destroy()
        language["comment_label"].destroy()
        language["comment"].destroy()
        language["comment_button"].destroy()
        language["delete_button"].destroy()
        interface["languages"].remove(language)
        if len(interface["languages"]) > 0:
            interface["languages"][-1]["delete_button"].grid(row=len(interface["languages"]) + 1, column=17, sticky=tk.W)
        if len(interface["languages"]) == 1:
            interface["languages"][-1]["delete_button"].grid_forget()

def add_interface():
    interface_num = len(interfaces)
    interface = {}
    interface["frame"] = tk.Frame(root)
    interface["frame"].config(bg="#F0F0F0")
    interface["frame"].grid(row=interface_num+3, column=0, sticky=tk.W)
    interface["name"] = tk.Label(interface["frame"], text="接口"+str(interface_num+1), width=8, font=("Arial", 11), bg="#F0F0F0")
    interface["name"].grid(row=0, column=0, sticky=tk.W)
    tk.Label(interface["frame"], text="端口:", width=5, font=("Arial", 11), bg="#F0F0F0").grid(row=0, column=1, sticky=tk.W)
    interface["port"] = tk.Entry(interface["frame"], width=6, font=("Arial", 11))
    interface["port"].grid(row=0, column=2, sticky=tk.W)
    tk.Label(interface["frame"], text="图片:", width=4, font=("Arial", 11), bg="#F0F0F0").grid(row=0, column=3, sticky=tk.W)
    interface["image"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
    interface["image"].grid(row=0, column=4, sticky=tk.W)
    interface["image_button"] = tk.Button(interface["frame"], text="选择文件夹", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(interface["image"]))
    interface["image_button"].grid(row=0, column=5, sticky=tk.W)
    interface["languages"] = []
    language = {}
    language["language_label"] = tk.Label(interface["frame"], text="语种:", width=6, font=("Arial", 11), bg="#F0F0F0")
    language["language_label"].grid(row=0, column=6, sticky=tk.W)
    language["language"] = tk.StringVar(value="英语")
    language["language_option"] = tk.OptionMenu(interface["frame"], language["language"], "阿拉伯语", "丹麦语", "德语", "俄语", "法语", "芬兰语", "韩语", "荷兰语", "捷克语", "马来西亚语", "葡萄牙语", "日语", "瑞典语", "瑞士语", "斯洛伐克语", "泰语", "土耳其语", "西班牙语", "希腊语", "匈牙利语", "意大利语", "印地语", "印度尼西亚语", "英语", "中文繁体", "中文简体")
    language["language_option"].config(width=8, font=("Arial", 11), bg="#87CEFA")
    language["language_option"].grid(row=0, column=7, sticky=tk.W)
    language["blacklist_label"] = tk.Label(interface["frame"], text="黑名单:", width=6, font=("Arial", 11), bg="#F0F0F0")
    language["blacklist_label"].grid(row=0, column=8, sticky=tk.W)
    language["blacklist"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
    language["blacklist"].grid(row=0, column=9, sticky=tk.W)
    language["blacklist_button"] = tk.Button(interface["frame"], text="选择黑名单", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(language["blacklist"]))
    language["blacklist_button"].grid(row=0, column=10, sticky=tk.W)
    language["keyword_label"] = tk.Label(interface["frame"], text="关键词:", width=6, font=("Arial", 11), bg="#F0F0F0")
    language["keyword_label"].grid(row=0, column=11, sticky=tk.W)
    language["keyword"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
    language["keyword"].grid(row=0, column=12, sticky=tk.W)
    language["keyword_button"] = tk.Button(interface["frame"], text="选择关键词", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(language["keyword"]))
    language["keyword_button"].grid(row=0, column=13, sticky=tk.W)
    language["comment_label"] = tk.Label(interface["frame"], text="评论文本:", width=8, font=("Arial", 11), bg="#F0F0F0")
    language["comment_label"].grid(row=0, column=14, sticky=tk.W)
    language["comment"] = tk.Entry(interface["frame"], width=15, font=("Arial", 11))
    language["comment"].grid(row=0, column=15, sticky=tk.W)
    language["comment_button"] = tk.Button(interface["frame"], text="选择评论文本", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: select_path(language["comment"]))
    language["comment_button"].grid(row=0, column=16, sticky=tk.W)
    language["delete_button"] = tk.Button(interface["frame"], text="删除语种", width=12, font=("Arial", 10), bg="#FF0000")
    language["delete_button"].grid(row=0, column=17, sticky=tk.W)
    language["delete_button"].config(command=lambda: delete_language(interface, language))
    interface["languages"].append(language)
    interface["add_language_button"] = tk.Button(interface["frame"], text="新增语种", width=12, font=("Arial", 10), bg="#87CEFA", command=lambda: add_language(interface))
    interface["add_language_button"].grid(row=0, column=18, sticky=tk.W)
    interface["add_interface_button"] = tk.Button(interface["frame"], text="新增接口", width=12, font=("Arial", 10), bg="#87CEFA", command=add_interface)
    interface["add_interface_button"].grid(row=0, column=19, sticky=tk.W)
    interface["delete_interface_button"] = tk.Button(interface["frame"], text="删除接口", width=12, font=("Arial", 10), bg="#FF0000")
    interface["delete_interface_button"].grid(row=0, column=20, sticky=tk.W)
    interface["delete_interface_button"].config(command=lambda: delete_interface(interface))
    interfaces.append(interface)
    if interface_num > 0:
        interfaces[interface_num - 1]["languages"][-1]["delete_button"].grid_forget()

def delete_interface(interface):
    if len(interfaces) > 1:
        interface["frame"].destroy()
        interfaces.remove(interface)
        for i in range(len(interfaces)):
            interfaces[i]["name"].config(text="接口"+str(i+1))
            interfaces[i]["frame"].grid(row=i+3, column=0, sticky=tk.W)
        if len(interfaces) > 0:
            interfaces[-1]["languages"][-1]["delete_button"].grid(row=len(interfaces[-1]["languages"]) + 1, column=17, sticky=tk.W)
        if len(interfaces) == 1:
            interfaces[0]["languages"][-1]["delete_button"].grid_forget()

title = tk.Label(root, text="OCR控制界面", font=("Arial", 20, "bold"), bg="#F0F0F0", fg="#0000FF")
title.grid(row=0, column=0, pady=(20, 0), sticky=tk.W+tk.E)

tk.Label(root, text="", font=("Arial", 11), bg="#F0F0F0").grid(row=1, column=0)

interfaces = []
add_interface()

button_frame = tk.Frame(root, bg="#F0F0F0")
start_button = tk.Button(button_frame, text="启动", width=10, font=("Arial", 12), bg="#87CEFA")
stop_button = tk.Button(button_frame, text="停止", width=10, font=("Arial", 12), bg="#FF0000")

button_frame.grid(row=len(interfaces)+3, column=0, sticky=tk.W, pady=10)
start_button.grid(row=0, column=0, padx=(100, 50))
stop_button.grid(row=0, column=1, padx=(50, 100))

# 监听窗口大小变化的事件
def on_resize(event):
    button_frame.grid(row=len(interfaces)+3, column=0, sticky=tk.W, pady=10)
    start_button.grid(row=0, column=0, padx=(100, 50))
    stop_button.grid(row=0, column=1, padx=(50, 100))

root.bind('<Configure>', on_resize)

root.mainloop()
