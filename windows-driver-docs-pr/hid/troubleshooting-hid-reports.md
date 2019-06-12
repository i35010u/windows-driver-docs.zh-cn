---
title: 排查 HID 报告问题
description: 排查 HID 报告问题
ms.assetid: 8fbf641b-461b-44c2-9cc5-c1547abc75d6
keywords:
- HID 报告 WDK，故障排除
- 报告 WDK HID，故障排除
- WDK HID 报表故障排除
- 已删除的 HID 报表 WDK
- WDK HID 报告错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a668f4a72cf44ca47e9c454178da2e4bf8d797a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376745"
---
# <a name="troubleshooting-hid-reports"></a>排查 HID 报告问题





本部分介绍以下最常见的问题的用户模式应用程序和内核模式驱动程序时可能会遇到尝试提取或设置[HID 用法](hid-usages.md):

[HID 的报表 ID 错误](#hid-report-id-errors)

[删除 HID 报表](#dropped-hid-reports)

### <a href="" id="hid-report-id-errors"></a> HID 的报表 ID 错误

当应用程序或驱动程序收到 HID 报表从 HID 集合时，它可以是任何报表，该集合包含 （因为集合可按任意顺序返回报表）。 **HidP\_获取 * * * Xxx*例程将返回以下状态值，指示报表 ID 错误：

<a href="" id="hidp-status-incompatible-report-id"></a>HIDP\_状态\_不兼容\_报表\_ID  
请求的用法是在报表中支持的 HID 集合，但不是在指定的应用程序或驱动程序的报表。

<a href="" id="hidp-status-usage-not-found"></a>HIDP\_状态\_用法\_不\_找到  
请求的用法不支持顶级集合的任何报表中。

例如下, 图显示了包含两个报告的 HID 集合。

![说明包含两个报告的 hid 的集合的关系图](images/reportid.png)

根据此示例中，假定应用程序或驱动程序从一个集合并调用接收到的报告[ **HidP\_GetUsageValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539748)提取"值 X。"的当前值 如果报表的 ID 为 7，例程将返回 HIDP\_状态\_不兼容\_报表\_ID，以指示设备是否支持在值 X，但值 X 不是在报告中提供。 但是，如果应用程序或驱动程序请求"值 Z"的值，例程将返回 HIDP\_状态\_用法\_不\_找到，它指示值 Z 不在支持的任何报表集合。

当应用程序或驱动程序使用 **HidP\_设置 * * * Xxx*还在报表中，例程可以设置用法的例程将返回相同的两个状态值。 HIDP 的含义\_状态\_用法\_不\_找到等同于使用 **HidP\_获取 * * * Xxx*例程。 但是，HIDP 的含义\_状态\_不兼容\_报表\_ID 是不同。 此状态值指示报表以前配置为使用报表 ID，并指定由调用方的用法不属于该报表 id。 作为示例，使用上图中，在应用程序或驱动程序后使用[ **HidP\_SetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539792)初始化为零的报表中设置"按钮 2"，报表使用配置的报表 ID七个。 如果应用程序或驱动程序随后尝试使用[ **HidP\_SetUsageValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539797)若要在同一报表中设置"值 X"，该例程将返回 HIDP\_状态\_不兼容\_报表\_id。

如果**HidP\_** <em>Xxx</em>例程将返回 HIDP\_状态\_兼容\_报表\_ID，调用方应采用之一以下操作：

-   如果调用方会将设置用法，它应分配正确长度的新的报表、 零初始化，然后再次调用该例程。 调用方可以将报表发送到已成功设置报表中的所有用法后的集合。

-   如果调用方提取使用情况，则应使用不同的报表从集合中获取调用例程。

### <a href="" id="dropped-hid-reports"></a> 删除 HID 报表

当[HID 客户端驱动程序](hid-client-drivers.md)获取输入 HID 集合，从报表的报表存储在环形缓冲区维护的 HID 类驱动程序。 此机制减少应用程序或驱动程序将丢失其需要的输入的报表的可能性。

默认情况下的 HID 类驱动程序维护包含 32 报表输入的报表环形缓冲区。 如果集合将数据传输到 HID 类驱动程序比在用户模式应用程序更快地或内核模式驱动程序从缓冲区中检索，都将因缓冲区溢出而丢失输入的报表。 要降低的可能性的缓冲区溢出、 应用程序或驱动程序可以重新配置的大小，以报告的缓冲区数。 驱动程序检索并更改使用的缓冲区的大小[ **IOCTL\_获取\_NUM\_设备\_输入\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff541058)请求和一个[ **IOCTL\_设置\_NUM\_设备\_输入\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff542087)请求。 应用程序通过调用执行相同的操作[ **HidD\_GetNumInputBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff539675)并[ **HidD\_SetNumInputBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff539686).

 

 




