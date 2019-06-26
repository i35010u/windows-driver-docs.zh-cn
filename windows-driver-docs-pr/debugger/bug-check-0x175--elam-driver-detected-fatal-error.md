---
title: Bug 检查 0x178 ELAM_DRIVER_DETECTED_FATAL_ERROR
description: ELAM_DRIVER_DETECTED_FATAL_ERROR bug 检查具有 0x00000178 值。 这表示 ELAM 驱动程序检测到一个错误。
ms.assetid: 4D37FE16-0189-426C-8015-9F14DA3C52F6
keywords:
- Bug 检查 0x178 ELAM_DRIVER_DETECTED_FATAL_ERROR
- ELAM_DRIVER_DETECTED_FATAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ELAM_DRIVER_DETECTED_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1da1334d6d85780ad08b5f72e536b8e1dac842b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362104"
---
# <a name="bug-check-0x178-elamdriverdetectedfatalerror"></a>Bug 检查 0x178：ELAM\_DRIVER\_DETECTED\_FATAL\_ERROR


ELAM\_驱动程序\_已检测\_致命错误\_错误 bug 检查的值为 0x00000178。 这表示 ELAM 驱动程序检测到一个错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="elamdriverdetectedfatalerror-parameters"></a>ELAM\_驱动程序\_已检测\_致命错误\_错误参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">失败的类型。
<p>0x0:不会撤消 TPM 证明</p>
2-指向 BDCB_IMAGE_INFORMATION 结构的驱动程序正在检查 3-TBS_RESULT 失败代码
<p>0x10000:ELAM 供应商定义失败</p>
2-（可选） ELAM 供应商提供的值为 3-（可选） ELAM 供应商提供值</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">（可选）ELAM 供应商提供的常规用途数据块</td>
</tr>
</tbody>
</table>

 

 

 




