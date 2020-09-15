---
title: 'NdisMRegisterIoPortRange 规则 (ndis) '
description: 微型端口驱动程序从其 MiniportInitializeEx 或微型端口 \_ 添加 \_ 设备功能调用 NdisMRegisterIoPortRange。 MiniportInitializeEx 或微型端口 \_ 添加 \_ 设备必须先调用 NdisMSetMiniportAttributes，然后才能调用 NdisMRegisterIoPortRange。
ms.assetid: 74CFCBDB-3044-4447-ABEF-A60BA31C0BE0
ms.date: 05/21/2018
keywords:
- 'NdisMRegisterIoPortRange 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisMRegisterIoPortRange
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a6d4dc7aee5aaf2e3025b95f756295113c6a7e0d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102242"
---
# <a name="ndismregisterioportrange-rule-ndis"></a>NdisMRegisterIoPortRange 规则 (ndis) 


微型端口驱动程序从其[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)或微型端口[**NdisMRegisterIoPortRange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange) \_ 添加 \_ 设备功能调用 NdisMRegisterIoPortRange。 *MiniportInitializeEx* 或微型端口 \_ 添加 \_ 设备必须先调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，然后才能调用 **NdisMRegisterIoPortRange**。

**驱动程序模型： NDIS**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>NdisMRegisterIoPortRange</strong> 规则。</p>
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

[**NdisMRegisterIoPortRange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange) 
[ **NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)
