---
title: KsDeviceMutex 规则 （)
description: KsDeviceMutex 规则指定流式处理微型端口驱动程序的内核使用 KsAcquireDevice 和 KsReleaseDevice 正确的顺序。 也就是说，KsAcquireDevice 的每个调用都必须具有 KsReleaseDevice 相应地调用。
ms.assetid: 6F69B273-6780-4A01-8266-2B056E4F2C84
ms.date: 05/21/2018
keywords:
- KsDeviceMutex 规则 （)
topic_type:
- apiref
api_name:
- KsDeviceMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16024a3114bd768034bd450a76f9818491578577
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392782"
---
# <a name="ksdevicemutex-rule-"></a>KsDeviceMutex 规则 （)


**KsDeviceMutex**规则指定流式处理微型端口驱动程序的内核使用[ **KsAcquireDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksacquiredevice)并[ **KsReleaseDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksreleasedevice)正确的顺序。 也就是说，每次调用**KsAcquireDevice**必须具有相应地调用**KsReleaseDevice**。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081001) |

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

 

 

 





