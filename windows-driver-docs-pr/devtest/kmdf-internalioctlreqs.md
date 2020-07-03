---
title: InternalIoctlReqs 规则（kmdf）
description: InternalIoctlReqs 规则指定内部 IOCTL 请求不会传递到不适当的 KMDF 请求-发送设备驱动程序接口（DDIs）。
ms.assetid: a6d75752-21eb-486b-b73a-8d810b392e6b
ms.date: 05/21/2018
keywords:
- InternalIoctlReqs 规则（kmdf）
topic_type:
- apiref
api_name:
- InternalIoctlReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0cfea2f1b012483d915258794a46de470774746d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916985"
---
# <a name="internalioctlreqs-rule-kmdf"></a>InternalIoctlReqs 规则（kmdf）


**InternalIoctlReqs**规则指定内部 IOCTL 请求不会传递到不适当的 KMDF 请求-发送设备驱动程序接口（DDIs）。

在 .EVT \_ WDF \_ io \_ QUEUE io 内部设备控制回调函数中提供给驱动程序的所有请求 \_ \_ \_ \_ 都保证为内部 IOCTL 请求。 因此，不能使用特定于发送读取、写入或 IOCTL 请求的 DDIs （如**WdfIoTargetSendReadSynchronously**、 **WdfIoTargetSendWriteSynchronously**、 **WdfIoTargetSendIoctlSynchronously**、 **WdfUsbTargetPipeWriteSynchronously**）发送这些 IOCTLs。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>InternalIoctlReqs</strong>规则。</p>
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

[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 
[**WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously) 
[**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously) 
[**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously) 
[**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)
 

 





