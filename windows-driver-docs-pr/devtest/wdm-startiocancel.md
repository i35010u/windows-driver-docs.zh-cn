---
title: StartIoCancel 规则（wdm）
description: StartIoCancel 规则指定，在使用非 NULLCancel 例程调用 IoSetCancelRoutine 之前，驱动程序不得调用 IoSetStartIoAttributes，并将 NonCancelable 参数设置为 FALSE。
ms.assetid: 08fde0b1-4f4e-473a-9e07-3b39683a3a1b
ms.date: 05/21/2018
keywords:
- StartIoCancel 规则（wdm）
topic_type:
- apiref
api_name:
- StartIoCancel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b6f7856904595e40848c1df8f52026e6be1c84d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917845"
---
# <a name="startiocancel-rule-wdm"></a>StartIoCancel 规则（wdm）


**StartIoCancel**规则指定，在使用非**NULL**[**Cancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)之前，驱动程序不得调用[**IoSetStartIoAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes) ，并将*NonCancelable*参数设置为**FALSE** 。

在注册[**取消**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程之前，将*NonCancelable*参数设置为**FALSE**可能会导致取消争用情况。

由于驱动程序的[**Cancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程必须包括对[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))的调用（以释放 i/o 管理器在调用**取消**例程之前获取的旋转锁），因此请考虑使用**StartIoCancel**规则和[**CancelSpinLock**](wdm-cancelspinlock.md)规则验证驱动程序。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>StartIoCancel</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) 
[**IoSetStartIoAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)另请参阅
--------

[**CancelSpinLock**](wdm-cancelspinlock.md)
 

 





