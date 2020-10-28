---
title: 'ZwRegistryOpen 规则 (wdm) '
ms.assetid: c98682c3-0d38-4d5b-9649-7574106f9ce3
ms.date: 05/21/2018
description: '了解详细信息： ZwRegistryOpen 规则 (wdm) '
keywords:
- 'ZwRegistryOpen 规则 (wdm) '
topic_type:
- apiref
api_name:
- ZwRegistryOpen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4feb78f1e6f98b2a83a816e4024ceaf2bc1a40be
ms.sourcegitcommit: f47c072e88dce59daba1231027b60eb56bd2cde9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92689372"
---
# <a name="zwregistryopen-rule-wdm"></a>ZwRegistryOpen 规则 (wdm) 


[**ZwRegistryOpen**](storport-zwregistryopen.md)规则指定在调用 [**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)之后，驱动程序只会在将打开的句柄保存到注册表项 (的情况下，在调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)或 [**ZwDeleteKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)) 之前调用以下注册表函数：

-   [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)

-   [**ZwDeleteKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)

-   [**ZwEnumerateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)

-   [**ZwEnumerateValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)

-   [**ZwFlushKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey)

-   [**ZwQueryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)

-   [**ZwQueryValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)

-   [**ZwSetValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)

此规则还指定如果驱动程序已拥有该注册表项的开放句柄，则不能调用 [**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey) 。

最后，此规则指定驱动程序在将打开的句柄保存到注册表项时，不能从调度例程或取消例程中返回。

此规则不会验证驱动程序在调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 或 [**ZwDeleteKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)时是否为正确的注册表项保存了一个打开的句柄。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ZwRegistryOpen</strong> 规则。</p>
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

[**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 
[**ZwCreateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey) 
[**ZwDeleteKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey) 
[**ZwEnumerateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey) 
[**ZwEnumerateValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey) 
[**ZwFlushKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey) 
[**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey) 
[**ZwQueryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey) 
[**ZwQueryValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey) 
[**ZwSetValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)另请参阅
--------

[**ZwRegistryCreate**](wdm-zwregistrycreate.md)
