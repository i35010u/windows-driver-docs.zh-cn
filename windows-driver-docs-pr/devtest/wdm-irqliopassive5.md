---
title: 'IrqlIoPassive5 规则 (wdm) '
description: IrqlIoPassive5 规则指定，仅当驱动程序在 IRQL PASSIVE_LEVEL 执行时，该驱动程序才调用特定的 i/o 管理器例程。
ms.assetid: 07037cf2-37eb-4045-9588-ac10e79b9c5c
ms.date: 05/21/2018
keywords:
- 'IrqlIoPassive5 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlIoPassive5
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a80a24b2469a0772ab3571024de46aa03e49af77
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382789"
---
# <a name="irqliopassive5-rule-wdm"></a>IrqlIoPassive5 规则 (wdm) 


**IrqlIoPassive5**规则指定，仅当驱动程序以 IRQL = 被动级别执行时，驱动程序才调用特定的 I/o 管理器例程 \_ 。

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x0002000E) 


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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlIoPassive5</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**IoGetConfigurationInformation**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetconfigurationinformation) 
[**Plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer) 
[**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter) 
[**IoGetFileObjectGenericMapping**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetfileobjectgenericmapping) 
[**IoInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer) 
[**IoIsWdmVersionAvailable**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable) 
[**IoRegisterDriverReinitialization**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization) 
[**IoRegisterShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification) 
[**IoRemoveShareAccess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioremoveshareaccess) 
[**IoSetShareAccess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetshareaccess) 
[**IoUnregisterShutdownNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregistershutdownnotification) 
[**IoUpdateShareAccess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioupdateshareaccess) 
[**IoWMIAllocateInstanceIds**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiallocateinstanceids) 
[**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)
 

