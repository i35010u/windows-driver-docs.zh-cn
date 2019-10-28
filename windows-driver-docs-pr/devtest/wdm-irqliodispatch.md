---
title: IrqlIoDispatch 规则（wdm）
description: IrqlIoDispatch 规则指定驱动程序仅在以下情况下调用以下 i/o 管理器例程：在 IRQL 调度\_LEVEL IoGetDeviceToVerify，IoSetDeviceToVerify。
ms.assetid: 4794123F-EB8E-4B3D-A7DE-8E6B145AE816
ms.date: 05/21/2018
keywords:
- IrqlIoDispatch 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlIoDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24f4fcc87d19dd46cc6f774b7fb6e7b0f782033e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839928"
---
# <a name="irqliodispatch-rule-wdm"></a>IrqlIoDispatch 规则（wdm）


**IrqlIoDispatch**规则指定，仅当驱动程序 &lt;在以下情况下执行时，才调用以下 I/o 管理器例程：\_LEVEL： [**IoGetDeviceToVerify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdevicetoverify)， [**IoSetDeviceToVerify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetdevicetoverify)。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查0xC4：检测到的驱动程序\_验证程序\_\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x 0x20022） |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlIoDispatch</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="see-also"></a>另请参阅
--------

[管理硬件优先级](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)
 

 





