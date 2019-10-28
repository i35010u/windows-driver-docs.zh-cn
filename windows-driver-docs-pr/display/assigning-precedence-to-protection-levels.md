---
title: 将优先顺序分配到保护级别
description: 将优先顺序分配到保护级别
ms.assetid: 87a63d30-4aa2-4835-87bc-1acb062bde26
keywords:
- 保护级别，WDK 显示，分配优先级
- 保护级别 WDK 显示，ACP 优先级
- 保护级别 WDK 显示，CGMS-优先
- 保护级别 WDK 显示，HDCP 优先级
- 保护级别 WDK 显示，DPCP 优先级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcdfb06305c196c9eb4abdc834a0b414f2331652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839828"
---
# <a name="assigning-precedence-to-protection-levels"></a>将优先顺序分配到保护级别


为每个保护类型的每个保护级别分配一个优先级值。 这样一来，如果两个或多个受保护的输出与物理输出相关联，并且每个受保护的输出都有不同的保护级别，则物理输出可以确定要使用的保护级别。

Microsoft DirectX 图形内核子系统（*Dxgkrnl*）可对显示微型端口驱动程序的[**DxgkDdiOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)函数进行多个调用，以为特定物理输出创建多个受保护的输出。 此外，其中每个受保护的输出对于同一输出保护类型可能有不同的保护级别。

例如，假设图形适配器具有一个具有 CGMS 保护类型的复合输出，并且受保护的输出 A 和 B 均与该复合输出相关联。 接下来，假定受保护的输出 A 的[**CGMS-A 保护级别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)设置为 DXGKMDT\_OPM\_CGMSA\_在受保护的输出 B 的 CGMS 时，\_no\_; 保护级别设置为 DXGKMDT\_OPM\_CGMSA\_复制\_一个\_代。 在这种情况下，物理输出不能同时使用这两种保护级别。 因此，因为物理输出每次只能输出一 CGMS 保护级别，所以物理输出必须使用具有较高优先级的 CGMS 保护级别。

以下各节说明了当不同的受保护的输出指示物理输出使用不同的保护级别时，物理输出应使用哪种保护级别（从最高到最低的优先级）。 请注意，这些表适用于具有 COPP 或 OPM 语义的受保护的输出。

### <a name="span-idacp_protection_level_precedencespanspan-idacp_protection_level_precedencespanacp-protection-level-precedence"></a><span id="acp_protection_level_precedence"></span><span id="ACP_PROTECTION_LEVEL_PRECEDENCE"></span>ACP 保护级别优先级

当不同的保护输出指示物理输出使用不同的 ACP 保护级别时，物理输出应使用优先级较高的保护级别，如下表所示。 请注意，此表适用于带有 COPP 语义的受保护的输出。

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
<td align="left"><p>DXGKMDT_OPM_ACP_OFF （0）</p></td>
<td align="left"><p>最低优先级（0）</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_ONE （1）</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_THREE （3）</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_TWO （2）</p></td>
<td align="left"><p>最高优先级（3）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcgms_a_protection_level_precedencespanspan-idcgms_a_protection_level_precedencespancgms-a-protection-level-precedence"></a><span id="cgms_a_protection_level_precedence"></span><span id="CGMS_A_PROTECTION_LEVEL_PRECEDENCE"></span>CGMS-保护级别优先级

当不同的保护输出指示物理输出使用不同的 CGMS 保护级别时，物理输出应使用优先级较高的保护级别，如下表所示。 请注意，此表适用于带有 COPP 语义的受保护的输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CGMS-保护级别值</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_OFF （0）</p></td>
<td align="left"><p>最低优先级（0）</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_FREELY （1）</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_ONE_GENERATION （3）</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_NO_MORE （2）</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_NEVER （4）</p></td>
<td align="left"><p>最高优先级（4）</p></td>
</tr>
</tbody>
</table>

 

**请注意**   重新分发控制标志（DXGKMDT\_OPM\_重新分发\_控制\_必需）不影响 CGMS-优先级值。 例如，（DXGKMDT\_OPM\_CGMSA\_复制\_一\_代 |DXGKMDT\_OPM\_\_控制\_必需的）的优先级值与 DXGKMDT\_OPM\_CGMSA\_COPY\_\_生成的优先级相同。

 

### <a name="span-idhdcp_protection_level_precedencespanspan-idhdcp_protection_level_precedencespanhdcp-protection-level-precedence"></a><span id="hdcp_protection_level_precedence"></span><span id="HDCP_PROTECTION_LEVEL_PRECEDENCE"></span>HDCP 保护级别优先级

当不同的保护输出指示物理输出使用不同的 HDCP 保护级别时，物理输出应使用优先级较高的保护级别，如下表所示。 请注意，此表适用于具有 COPP 或 OPM 语义的受保护的输出。

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
<td align="left"><p>DXGKMDT_OPM_HDCP_OFF （0）</p></td>
<td align="left"><p>最低优先级（0）</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_HDCP_ON （1）</p></td>
<td align="left"><p>最高优先级别（1）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddpcp_protection_level_precedencespanspan-iddpcp_protection_level_precedencespandpcp-protection-level-precedence"></a><span id="dpcp_protection_level_precedence"></span><span id="DPCP_PROTECTION_LEVEL_PRECEDENCE"></span>DPCP 保护级别优先级

当不同的保护输出指示物理输出使用不同的 DPCP 保护级别时，物理输出应使用优先级较高的保护级别，如下表所示。 请注意，此表适用于带有 OPM 语义的受保护的输出。

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
<td align="left"><p>DXGKMDT_OPM_DPCP_OFF （0）</p></td>
<td align="left"><p>最低优先级（0）</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_DPCP_ON （1）</p></td>
<td align="left"><p>最高优先级别（1）</p></td>
</tr>
</tbody>
</table>

 

 

 





