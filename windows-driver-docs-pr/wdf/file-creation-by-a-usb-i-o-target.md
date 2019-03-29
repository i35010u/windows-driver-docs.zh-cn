---
title: 通过 USB I/O 目标创建文件
description: 通过 USB I/O 目标创建文件
ms.assetid: 44bbc4c7-632d-4d75-94b9-f65e4d480e90
keywords:
- 用户模式驱动程序 WDK UMDF，USB I/O 目标文件创建
- UMDF WDK，USB I/O 目标、 文件创建
- 用户模式驱动程序框架 WDK，USB I/O 目标
- 基于框架的驱动程序 WDK UMDF，USB I/O 目标
- USB I/O 面向 WDK UMDF，文件创建
- I/O 面向 WDK UMDF，USB、 文件创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 868367ed25ef7b88ac0b7f8468a66c8fd848d7ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565374"
---
# <a name="file-creation-by-a-usb-io-target"></a>通过 USB I/O 目标创建文件


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

其在初始化期间，USB I/O 目标创建一个内部堆栈文件对象，它表示 USB I/O 目标保持打开状态的默认会话。 有关内部堆栈文件对象的详细信息，请参阅[创建将文件对象传递给处理 I/O](creating-a-file-object-to-handle-i-o.md)。 USB I/O 目标或其子 USB 管道目标项使用此文件对象发送它们 （例如，若要获取的 USB 配置描述符的 I/O） 源自任何 I/O。

驱动程序可以使用此内部堆栈文件对象中的格式函数 (例如，驱动程序可以将指针传递给该文件对象到*pFile*调用中的参数[ **IWDFIoTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)方法) 如果该驱动程序必须在此文件对象的默认会话上发送输入/输出。 若要获取的内部堆栈文件对象，该驱动程序可以调用[ **IWDFIoTarget::GetTargetFile** ](https://msdn.microsoft.com/library/windows/hardware/ff559243)方法。

此内部堆栈文件对象已关闭时 I/O 目标为显式释放，当驱动程序调用[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)方法上的 I/O 目标值，或隐式地时我 /O 目标父被释放。

如果任何 I/O 设备删除时保持此内部堆栈文件对象上的未完成，此文件对象将无法关闭，并且 UMDF 将生成一个驱动程序停止。 有关详细信息，请参阅[创建和 Using Driver-Created 文件对象](creating-and-using-driver-created-file-objects.md)。

 

 





