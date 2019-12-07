---
title: NatVis 中的本机调试器对象
description: Dx 命令显示使用 NatVis C++扩展模型的表达式。 有关 NatVis 的详细信息，请参阅在调试器中创建本机对象的自定义视图。
keywords:
- NatVis 中的本机调试器对象
ms.date: 08/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: dced0a8dea51c87864447e104f9cf2ea3a82c742
ms.sourcegitcommit: 5a10ea8a98fa4b6f8c43176156530e859a71b10e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908354"
---
# <a name="native-debugger-objects-in-natvis"></a>NatVis 中的本机调试器对象

## <a name="overview"></a>概述

本机调试器对象表示调试器环境的各种构造和行为。 示例调试器对象包括以下各项。

-   会议
-   线程/线程
-   进程/进程
-   堆栈帧/堆栈帧
-   局部变量
-   模块/模块
-   实用程序
-   省/市/自治区
-   “设置”

可以使用 dx 命令和 LINQ 与调试器对象进行交互。 有关详细信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)和[将 LINQ 与调试器对象配合使用](using-linq-with-the-debugger-objects.md)。

还可以使用 JavaScript 来处理调试器对象。 有关此内容的详细信息，请参阅[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md)。

本主题介绍如何创建自定义 NatVis 可视化工具以显示调试器对象。 

## <a name="natvis-development-resources"></a>NatVis 开发资源

有关使用 NatVis 的常规信息，请参阅这些资源。

[创建本机对象的自定义视图](https://docs.microsoft.com/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015)

[ **.nvload**](-nvload--natvis-load-.md)

[ **.nvlist**](-nvlist--natvis-list-.md)

[ **.nvunload**](-nvunload--natvis-unload-.md)

[ **.nvunloadall**](-nvunloadall--natvis-unload-all-.md)

## <a name="custom-natvis-object-example"></a>自定义 NatVis 对象示例

创建一个具有C++ **CDog**类的实例的简单应用程序。

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

创建一个名为 natvis 的文件，其中包含以下 XML：

```XML
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="https://schemas.microsoft.com/vstudio/debugger/natvis/2010">
   <Type Name="CDog">
      <DisplayString>{{Age = {m_age} years. Weight = {m_weight} pounds.}}</DisplayString>
   </Type>
</AutoVisualizer>
```

将 natvis 复制到安装目录中的 "可视化工具" 文件夹，以用于 Windows 调试工具。 例如：

C：\\程序文件\\Windows 调试工具（x64）\\可视化工具

运行程序，并在 main 函数处中断。 执行一个步骤，以便初始化变量 `MyDog`。 使用[ **？？** 显示 `MyDog`](----evaluate-c---expression-.md) 并再次使用**dx**。

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

## <a name="see-also"></a>另请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[将 LINQ 用于调试器对象](using-linq-with-the-debugger-objects.md)

[JavaScript 扩展中的本机调试器对象](native-objects-in-javascript-extensions.md) 
