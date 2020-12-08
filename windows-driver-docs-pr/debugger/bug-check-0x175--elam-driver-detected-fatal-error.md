---
title: Bug 检查 0x178 ELAM_DRIVER_DETECTED_FATAL_ERROR
description: ELAM_DRIVER_DETECTED_FATAL_ERROR bug 检查的值为0x00000178。 这表明 ELAM 驱动程序检测到错误。
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
ms.openlocfilehash: 0c7f5dd59b81e9bc05b5e85112b2a4506145b991
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791637"
---
# <a name="bug-check-0x178-elam_driver_detected_fatal_error"></a>Bug 检查0x178： ELAM \_ 驱动程序 \_ 检测到 \_ \_ 错误


ELAM \_ 驱动程序 \_ 检测 \_ 到 \_ 错误 bug 检查的值为0x00000178。 这表明 ELAM 驱动程序检测到错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="elam_driver_detected_fatal_error-parameters"></a>ELAM \_ 驱动程序 \_ 检测到 \_ \_ 错误参数


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
<p>0x0：无法撤消 TPM 证明</p>
2-指向要检查的驱动程序的 BDCB_IMAGE_INFORMATION 结构的指针 3-TBS_RESULT 故障代码
<p>0x10000： ELAM-供应商定义的失败</p>
2- (可选) ELAM 供应商提供的值 3- (可选) ELAM 供应商提供的值</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left"> (可选) ELAM 供应商提供的常规用途数据块</td>
</tr>
</tbody>
</table>

 

 

 




