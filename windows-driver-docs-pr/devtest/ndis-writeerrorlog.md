---
title: WriteErrorLog 规则（ndis）
description: WriteErrorLog 规则指定在 MiniportInitializeEx 函数中调用 NdisMAllocateSharedMemory 函数时，如果分配失败，驱动程序还应调用 NdisWriteErrorLogEntry。
ms.assetid: b626f25a-3101-4c0a-b0a9-fef6ce964055
ms.date: 05/21/2018
keywords:
- WriteErrorLog 规则（ndis）
topic_type:
- apiref
api_name:
- WriteErrorLog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cc3f196f81ef90fba7b565cbae41aacec22b9cc8
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917837"
---
# <a name="writeerrorlog-rule-ndis"></a>WriteErrorLog 规则（ndis）


WriteErrorLog 规则指定在*MiniportInitializeEx*函数中调用**NdisMAllocateSharedMemory**函数时，如果分配失败，驱动程序还应调用**NdisWriteErrorLogEntry** 。

通常情况下，只要分配内存操作失败，就可以在日志中记录错误条目。 大多数分配操作都在*MiniportInitializeEx*回调函数中发生。 有关如何记录错误的详细信息，请参阅下面的代码示例。

**驱动程序模型： NDIS**

<a name="example"></a>示例
-------

```
// an example of how to log an error if memory allocation fails PVOID p;
NdisMAllocateSharedMemory(par1, par2, par3, &p, ...);
if (p == NULL)
{
 NdisWriteErrorLogEntry("Memory allocation failed");
}
```

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>WriteErrorLog</strong>规则。</p>
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

 

 





