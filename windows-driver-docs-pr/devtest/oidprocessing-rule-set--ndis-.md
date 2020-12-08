---
title: OidProcessing 规则集 (NDIS)
description: 使用这些规则验证驱动程序是否正确地处理了 OID 请求。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d5230a51e0f65a836756dd050b8d7ec10d534339
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790007"
---
# <a name="oidprocessing-rule-set-ndis"></a>OidProcessing 规则集 (NDIS)


使用这些规则验证驱动程序是否正确地处理了 OID 请求。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="ndis-doublecomplete.md" data-raw-source="[DoubleComplete](ndis-doublecomplete.md)">DoubleComplete</a>规则指定 NDIS 驱动程序不得 (OID) 请求中多次完成对象标识符。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-doublecompleteworkitem.md" data-raw-source="[&lt;strong&gt;DoubleCompleteWorkItem&lt;/strong&gt;](ndis-doublecompleteworkitem.md)"><strong>DoubleCompleteWorkItem</strong></a></p></td>
<td align="left"><p>DoubleCompleteWorkItem 规则指定 NDIS 驱动程序在工作项中延迟完成时不得多次完成 OID 请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismnetpnpeventinoidrequest.md" data-raw-source="[&lt;strong&gt;NdisMNetPnPEventInOIDRequest&lt;/strong&gt;](ndis-ndismnetpnpeventinoidrequest.md)"><strong>NdisMNetPnPEventInOIDRequest</strong></a></p></td>
<td align="left"><p>此规则检查 OID 请求的上下文中是否未调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent" data-raw-source="[&lt;strong&gt;NdisMNetPnPEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)"><strong>NdisMNetPnPEvent</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**选择 OidProcessing 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **OidProcessing**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **OidProcessing。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:OidProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

