---
title: 命令执行顺序
description: 命令执行顺序
ms.assetid: 2bf7438c-bfb0-407f-9c80-be3b8a9322f9
keywords:
- 打印机命令 WDK Unidrv，执行顺序
- 序列号 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950bc0c7bc784778d077f5e298d3901ea8b5754f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519254"
---
# <a name="command-execution-order"></a>命令执行顺序





必须将打印机命令发送到打印机硬件有意义的顺序。 对于大多数 GPD 语言中定义的命令名称，Unidrv 知道何时向打印机发送命令的转义序列。 有两种例外情况：

[选项选择命令](option-selection-command.md)

[打印机配置命令](printer-configuration-commands.md)

对于这两种命令类型，必须指定应在执行命令的顺序。

命令执行顺序由两个组件--作业部分名称和一个序号顺序组成。 Unidrv 驱动程序将每个打印作业划分为六个部分。 对于每个部分中，Unidrv 发送打印机分配到的部分中，指定序列中的命令。 定义以下各节：

<a href="" id="job-setup"></a>作业\_安装程序  
分配给作业的命令\_设置部分发送一次每个作业。 它们是发送一个新的作业开始时的第一个命令。 这些命令从发送 Unidrv 的实现的内部[ **DrvStartDoc** ](https://msdn.microsoft.com/library/windows/hardware/ff556296)函数。

<a href="" id="doc-setup"></a>DOC\_安装程序  
命令分配给文档\_发送文档的第一页之前发送设置部分。 将命令发送从 DrvStartDoc 函数 Unidrv 的实现中。 （这些命令也会发送后应用程序调用 Win32 ResetDC 函数。 在本部分中的命令必须不删除下载的信息，例如软字体和模式。）

<a href="" id="page-setup"></a>页\_安装程序  
命令分配给该页\_设置部分在每个新页的开头发送之前开始绘制。 这些命令从发送 Unidrv 的实现的内部[ **DrvStartPage** ](https://msdn.microsoft.com/library/windows/hardware/ff556298)函数。

<a href="" id="page-finish"></a>PAGE\_FINISH  
命令分配给该页\_完成部分绘制完成后发送的每个页上，末尾。 这些命令从发送 Unidrv 的实现的内部[ *DrvSendPage* ](https://msdn.microsoft.com/library/windows/hardware/ff556281)函数。

<a href="" id="doc-finish"></a>DOC\_完成  
命令分配给文档\_发送文档的最后一页之后发送完成部分。 将命令发送从 Unidrv 的实现的内部[ **DrvEndDoc** ](https://msdn.microsoft.com/library/windows/hardware/ff556215)函数。 （在本部分中的命令必须删除已下载的信息，例如软字体和模式）。

<a href="" id="job-finish"></a>作业\_完成  
分配给作业的命令\_完成部分发送一次每个作业。 它们是在作业结束时发送的最后一个命令。 这些命令从发送 DrvEndDoc 函数 Unidrv 的实现中。

在这些部分中，通过其序列号指示的顺序执行命令。

若要指定命令的部分和序列号，请使用**\*顺序**属性中所述[命令属性](command-attributes.md)。 格式为：

**\*顺序**:*SectionName*。*序列号*

其中*SectionName*是作业之一\_安装程序、 文档\_安装程序页\_安装过程中，页\_完成、 DOC\_完成或作业\_完成，和*SequenceNumber*是数字值。

序列号不需要是连续的但在某一部分指定每个数字必须是唯一的。 部分中执行命令从最低序列号的最高。 例如，以下条目表示的选项**InputBin**， **PaperSize**，并**解析**功能分配给文档\_安装程序部分并发送指定的顺序：

```cpp
*Feature: InputBin
{
    *Option: Auto
    {
        *Name: "Auto Tray"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.50
            *Cmd: "<1B>(1<010014>"
        }
    }
    ...
}
*Feature: PaperSize
{
    *DefaultOption: Letter
    *Option: Letter
    {
        *Name: "Letter size"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.60
            *Cmd: "<1B>(g<0300>n<01>r"
        }
    }
    ...
}
*Feature: Resolution
{
    *DefaultOption: 360dpi
    *Option: 360dpi
    {
        *Name: "360 dpi x 360dpi"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.70
            *Cmd: "<1B>(d<020001>"
        }
    }
    ...
}
```

 

 




