---
title: hidkd.hidtree
description: Hidkd.hidtree 命令显示所有已以及及其子节点的 HID 函数驱动程序的设备节点的列表。
ms.assetid: 50FD5526-3B0E-4585-BFFD-72ED363D007A
keywords:
- hidkd.hidtree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidtree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c6d6304de090ad2ffc27721a49d599045e2a781b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336481"
---
# <a name="hidkdhidtree"></a>!hidkd.hidtree


**！ Hidkd.hidtree**命令显示所有已以及及其子节点的 HID 函数驱动程序的设备节点的列表。 子节点有一个物理设备对象 (PDO) 创建的父节点的 HID 功能驱动程序。

```dbgcmd
!hidkd.hidtree
```

此屏幕截图显示的输出的示例 **！ hidtree**命令。

![hidtree 命令的输出](images/hidkd01.png)

O

在此示例中，有两个具有 HID 函数驱动程序的设备节点。 功能的设备对象 (FDO) 表示这两个节点中的 HID 驱动程序。 第一个 FDO 节点具有两个子节点，并第二个 FDO 节点有一个子节点。 在调试器输出中，子节点具有 PDO 标题。

**请注意**  此组设备节点未形成一个树，它有一个单一根节点。 HID 函数驱动程序的设备节点可以是相互隔离的。

 

在调试时 HID 问题 **！ hidtree**是一个良好起点，因为该命令将显示您可以将它们传递给其他 HID 调试器命令的多个地址。 输出会使用[调试器标记语言 (DML)](debugger-markup-language-commands.md)提供链接。 链接执行命令来提供与单个设备节点相关的详细的信息。 例如，可以单击其中一个获取信息 FDO [ **！ hidfdo** ](-hidkd-hidfdo.md)链接。 作为单击的链接的替代方法，你可以输入命令。 例如，若要查看有关在上面的输出的第一个节点的详细的信息，可以输入命令 **！ devnode 0xffffe00003b18d30**。

**请注意**  DML 功能现已推出的 WinDbg 中，但未在 Visual Studio 或 KD。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HID 的扩展](hid-extensions.md)

 

 






