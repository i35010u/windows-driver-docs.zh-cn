---
title: RemoveLockQueryMnRemove 规则（wdm）
description: RemoveLockQueryMnRemove 规则验证在 \_ \_ 使用 MinorFunction IRP \_ MN \_ 查询 \_ 删除 \_ 设备处理 IRP MJ PNP 时，对 IoAcquireRemoveLock 和 IoReleaseRemoveLock 的调用是否正确使用。
ms.assetid: 593B8305-EA61-4857-9304-A8319A8E0017
ms.date: 05/21/2018
keywords:
- RemoveLockQueryMnRemove 规则（wdm）
topic_type:
- apiref
api_name:
- RemoveLockQueryMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f8452c1ca8630daf18592fcdb880a36e3941c010
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916159"
---
# <a name="removelockquerymnremove-rule-wdm"></a>RemoveLockQueryMnRemove 规则（wdm）


**RemoveLockQueryMnRemove**规则验证在[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) \_ \_ 使用 MinorFunction IRP \_ MN \_ 查询 \_ 删除 \_ 设备处理 IRP MJ PNP 时，对 IoAcquireRemoveLock 和 IoReleaseRemoveLock 的调用是否正确使用。 在将 IRP 转发到堆栈之前，驱动程序应该获取删除锁定。

此规则仅适用于 FDO 和 FIDO 驱动程序。

例如，请考虑包含筛选器驱动程序、FDO 和 PDO 的 PnP 驱动程序堆栈。

PnP 管理器通过堆栈发送查询删除。 当系统正在运行时，FDO 已启用为空闲状态。 FDO 决定在查询删除状态下断电，因此它请求 d0 IRP。 在 d0 IRP 到达之前，PnP 管理器将发送 PnP 删除 IRP，并由筛选器驱动程序处理 IRP。 筛选器驱动程序与堆栈分离并清除其状态。 D0 到达堆栈顶部，但筛选器驱动程序不会将其发送到堆栈中，因为它没有上下文或数据来知道要将其发送到的位置。 FDO 挂起等待 d0 IRP 到达，但 IRP 永远不会。

**若要避免此错误**

1.  在设备从设备堆栈分离之前， [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)必须在将 irp 转发到以下 irp 类型的堆栈之前成功：

    -   IRP \_ MN \_ 查询 \_ 删除
    -   IRP \_ MN \_ SUPRISE \_ 删除
    -   IRP \_ MN \_ 删除 \_ 设备

2.  调用[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)或[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)之前应调用[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) 。 （这可确保在设备驱动程序中释放所有删除锁）。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>RemoveLockQueryMnRemove</strong>规则。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





