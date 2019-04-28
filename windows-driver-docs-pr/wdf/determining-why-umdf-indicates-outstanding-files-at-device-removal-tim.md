---
title: 在设备删除时 UMDF 指示未完成的文件
description: 介绍如何使用 Wudfext.dll 来确定为何 UMDF 指示时删除设备有未完成的文件。
ms.assetid: 9a8b3b69-1192-40c1-895b-4abfc01c1ca7
keywords:
- 调试方案 WDK UMDF，UMDF 在设备删除时指示未完成的文件
- UMDF WDK，调试方案，UMDF 在设备删除时指示未完成的文件
- UMDF WDK UMDF 在设备删除时指示未完成的文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 552b9ac5d04b0764ad1248649b828b02177340a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337858"
---
# <a name="determining-why-umdf-indicates-outstanding-files-at-device-removal-time"></a>确定 UMDF 在删除设备时指示文件未完成的原因


本主题介绍如何结合使用用户模式驱动程序框架 (UMDF) 版本 1 或 2 驱动程序中使用 Wudfext.dll 调试器扩展来确定为何 UMDF 指示时删除设备有未完成的文件。

对于 UMDF 版本 1，将使用在 wudfext.dll 中实现的扩展命令。 从 UMDF 版本 2 开始，将使用在 wdfkd.dll 中实现的扩展命令。

若要确定为什么 UMDF 指示未完成的文件，请使用以下步骤：

1.  使用[ **！ wudfext.umdevstack** ](https://msdn.microsoft.com/library/windows/hardware/ff566189) (UMDF 1) 或[ **！ wdfkd.wdfumdevstack** ](https://msdn.microsoft.com/library/windows/hardware/dn265379) (UMDF 2)，转储设备堆栈。 转储包括未完成的 UMDF 内部堆栈文件 （即，而不是由应用程序或由另一个堆栈中的驱动程序创建的文件对象的堆栈中的驱动程序创建的文件对象）。

2.  对于每个内部堆栈文件，请运行[ **！ wudfext.umfile** ](https://msdn.microsoft.com/library/windows/hardware/ff566193) (UMDF 1) 或[ **！ wdfkd.wdfumfile** ](https://msdn.microsoft.com/library/windows/hardware/dn265382) (UMDF 2) 若要获取有关文件的信息.

    输出包括处于挂起状态的 Irp 的列表。

3.  确定每个 IRP 为什么使用未完成[ **！ wudfext.umirp** ](https://msdn.microsoft.com/library/windows/hardware/ff566195) (UMDF 1) 或[ **！ wdfkd.wdfumirp** ](https://msdn.microsoft.com/library/windows/hardware/dn265383) (UMDF 2) 若要获取的信息有关 IRP。

    从每个输出[ **！ wudfext.umirp** ](https://msdn.microsoft.com/library/windows/hardware/ff566195)或[ **！ wdfkd.wdfumirp**](https://msdn.microsoft.com/library/windows/hardware/dn265383):

    -   确定是否 IRP 已完成。
    -   确定显式由驱动程序或对象树的隐式是否未删除驱动程序创建请求。

 

 





