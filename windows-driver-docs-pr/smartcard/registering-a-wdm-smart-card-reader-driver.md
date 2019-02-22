---
title: 注册 WDM 智能卡读卡器驱动程序
description: 注册 WDM 智能卡读卡器驱动程序
ms.assetid: 0f82c18b-3bbc-4bc6-825a-58e957f4e3aa
keywords:
- 智能卡驱动程序 WDK、 注册表
- 注册表 WDK 智能卡
- WDM 设备注册 WDK 智能卡
- 注册智能卡驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21003952ed0e6527b9e25b78b51a6175ba4ce128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542006"
---
# <a name="registering-a-wdm-smart-card-reader-driver"></a>注册 WDM 智能卡读卡器驱动程序


## <span id="_ntovr_registering_a_wdm_smart_card_reader_driver"></span><span id="_NTOVR_REGISTERING_A_WDM_SMART_CARD_READER_DRIVER"></span>


若要使智能卡读卡器驱动程序到设备管理器中可见，必须将以下项下的指明的注册表值：

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\**<em>SmartCardDriver</em>

下表列出了所需的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注册表值名称</th>
<th align="left">注册表值的内容</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>开始</strong></p></td>
<td align="left"><p><strong>DWORD:0x0000002</strong></p></td>
<td align="left"><p>值为 2 可自动启动的驱动程序。 在开发期间，使用<strong>启动</strong>值为 3 以使驱动程序手动启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Type</strong></p></td>
<td align="left"><p><strong>DWORD:0x0000001</strong></p></td>
<td align="left"><p>如果值为 1 标识为内核模式驱动程序的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>组合</strong></p></td>
<td align="left"><p><strong>SmartCardReader</strong></p></td>
<td align="left"><p>每个驱动程序必须是属于<strong>SmartCardReader</strong>安装程序类，因为智能卡资源管理器在等待此类，以开始。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ErrorControl</strong></p></td>
<td align="left"><p><strong>DWORD:0x0000001</strong></p></td>
<td align="left"><p>值为 1 显示一条错误消息，如果该驱动程序无法加载，但允许继续启动系统。</p></td>
</tr>
</tbody>
</table>

 

 

 





