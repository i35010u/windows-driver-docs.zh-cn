---
title: 警告规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。
ms.assetid: 454FB042-76FA-4A46-9549-4DE8BF52A2D3
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 447c8318b071a6b9a24adb60208a42e3e6988300
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381778"
---
# <a name="warning-rule-set-ndis"></a>警告规则集 (NDIS)


使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。

## <a name="in-this-section"></a>本节内容


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
<td align="left"><p><a href="ndis-ndisstallexecution-delay.md" data-raw-source="[&lt;strong&gt;NdisStallExecution_Delay&lt;/strong&gt;](ndis-ndisstallexecution-delay.md)"><strong>NdisStallExecution_Delay</strong></a></p></td>
<td align="left"><p>NdisStallExecution_Delay 规则规定<strong>NdisStallExecution</strong>永远不会必须由使用的值调用<em>MicrosecondsToStall</em>大于 50 微秒为单位。</p></td>
</tr>
</tbody>
</table>

 

**若要选择警告规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**警告**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Warning.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





