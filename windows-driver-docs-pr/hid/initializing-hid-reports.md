---
title: 初始化 HID 报告
description: 初始化 HID 报告
ms.assetid: 14229315-3928-4421-a8d8-c3f7837bf1c3
keywords:
- HID 报告 WDK，初始化
- 报告 WDK HID，初始化
- 初始化报表
- WDK HID 的控件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37f424e6fab021ced41e0bf829be151ebf43ccb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364658"
---
# <a name="initializing-hid-reports"></a>初始化 HID 报告





本部分介绍了如何用户模式应用程序和内核模式驱动程序之前，初始化 HID 报表使用[HIDClass 支持例程](https://msdn.microsoft.com/library/windows/hardware/ff538865)或 Ioctl 的 HID 类驱动程序。

若要初始化报表缓冲区，应用程序或驱动程序创建的初始化为零的缓冲区的所需的大小，以字节为单位的报表类型。 *Xxx*ReportByteLength HID 集合的成员[ **HIDP\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)结构指定的输入、 输出和功能的报表所需的大小。 初始化报表缓冲区之后, 的应用程序或驱动程序可以使用 **HidP\_设置 * * * Xxx*例程，从而为报表中设置控制数据。 报表中，在首次使用 **HidP\_设置 * * * Xxx*例程设置为与指定相关联的报表 ID [HID 用法](hid-usages.md)。 如果应用程序或驱动程序随后尝试设置不兼容的报表 id，使用 **HidP\_设置 * * * Xxx*例程将返回状态为 HIDP\_状态\_不兼容\_报表\_id。

 

 




