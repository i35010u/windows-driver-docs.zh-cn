---
title: 'IrqlIoPassive1 规则 (wdm) '
ms.date: 05/21/2018
description: '了解详细信息： IrqlIoPassive1 规则 (wdm) '
keywords:
- 'IrqlIoPassive1 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlIoPassive1
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f9652ab70b85d908d40e2b8921032af8db2a83df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791881"
---
# <a name="irqliopassive1-rule-wdm"></a>IrqlIoPassive1 规则 (wdm) 


**IrqlIoPassive1** 规则指定仅当驱动程序在 IRQL = 被动级别执行时才调用以下例程 \_ ：

-   [**IoAttachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)

-   [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

-   [**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

规则还指定该驱动程序仅在以下情况下才会调用以下例程： IRQL = 被动 \_ 级别或 IRQL = APC \_ 级别：

-   [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x0002000A) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlIoPassive1</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**IoAttachDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice) 
[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 
[**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 
[**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)
