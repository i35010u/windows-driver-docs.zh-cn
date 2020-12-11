---
title: 智能卡驱动程序库
description: 智能卡驱动程序库
keywords:
- 智能卡驱动程序 WDK，库
- 库 WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08283dcecc1e9456f392d5b1b49b863d1740e2df
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090976"
---
# <a name="smart-card-driver-library"></a>智能卡驱动程序库


## <span id="_ntovr_smart_card_driver_library"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY"></span>


Microsoft 提供了一个驱动程序库，其中包含一组用于标准化智能卡读卡器驱动程序必须执行的大部分功能的例程。 供应商提供的读取器驱动程序必须调用这些例程才能执行以下操作：

-   创建智能卡资源管理器所需的设备名称

-   检查参数并检测 IOCTL 调用的错误

-   分析 ATR 并转换参数

-   支持 T = 0 和 T = 1 ISO 协议

-   支持反向约定

-   记录事件

-   同步对驱动程序的访问

" [WDM 智能卡驱动程序例程](/previous-versions/ff549046(v=vs.85)) " 部分列出了驱动程序库例程，并标识了执行每个操作的例程。

驱动程序库处理资源管理器发送到读取器驱动程序的大部分 IOCTL 请求。 " [智能卡驱动程序 IOCTLs](/windows-hardware/drivers/ddi/winsmcrd) " 部分列出了驱动程序库代表读取器驱动程序处理的 IOCTLs。

以下文件由智能卡驱动程序库和调用智能卡驱动程序库例程的驱动程序使用。

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
<td align="left"><p><em>Smclib</em></p></td>
<td align="left"><p>包含调用智能卡库例程的所有驱动程序所需的声明和定义。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smcnt</em></p></td>
<td align="left"><p>包含 WDM 驱动程序调用智能卡库例程所需的声明和定义。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Winsmcrd</em></p></td>
<td align="left"><p>所有智能卡读卡器驱动程序和智能卡感知应用程序的全局头文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Smclib.sys</em></p></td>
<td align="left"><p>用于 WDM 驱动程序的库的二进制文件。</p></td>
</tr>
</tbody>
</table>

 

 

