---
title: OidProcessing 规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序正确处理 OID 请求。
ms.assetid: 0E12778B-BB86-4387-9B8A-19E3876D6F8C
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e762c59c2d2dd2c5ad79108c028be473d3167e0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554811"
---
# <a name="oidprocessing-rule-set-ndis"></a>OidProcessing 规则集 (NDIS)


使用这些规则来验证您的驱动程序正确处理 OID 请求。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-doublecomplete.md" data-raw-source="[&lt;strong&gt;DoubleComplete&lt;/strong&gt;](ndis-doublecomplete.md)"><strong>DoubleComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-doublecomplete.md" data-raw-source="[DoubleComplete](ndis-doublecomplete.md)">DoubleComplete</a>规则指定的 NDIS 驱动程序必须完成的对象标识符 (OID) 请求多个时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-doublecompleteworkitem.md" data-raw-source="[&lt;strong&gt;DoubleCompleteWorkItem&lt;/strong&gt;](ndis-doublecompleteworkitem.md)"><strong>DoubleCompleteWorkItem</strong></a></p></td>
<td align="left"><p>DoubleCompleteWorkItem 规则指定，NDIS 驱动程序必须完成的 OID 请求多个时间时完成延迟为工作项中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismnetpnpeventinoidrequest.md" data-raw-source="[&lt;strong&gt;NdisMNetPnPEventInOIDRequest&lt;/strong&gt;](ndis-ndismnetpnpeventinoidrequest.md)"><strong>NdisMNetPnPEventInOIDRequest</strong></a></p></td>
<td align="left"><p>此规则检查<a href="https://msdn.microsoft.com/library/windows/hardware/ff563616" data-raw-source="[&lt;strong&gt;NdisMNetPnPEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563616)"> <strong>NdisMNetPnPEvent</strong> </a> OID 请求的上下文中未调用。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 OidProcessing 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**OidProcessing**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**OidProcessing.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:OidProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





