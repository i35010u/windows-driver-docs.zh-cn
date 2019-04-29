---
title: KsCallbackReturn 规则 （)
description: KsCallbackReturn 规则指定一个内核流式处理 (KS) 微型端口驱动程序回调函数返回仅允许的状态值。
ms.assetid: 1779301C-5C2C-471F-88D8-3E5F2C90357D
ms.date: 05/21/2018
keywords:
- KsCallbackReturn 规则 （)
topic_type:
- apiref
api_name:
- KsCallbackReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f02bcdc1007a9434bca667fad3ea6c6f7af8baa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374731"
---
# <a name="kscallbackreturn-rule-"></a>KsCallbackReturn 规则 （)


KsCallbackReturn 规则指定一个内核流式处理 (KS) 微型端口驱动程序回调函数返回仅允许的状态值。

|              |     |
|--------------|-----|
| 驱动程序模型 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081005) |

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
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>请参阅
--------

[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)
[*AVStrMiniPinSetDeviceState*](https://msdn.microsoft.com/library/windows/hardware/ff556359)
[*AVStrMiniPinSetDataFormat*](https://msdn.microsoft.com/library/windows/hardware/ff556355)
 

 





