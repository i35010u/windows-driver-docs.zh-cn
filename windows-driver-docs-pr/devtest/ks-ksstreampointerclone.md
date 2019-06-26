---
title: KsStreamPointerClone 规则 （)
description: KsStreamPointerClone 规则指定内核流 (KS) 微型端口驱动程序正确使用 KsStreamPointerClone 和 KsStreamPointerDelete 函数。
ms.assetid: 5ECF0070-0E36-4A91-B9FA-AA0DB7636B0E
ms.date: 05/21/2018
keywords:
- KsStreamPointerClone 规则 （)
topic_type:
- apiref
api_name:
- KsStreamPointerClone
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5036831a5be2e766e295711a572f281c83196331
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392743"
---
# <a name="ksstreampointerclone-rule-"></a>KsStreamPointerClone 规则 （)


KsStreamPointerClone 规则指定内核流 (KS) 微型端口驱动程序正确使用[ **KsStreamPointerClone** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)并[ **KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)函数。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081002) |

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

 

 

 





