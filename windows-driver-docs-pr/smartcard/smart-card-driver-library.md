---
title: 智能卡驱动程序库
description: 智能卡驱动程序库
ms.assetid: 12f67a8d-9281-4f79-88c0-e1c9dff5a05d
keywords:
- 智能卡驱动程序 WDK、 库
- 库 WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682f9bbd6f6bcacd2c2722b4315b03a1730fcae9
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349158"
---
# <a name="smart-card-driver-library"></a>智能卡驱动程序库


## <span id="_ntovr_smart_card_driver_library"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY"></span>


Microsoft 提供了一个包含一组标准化的智能卡读卡器驱动程序必须执行的函数的大部分例程的驱动程序库。 供应商提供读卡器驱动程序必须调用这些例程执行以下操作：

-   若要创建智能卡资源管理器要求的设备名称

-   若要检查参数并检测错误 IOCTL 调用

-   若要分析 ATR 字符串并将参数转换

-   若要支持 T = 0 和 T = 1 ISO 协议

-   若要支持的反约定

-   若要记录的事件

-   该驱动程序对访问进行同步

[WDM 智能卡驱动程序例程](https://msdn.microsoft.com/library/windows/hardware/ff549046)部分中，列出了驱动程序库例程并标识哪个例程执行每个操作。

驱动程序库处理大多数 IOCTL 请求的资源管理器将发送到读卡器驱动程序。 [智能卡驱动程序 Ioctl](https://msdn.microsoft.com/library/windows/hardware/ff548988)部分中，列出了 Ioctl 代表读卡器驱动程序处理驱动程序库。

通过智能卡驱动程序库和驱动程序调用智能卡驱动程序库例程，均使用下面的文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文件</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>Smclib.h</em></p></td>
<td align="left"><p>包含声明和定义所需的所有驱动程序调用智能卡库例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smcnt.h</em></p></td>
<td align="left"><p>包含声明和定义所需的调用智能卡库例程的 WDM 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Winsmcrd.h</em></p></td>
<td align="left"><p>所有智能卡读卡器驱动程序和可识别智能卡的应用程序的全局标头文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smclib.sys</em></p></td>
<td align="left"><p>用于 WDM 驱动程序库的二进制文件。</p></td>
</tr>
</tbody>
</table>

 

 

 





