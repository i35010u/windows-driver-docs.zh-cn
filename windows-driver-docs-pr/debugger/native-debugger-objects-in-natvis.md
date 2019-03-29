---
title: NatVis 中的本机调试器对象
description: Dx 命令显示使用 NatVis 扩展模型的 c + + 表达式。 NatVis 有关的详细信息，请参阅在调试器中的本机对象的创建自定义视图。
keywords:
- NatVis 中本机调试器对象"
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22087a2b36d254b9b287d85ca37103f119647af0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561750"
---
# <a name="native-debugger-objects-in-natvis"></a>NatVis 中的本机调试器对象

## <a name="overview"></a>概述

本机调试器对象表示各种构造和调试器环境的行为。 如调试器对象包括以下内容。

-   会议
-   线程 / 线程
-   进程数 / 处理
-   堆栈帧 / 堆栈帧
-   本地变量
-   模块 / 模块
-   实用程序
-   状态
-   设置

可以使用 dx 命令和 LINQ 与调试器对象进行交互。 有关详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)并[使用 LINQ 与调试器对象](using-linq-with-the-debugger-objects.md)。

您还可以与使用 JavaScript 调试器对象。 有关更多信息，请参阅[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

本主题介绍如何创建自定义的 NatVis 可视化工具显示调试器对象。 

## <a name="natvis-development-resources"></a>NatVis 开发资源

请参阅以下资源使用 NatVis 有关常规信息。

[创建本机对象的自定义视图](https://msdn.microsoft.com/library/jj620914.aspx)

[C + + 使用.natvis 文件的写入调试器类型可视化工具](https://code.msdn.microsoft.com/windowsdesktop/Writing-type-visualizers-2eae77a2)

[**.nvload**](-nvload--natvis-load-.md)

[**.nvlist**](-nvlist--natvis-list-.md)

[**.nvunload**](-nvunload--natvis-unload-.md)

[**.nvunloadall**](-nvunloadall--natvis-unload-all-.md)


## <a name="span-idcustomnatvisobjectexamplespanspan-idcustomnatvisobjectexamplespanspan-idcustomnatvisobjectexamplespancustom-natvis-object-example"></a><span id="Custom_NatVis_object_example"></span><span id="custom_natvis_object_example"></span><span id="CUSTOM_NATVIS_OBJECT_EXAMPLE"></span>自定义 NatVis 对象示例


创建一个简单的 c + + 应用程序具有类的实例**CDog**。

```cpp
class CDog
{
public:
   CDog(){m_age = 8; m_weight = 30;}
   long m_age;
   long m_weight;
};

int main()
{
   CDog MyDog;
   printf_s("%d, %d\n", MyDog.m_age, MyDog.m_weight);
   return 0;
}
```

创建一个名为 Dog.natvis 包含此 XML 文件：

```XML
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
   <Type Name="CDog">
      <DisplayString>{{Age = {m_age} years. Weight = {m_weight} pounds.}}</DisplayString>
   </Type>
</AutoVisualizer>
```

将 Dog.natvis 的有关 Windows 调试工具复制到你的安装目录中的可视化工具文件夹。 例如：

C:\\程序文件\\(x64) Windows 调试工具\\可视化工具

运行程序，并在主函数处中断。 迈出一步，以便该变量`MyDog`就会初始化。 显示`MyDog`使用[ **??**](----evaluate-c---expression-.md) 和使用再次**dx**。

```dbgcmd
0:000> ??MyDog
class CDog
   +0x000 m_age        : 0n8
   +0x004 m_weight     : 0n30
0:000> *
0:000> dx -r1 MyDog
.....
MyDog     : {Age = 8 years. Weight = 30 pounds.} [Type: CDog]
```


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[使用 LINQ 与调试器对象](using-linq-with-the-debugger-objects.md)

[中 JavaScript 扩展本机调试器对象](native-objects-in-javascript-extensions.md) 

 
---
 






