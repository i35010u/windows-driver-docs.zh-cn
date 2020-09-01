---
title: 通过 USB I/O 目标创建文件
description: 通过 USB I/O 目标创建文件
ms.assetid: 44bbc4c7-632d-4d75-94b9-f65e4d480e90
keywords:
- 用户模式驱动程序 WDK UMDF、USB i/o 目标、文件创建
- UMDF WDK、USB i/o 目标、文件创建
- 用户模式驱动程序框架 WDK，USB i/o 目标
- 基于框架的驱动程序 WDK UMDF，USB i/o 目标
- USB i/o 目标是 WDK UMDF，文件创建
- I/o 目标为 WDK UMDF、USB、文件创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ee7fbc24d42798518661bdbee98dac49ad0fba
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192765"
---
# <a name="file-creation-by-a-usb-io-target"></a>通过 USB I/O 目标创建文件


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

在初始化期间，USB i/o 目标将创建一个内部堆栈文件对象，该对象表示 USB i/o 目标保持打开状态的默认会话。 有关堆栈内文件对象的详细信息，请参阅 [创建用于处理 i/o 的文件对象](creating-a-file-object-to-handle-i-o.md)。 USB i/o 目标或其 USB 管道目标子对象使用此文件对象发送其产生的任何 i/o (例如，通过 i/o 获取 USB 配置描述符) 。

驱动程序可以在格式函数中使用此堆栈内文件对象 (例如，驱动程序可以在调用[**IWDFIoTarget：： FormatRequestForRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)方法时将指向此文件对象的指针传递到 *.pfile*参数) 如果驱动程序必须在此文件对象的默认会话上发送 i/o。 为了获取堆栈内文件对象，驱动程序可以调用 [**IWDFIoTarget：： GetTargetFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile) 方法。

当 i/o 目标被显式释放时，当驱动程序调用 i/o 目标上的 [**IWDFObject：:D eletewdfobject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) 方法时，或者当 i/o 目标的父级被释放时，将关闭此堆栈内文件对象。

如果在设备删除时此堆栈内文件对象上的任何 i/o 仍处于未处理状态，则此文件对象将无法关闭，且 UMDF 将生成驱动程序停止。 有关详细信息，请参阅 [创建和使用驱动程序创建的文件对象](creating-and-using-driver-created-file-objects.md)。

 

