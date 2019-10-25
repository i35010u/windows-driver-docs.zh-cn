---
title: 排查 HID 报告问题
description: 排查 HID 报告问题
ms.assetid: 8fbf641b-461b-44c2-9cc5-c1547abc75d6
keywords:
- HID 报告 WDK，故障排除
- 报告 WDK HID，故障排除
- 报告 WDK HID 疑难解答
- 已删除 HID 报表 WDK
- 错误 WDK HID 报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d433ee89e0a72f0f080cd40b340648de89271cec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841551"
---
# <a name="troubleshooting-hid-reports"></a>排查 HID 报告问题





本部分介绍了在尝试提取或设置[HID 用法](hid-usages.md)时，用户模式应用程序和内核模式驱动程序可能会遇到的下列最常见问题：

[HID 报表 ID 错误](#hid-report-id-errors)

[已删除 HID 报表](#dropped-hid-reports)

### <a href="" id="hid-report-id-errors"></a>HID 报表 ID 错误

当应用程序或驱动程序从 HID 集合接收到 HID 报表时，它可以是该集合包含的任何报表（因为集合可以按任意顺序返回报表）。 **HidP\_Get * * * Xxx*例程返回以下状态值，指示报表 ID 错误：

<a href="" id="hidp-status-incompatible-report-id"></a>HIDP\_状态\_不兼容\_报表\_ID  
请求的使用情况位于 HID 集合支持的报表中，但不在应用程序或驱动程序所指定的报表中。

<a href="" id="hidp-status-usage-not-found"></a>HIDP\_状态\_使用情况\_找不到\_  
请求的使用情况不在顶级集合支持的任何报表中。

例如，下图显示了包含两个报告的 HID 集合。

![阐释包含两个报告的 hid 集合的关系图](images/reportid.png)

根据此示例，假设应用程序或驱动程序从集合接收到了一个报表，并调用[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)来提取当前值 "X"。 如果报表的 ID 为7，则例程返回 HIDP\_状态\_不兼容的\_报表\_ID，这表示设备支持值 X，但报表中不存在值 X。 另一方面，如果应用程序或驱动程序请求 "值 Z" 的值，例程将返回 HIDP\_状态\_使用情况\_未找到\_，这表示值 Z 不在集合支持的任何报表中。

当应用程序或驱动程序使用 **HidP\_集 * * * Xxx*例程来设置报表中的用法时，这些例程还可以返回相同的两个状态值。 找\_不到\_状态\_用法\_的含义与使用 **HIDP\_Get * * * Xxx*例程相同。 但是，HIDP\_状态\_不兼容\_报表\_ID 的含义是不同的。 此状态值指示报表以前配置了报表 ID，并且调用方指定的使用不属于该报表 ID。 使用上图作为示例，在应用程序或驱动程序使用[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)将 "Button 2" 设置为零初始化报表后，报表将配置为报表 ID 7。 如果应用程序或驱动程序随后尝试使用[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)在同一报表中设置 "值 X"，则例程将返回 HIDP\_状态\_不兼容\_报表\_ID。

如果**HidP\_** <em>XXX</em>例程返回 HIDP\_状态\_不兼容\_报表\_ID，则调用方应执行下列操作之一：

-   如果调用方正在设置用法，则它应分配正确长度的新报表，对其进行零初始化，然后再次调用例程。 在成功设置报表中的所有用法后，调用方可以将报表发送到集合。

-   如果调用方正在提取用法，则应使用从集合获取的不同报表来调用例程。

### <a href="" id="dropped-hid-reports"></a>已删除 HID 报表

当[Hid 客户端驱动程序](hid-client-drivers.md)从 hid 集合获取输入报告时，报告存储在由 hid 类驱动程序维护的环形缓冲区中。 此机制可降低应用程序或驱动程序丢失所需的输入报告的可能性。

默认情况下，HID 类驱动程序维护一个包含32报告的输入报告环形缓冲区。 如果集合将数据传输到 HID 类驱动程序的速度比用户模式应用程序或内核模式驱动程序更快，则会因为缓冲区溢出而导致输入报告丢失。 为了降低缓冲区溢出的可能性，应用程序或驱动程序可以重新配置缓冲区的大小（以报表数为限）。 驱动程序使用 IOCTL 检索和更改缓冲区的大小[ **\_获取\_NUM\_设备\_输入\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_get_num_device_input_buffers)请求和 IOCTL\_\_\_[ **\_@no__t_ 输入13_ 缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_set_num_device_input_buffers)请求。 应用程序通过调用[**HidD\_GetNumInputBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)和[**HidD\_SetNumInputBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)来执行相同的操作。

 

 




