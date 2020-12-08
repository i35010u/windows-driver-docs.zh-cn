---
title: 通过 USB I/O 目标创建文件
description: 通过 USB I/O 目标创建文件
keywords:
- 用户模式驱动程序 WDK UMDF、USB i/o 目标、文件创建
- UMDF WDK、USB i/o 目标、文件创建
- User-Mode Driver Framework WDK，USB i/o 目标
- 基于框架的驱动程序 WDK UMDF，USB i/o 目标
- USB i/o 目标是 WDK UMDF，文件创建
- I/o 目标为 WDK UMDF、USB、文件创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d57e859b3bbb24212c89ac1aad510bdd09c7f2cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815745"
---
# <a name="file-creation-by-a-usb-io-target"></a>通过 USB I/O 目标创建文件


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

在初始化期间，USB i/o 目标将创建一个内部堆栈文件对象，该对象表示 USB i/o 目标保持打开状态的默认会话。 有关堆栈内文件对象的详细信息，请参阅 [创建用于处理 i/o 的文件对象](creating-a-file-object-to-handle-i-o.md)。 USB i/o 目标或其 USB 管道目标子对象使用此文件对象发送其产生的任何 i/o (例如，通过 i/o 获取 USB 配置描述符) 。

驱动程序可以在格式函数中使用此堆栈内文件对象 (例如，驱动程序可以在调用 [**IWDFIoTarget：： FormatRequestForRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)方法时将指向此文件对象的指针传递到 *.pfile* 参数) 如果驱动程序必须在此文件对象的默认会话上发送 i/o。 为了获取堆栈内文件对象，驱动程序可以调用 [**IWDFIoTarget：： GetTargetFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile) 方法。

当 i/o 目标被显式释放时，当驱动程序调用 i/o 目标上的 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 方法时，或者当 i/o 目标的父级被释放时，将关闭此堆栈内文件对象。

如果在设备删除时此堆栈内文件对象上的任何 i/o 仍处于未处理状态，则此文件对象将无法关闭，且 UMDF 将生成驱动程序停止。 有关详细信息，请参阅 [创建和使用 Driver-Created 文件对象](creating-and-using-driver-created-file-objects.md)。

 

