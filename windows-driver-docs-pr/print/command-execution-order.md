---
title: 命令执行顺序
description: 命令执行顺序
ms.assetid: 2bf7438c-bfb0-407f-9c80-be3b8a9322f9
keywords:
- 打印机命令 WDK Unidrv，执行顺序
- 序列号 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff9f9da1fbf6ba92d821a49ae0af2a7824716cf
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802453"
---
# <a name="command-execution-order"></a>命令执行顺序





必须以有意义的顺序将打印机命令发送到打印机硬件。 对于在 GPD 语言中定义的大多数命令名称，Unidrv 知道何时将命令的转义序列发送到打印机。 有两种例外情况：

[选项选择命令](option-selection-command.md)

[打印机配置命令](printer-configuration-commands.md)

对于这两种命令类型，都必须指定命令的执行顺序。

命令执行顺序由两个组件组成：一个作业部分名称和一个序列顺序号。 Unidrv 驱动程序将每个打印作业分为六部分。 对于每个部分，Unidrv 将按指定顺序向打印机发送分配给部分的命令。 定义了下列部分：

<a href="" id="job-setup"></a>作业 \_ 设置  
分配给作业 \_ 设置部分的命令将每个作业发送一次。 它们是新作业开始时发送的第一个命令。 这些命令是从 Unidrv 的 [**DrvStartDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc) 函数实现中发送的。

<a href="" id="doc-setup"></a>文档 \_ 设置  
分配给 "文档设置" 部分的命令 \_ 将在发送文档的第一页之前发送。 命令是从 Unidrv 的 DrvStartDoc 函数实现中发送的。  (这些命令也会在应用程序调用 Win32 ResetDC 函数后发送。 本部分中的命令不得删除已下载的信息，如软字体和模式。 ) 

<a href="" id="page-setup"></a>页面 \_ 设置  
在 \_ 开始绘制之前，将在每个新页面的开头发送分配给 "页面设置" 部分的命令。 这些命令是从 Unidrv 的 [**DrvStartPage**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartpage) 函数实现中发送的。

<a href="" id="page-finish"></a>页面 \_ 完成  
\_绘制完成后，会在每个页面的末尾发送分配给 "页面完成" 部分的命令。 这些命令是从 Unidrv 的 [*DrvSendPage*](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsendpage) 函数实现中发送的。

<a href="" id="doc-finish"></a>文档 \_ 完成  
分配给 "文档完成" 部分的命令 \_ 将在发送文档的最后一页后发送。 命令是从 Unidrv 的 [**DrvEndDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenddoc) 函数实现中发送的。 此部分中 (命令不得删除已下载的信息，如软字体和模式。 ) 

<a href="" id="job-finish"></a>作业 \_ 完成  
分配给 "作业完成" 部分的命令 \_ 将每个作业发送一次。 它们是作业结束时发送的最后一条命令。 这些命令是从 Unidrv 的 DrvEndDoc 函数实现中发送的。

在上述每个部分中，命令按序列号所指示的顺序执行。

若要指定命令的部分和序列号，请使用[命令属性](command-attributes.md)中所述的** \* Order**属性。 格式为：

** \* 顺序**： *SectionName*。*SequenceNumber*

其中， *SectionName* 是作业 \_ 安装、DOC \_ 设置、页面 \_ 设置、页面 \_ 完成、文档 \_ 完成或作业完成的其中一个 \_ ， *SequenceNumber* 为数值。

序列号不必是连续的，但部分中指定的每个数字必须是唯一的。 部分中的命令将从其序列号最小的序列号到最高的顺序执行。 例如，以下条目指示将 **InputBin**、 **PaperSize**和 **解决** 功能的选项分配给 "文档 \_ 设置" 部分，并按指定顺序发送：

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

 

 




