---
title: KsTimedPinSetDeviceState 规则 （)
description: KsTimedPinSetDeviceState 规则指定 AVStream (KS) 微型端口驱动程序，可在所需的时间内使用 AVStream 微型驱动程序的 AVStrMiniPinSetDeviceState 例程的状态转换。
ms.assetid: 2BDA0358-A3B1-4A47-AA08-8B086041BC52
ms.date: 05/21/2018
keywords:
- KsTimedPinSetDeviceState 规则 （)
topic_type:
- apiref
api_name:
- KsTimedPinSetDeviceState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 387094265ac5224db0b66ddc77954714f35d0fe1
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392721"
---
# <a name="kstimedpinsetdevicestate-rule-"></a>KsTimedPinSetDeviceState 规则 （)


KsTimedPinSetDeviceState 规则指定 AVStream (KS) 微型端口驱动程序，可使用 AVStream 微型驱动程序的状态转换[ *AVStrMiniPinSetDeviceState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)例程中所需的时间。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00082001) |

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
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>请参阅
--------

[*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)
 

 





