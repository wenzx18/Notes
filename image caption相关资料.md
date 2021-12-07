# image caption相关资料

[image caption毕设代码](https://github.com/ruotianluo/self-critical.pytorch)

dense image caption & style caption 毕设的研究方向

e.g. 风格 对同一个青少年 随着时间改变 可能某一时刻style发生变化 没准是抑郁了

将demo做成本地的，用于chatbot上

带语言风格的caption可用于心理学

- dense image caption 用于demo，描述图像某一块的内容，互动性比较强

- point caption就是用户点哪块就说哪块，也比较合适

https://github.com/jcjohnson/densecap

https://github.com/Dong-JinKim/DenseRelationalCaptioning

https://github.com/zhjohnchan/awesome-image-captioning 这应该是一个caption的paper和代码 数据大全(mark)

https://openaccess.thecvf.com/content_CVPR_2019/papers/Guo_MSCap_Multi-Style_Image_Captioning_With_Unpaired_Stylized_Text_CVPR_2019_paper.pdf 这是一个style的paper 同一个照片 不同的语气来描述，把这里面的backbone换成比较新的sota应该能再提升一些

在毕设里能不能加入 给用户看图像 就像上面这个paper 产生并给用户5个或更多选项 其中有1~2个 选了就是判断焦虑/抑郁的

目前sota的标准caption的工作是 m2transformer , x-linear transformer和DLCT，都有开源代码