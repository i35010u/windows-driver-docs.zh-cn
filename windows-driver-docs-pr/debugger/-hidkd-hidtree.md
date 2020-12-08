---
title: hidkd.hidtree
description: Hidkd. hidtree 命令显示具有 HID 函数驱动程序及其子节点的所有设备节点的列表。
keywords:
- hidkd hidtree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidtree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e150ddf145906e07e211dc215d756dc9f021d4ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821051"
---
# <a name="hidkdhidtree"></a>!hidkd.hidtree


**！ Hidkd. hidtree** 命令显示具有 HID 函数驱动程序及其子节点的所有设备节点的列表。 子节点的物理设备对象 (PDO) 由父节点的 HID 函数驱动程序创建。

```dbgcmd
!hidkd.hidtree
```

此屏幕截图显示了 **！ hidtree** 命令的输出示例。

![hidtree 命令的输出](images/hidkd01.png)

O

在此示例中，有两个具有 HID 函数驱动程序的设备节点。  (FDO) 的功能设备对象表示这两个节点中的 HID 驱动程序。 第一个 FDO 节点具有两个子节点，第二个 FDO 节点有一个子节点。 在调试器输出中，子节点具有 PDO 标题。

**注意**  这组设备节点不构成具有单个根节点的树。 具有 HID 函数驱动程序的设备节点可以彼此隔离。

 

调试 HID 问题时， **！ hidtree** 是一个不错的开端，因为该命令显示了几个可传递给其他 HID 调试器命令的地址。 输出使用 [ (DML) 的调试器标记语言 ](debugger-markup-language-commands.md) 来提供链接。 这些链接执行命令，这些命令可为与单个设备节点相关的详细信息。 例如，可以通过单击某个 [**！ hidfdo**](-hidkd-hidfdo.md) 链接获取有关 FDO 的信息。 作为单击链接的替代方法，可以输入命令。 例如，若要查看有关前面输出中第一个节点的详细信息，可以输入命令 **！ devnode 0xffffe00003b18d30**。

**注意**  DML 功能在 WinDbg 中可用，但在 Visual Studio 或 KD 中不可用。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Hidkd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 扩展](hid-extensions.md)

 

 






