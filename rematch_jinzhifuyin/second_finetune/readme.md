# 添加水印程序说明

　　本程序的目标是为了在使用gan进行去水印处理过程中能够得到更多与原始数据特征分布相似的训练数据，通过采用水印平移的方式进行训练数据的扩充。这里所说的特征分布主要指的是原始图片的亮度、图片的模糊度、水印的透明度等特征，在执行本程序之前，也尝试通过修改模糊程度、亮度等特征，生成了一批训练用的数据，但是该批数据与真实用数据仍存在较大差异，导致去水印的模型在伪造数据上取得较好表现而在真实数据上表现欠佳的情况，本程序就是针对该问题进行改进。通过水印平移的方式，通过设置不同水印和底片的清晰度，最大程度上来模拟真实的水印图片。

## 文件及程序使用

-- roi.jpg: 用于模板匹配的水印的模板，根据这个模板在待处理图片中找到水印的区域，并将该区域进行平移处理。

-- roi_2.jpg: 生成数据第一阶段用到的水印模板。

-- watermark_remover.py: 将添加水印的代码直接写在前期去水印的代码中，从程序的第194行开始对应的是添加水印的功能，已经修改代码，可以直接运行这个程序。

--source_815: 存放经过第一批挑选出来的原始图片，水印的位置在图片的空白位置处，但是部分水印和底片的文字有重叠。

--source_596: 存放第二批经过数据清洗之后得到的原始图片，水印的位置在图片的空白位置处，水印与底片的文字部分没有重叠。

程序运行的指令如下：

python3 no_watermark.py --template_file roi_example.jpg --file_path file_path_example --target_path target_path_example --ratio ratio_example

--template_file: 用于模板匹配的水印模板

--file_path: 存放待处理原始数据集的文件夹路径

--target_path: 存放经过水印平移处理之后图片的目标文件夹路径

--ratio: 控制生成图片的数量

　　在整个训练的过程中，待处理的原始数据一共用到了两批，第一批是没有经过数据清洗的815张图片，第二批是经过数据清洗之后的596张图片，两组原始数据存放在当前路径下的source_815和source_596两个文件夹下，需要注意的是，在输入路径的参数时，建议输入绝对路径，如果是相对路径，不可以以'.'作为文件夹路径的开头，如'./source_596/'，可以'source_596/'。

　　不同训练阶段对应水印平移程序的具体参数值在训练流程的说明中给出。