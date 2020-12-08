---
title: 注册 WDM 智能卡读卡器驱动程序
description: 注册 WDM 智能卡读卡器驱动程序
keywords:
- 智能卡驱动程序 WDK，注册表
- 注册表 WDK 智能卡
- WDM 设备注册 WDK 智能卡
- 注册智能卡驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b510ca06c85ab81dd41e25f5d9a445ffe4acab99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811897"
---
# <a name="registering-a-wdm-smart-card-reader-driver"></a>注册 WDM 智能卡读卡器驱动程序


## <span id="_ntovr_registering_a_wdm_smart_card_reader_driver"></span><span id="_NTOVR_REGISTERING_A_WDM_SMART_CARD_READER_DRIVER"></span>


若要使智能卡读卡器驱动程序对设备管理器可见，你必须将指示的注册表值放在以下注册表项下：

**HKEY \_LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services \\**<em>SmartCardDriver</em>

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
<td align="left"><p><strong>启动</strong></p></td>
<td align="left"><p><strong>DWORD：0x0000002</strong></p></td>
<td align="left"><p>如果值为2，则驱动程序将自动启动。 在开发过程中，请使用 <strong>Start</strong> 值3以手动启动驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>类型</strong></p></td>
<td align="left"><p><strong>DWORD：0x0000001</strong></p></td>
<td align="left"><p>如果值为1，则将驱动程序标识为内核模式驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>组</strong></p></td>
<td align="left"><p><strong>SmartCardReader</strong></p></td>
<td align="left"><p>每个驱动程序都必须是 <strong>SmartCardReader</strong> 安装程序类的成员，因为智能卡资源管理器会等待此类启动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ErrorControl</strong></p></td>
<td align="left"><p><strong>DWORD：0x0000001</strong></p></td>
<td align="left"><p>如果驱动程序未能加载，则值1显示错误消息，但允许系统继续启动。</p></td>
</tr>
</tbody>
</table>

 

 

 





