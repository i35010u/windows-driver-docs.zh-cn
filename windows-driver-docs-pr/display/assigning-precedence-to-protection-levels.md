---
title: 将优先级分配给保护级别
description: 将优先级分配给保护级别
ms.assetid: 87a63d30-4aa2-4835-87bc-1acb062bde26
keywords:
- 保护级别 WDK 显示分配的优先级
- 保护级别 WDK 显示 ACP 优先顺序
- 保护级别 WDK 显示 CGMS 的优先顺序
- 保护级别 WDK 显示 HDCP 优先顺序
- 保护级别 WDK 显示 DPCP 优先顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9b55f594291ec36d8e6c400ce03aeb59994d001
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546610"
---
# <a name="assigning-precedence-to-protection-levels"></a>将优先级分配给保护级别


优先级值分配给每个保护级别的每种保护类型。 这样一来，物理输出可以确定要使用如果两个或多个受保护的输出是与物理输出相关联，并且每个受保护的输出具有不同的保护级别的保护级别。

Microsoft DirectX 图形内核子系统 (*Dxgkrnl.sys*) 可以进行到显示微型端口驱动程序的多个调用[ **DxgkDdiOPMCreateProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559705)若要创建多个受保护的输出为特定的物理输出的函数。 此外，每个这些受保护的输出可以具有相同的输出保护类型的不同保护级别。

例如，假设图形适配器具有一个复合输出具有 CGMS 的保护类型，并受保护的输出 A 和 B 都与该复合输出相关联。 接下来，假设输出 A 的受保护的[ **CGMS 一个保护级别**](https://msdn.microsoft.com/library/windows/hardware/ff560846)设置为 DXGKMDT\_OPM\_CGMSA\_复制\_否\_更尽管受保护的输出 B 的 CGMS 一个保护级别设置为 DXGKMDT\_OPM\_CGMSA\_副本\_一个\_生成。 在此情况下，物理输出不能使用这两种保护级别。 因此，物理输出可以输出一次只有一个 CGMS 一个保护级别，因为物理输出必须具有高优先级使用 CGMS 一个保护级别。

以下各节显示物理输出应使用 （从最高优先级到最低优先级） 时不同的保护级别保护输出指示物理输出使用不同的保护级别。 请注意，这些表将应用于受保护包含 COPP 或 OPM 语义的输出结果。

### <a name="span-idacpprotectionlevelprecedencespanspan-idacpprotectionlevelprecedencespanacp-protection-level-precedence"></a><span id="acp_protection_level_precedence"></span><span id="ACP_PROTECTION_LEVEL_PRECEDENCE"></span>ACP 保护级别优先顺序

时不同的受保护的输出，指示要使用不同的 ACP 保护级别的物理输出，物理输出应使用的保护级别，具有较高的优先级下, 表中所示。 请注意，此表适用于受保护包含 COPP 语义的输出结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ACP 保护级别值</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_ACP_OFF (0)</p></td>
<td align="left"><p>最低优先级 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_ONE (1)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_THREE (3)</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_TWO (2)</p></td>
<td align="left"><p>最高优先级 (3)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcgmsaprotectionlevelprecedencespanspan-idcgmsaprotectionlevelprecedencespancgms-a-protection-level-precedence"></a><span id="cgms_a_protection_level_precedence"></span><span id="CGMS_A_PROTECTION_LEVEL_PRECEDENCE"></span>CGMS 一个保护级别优先顺序

时不同的受保护的输出，指示要使用不同的 CGMS 一个保护级别的物理输出，物理输出应使用的保护级别，具有较高的优先级下, 表中所示。 请注意，此表适用于受保护包含 COPP 语义的输出结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CGMS 一个保护级别值</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_OFF (0)</p></td>
<td align="left"><p>最低优先级 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_FREELY (1)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_ONE_GENERATION (3)</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_NO_MORE (2)</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_NEVER (4)</p></td>
<td align="left"><p>最高优先级 (4)</p></td>
</tr>
</tbody>
</table>

 

**请注意**  重新分发控制标志 (DXGKMDT\_OPM\_重新分发\_控制\_REQUIRED) 不会影响 CGMS 的优先顺序值。 例如，(DXGKMDT\_OPM\_CGMSA\_副本\_一个\_生成 |DXGKMDT\_OPM\_重新分发\_控件\_REQUIRED) 具有相同的优先级值 DXGKMDT\_OPM\_CGMSA\_复制\_一个\_生成。

 

### <a name="span-idhdcpprotectionlevelprecedencespanspan-idhdcpprotectionlevelprecedencespanhdcp-protection-level-precedence"></a><span id="hdcp_protection_level_precedence"></span><span id="HDCP_PROTECTION_LEVEL_PRECEDENCE"></span>HDCP 保护级别优先顺序

时不同的受保护的输出，指示要使用不同 HDCP 保护级别的物理输出，物理输出应使用的保护级别，具有较高的优先级下, 表中所示。 请注意，此表适用于受保护包含 COPP 或 OPM 语义的输出结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HDCP 保护级别值</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_HDCP_OFF (0)</p></td>
<td align="left"><p>最低优先级 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_HDCP_ON (1)</p></td>
<td align="left"><p>最高优先顺序 (1)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddpcpprotectionlevelprecedencespanspan-iddpcpprotectionlevelprecedencespandpcp-protection-level-precedence"></a><span id="dpcp_protection_level_precedence"></span><span id="DPCP_PROTECTION_LEVEL_PRECEDENCE"></span>DPCP 保护级别优先顺序

时不同的受保护的输出，指示要使用不同 DPCP 保护级别的物理输出，物理输出应使用的保护级别，具有较高的优先级下, 表中所示。 请注意，此表适用于受保护包含 OPM 语义的输出结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DPCP 保护级别值</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_DPCP_OFF (0)</p></td>
<td align="left"><p>最低优先级 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_DPCP_ON (1)</p></td>
<td align="left"><p>最高优先顺序 (1)</p></td>
</tr>
</tbody>
</table>

 

 

 





