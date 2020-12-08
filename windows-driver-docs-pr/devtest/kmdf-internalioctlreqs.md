---
title: 'InternalIoctlReqs 规则 (kmdf) '
description: InternalIoctlReqs 规则指定内部 IOCTL 请求不会传递到不适当的 KMDF 请求-发送设备驱动程序接口 (DDIs) 。
ms.date: 05/21/2018
keywords:
- 'InternalIoctlReqs 规则 (kmdf) '
topic_type:
- apiref
api_name:
- InternalIoctlReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4e0e949f98823a4f1a16b24d352b270b2ba7971
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841299"
---
# <a name="internalioctlreqs-rule-kmdf"></a>InternalIoctlReqs 规则 (kmdf) 


**InternalIoctlReqs** 规则指定内部 IOCTL 请求不会传递到不适当的 KMDF 请求-发送设备驱动程序接口 (DDIs) 。

在 .EVT \_ WDF \_ io \_ QUEUE io 内部设备控制回调函数中提供给驱动程序的所有请求 \_ \_ \_ \_ 都保证为内部 IOCTL 请求。 因此，不能使用特定于发送读取、写入或 IOCTL 请求的 DDIs （如 **WdfIoTargetSendReadSynchronously**、 **WdfIoTargetSendWriteSynchronously**、 **WdfIoTargetSendIoctlSynchronously**、 **WdfUsbTargetPipeWriteSynchronously**）发送这些 IOCTLs。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>InternalIoctlReqs</strong> 规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**WdfIoTargetSendIoctlSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 
[**WdfIoTargetSendReadSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously) 
[**WdfIoTargetSendWriteSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously) 
[**WdfUsbTargetPipeReadSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously) 
[**WdfUsbTargetPipeWriteSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)
