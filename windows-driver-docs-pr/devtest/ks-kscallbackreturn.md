---
title: KsCallbackReturn 规则（）
description: KsCallbackReturn 规则指定内核流式处理（KS）微型端口驱动程序回调函数只返回允许的状态值。
ms.assetid: 1779301C-5C2C-471F-88D8-3E5F2C90357D
ms.date: 05/21/2018
keywords:
- KsCallbackReturn 规则（）
topic_type:
- apiref
api_name:
- KsCallbackReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73d227ef69922a23a17c7ce6d9b47b0f8f0eca56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839425"
---
# <a name="kscallbackreturn-rule-"></a>KsCallbackReturn 规则（）


KsCallbackReturn 规则指定内核流式处理（KS）微型端口驱动程序回调函数只返回允许的状态值。

|              |     |
|--------------|-----|
| 驱动程序型号 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：检测到\_冲突的驱动程序\_验证程序\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （0x00081005） |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>另请参阅
--------

[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)
[*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)
[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)
 

 





