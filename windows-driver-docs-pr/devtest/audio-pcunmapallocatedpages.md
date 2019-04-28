---
title: PcUnmapAllocatedPages 规则 （音频）
description: PcUnmapAllocatedPages 规则指定 PortCls 微型端口驱动程序不会映射当前映射而无需第一个取消映射 MDL。PortCls 微型端口驱动程序取消映射的内存之前释放它使用 IMiniportWaveRTStream 接口。
ms.assetid: 0ADF523C-9480-4AD2-8B98-23C95571CB0B
ms.date: 05/21/2018
keywords:
- PcUnmapAllocatedPages 规则 （音频）
topic_type:
- apiref
api_name:
- PcUnmapAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c246b6dd5dade792113289a5840e30cc9604a540
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343103"
---
# <a name="pcunmapallocatedpages-rule-audio"></a>PcUnmapAllocatedPages 规则 （音频）


PcUnmapAllocatedPages 规则指定：

-   PortCls 微型端口驱动程序不会映射当前映射而无需第一个取消映射 MDL。
-   PortCls 微型端口驱动程序取消映射之前释放其使用的内存[IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)接口。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071004) |

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
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





