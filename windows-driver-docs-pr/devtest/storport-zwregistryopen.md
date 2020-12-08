---
title: 'ZwRegistryOpen 规则 (storport) '
description: 此规则验证通过 ZwOpenKey 打开的注册表项的句柄以后是否可以由其他 ZwXxx 例程正确使用。
ms.date: 05/21/2018
keywords:
- 'ZwRegistryOpen 规则 (storport) '
topic_type:
- apiref
api_name:
- ZwRegistryOpen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26fdf7ed97d969c8918d69554eaf52aaa64a8ee6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820852"
---
# <a name="zwregistryopen-rule-storport"></a>ZwRegistryOpen 规则 (storport) 


此规则验证通过 **ZwOpenKey** 打开的注册表项的句柄以后是否可以由其他 ZwXxx 例程正确使用。 不能在未打开的句柄上调用例程 **ZwEnumerateKey**、 **ZwEnumerateValueKey**、 **ZwFlushKey**、 **ZwQueryKey**、 **ZwQueryValueKey**、 **ZwSetValueKey**、 **ZwClose** 和 **ZwDeleteKey** 。 还必须在返回前关闭句柄。

**驱动程序模型： Storport**

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
[**ZwDeleteKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey) 
[**ZwEnumerateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey) 
[**ZwEnumerateValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey) 
[**ZwFlushKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey) 
[**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey) 
[**ZwQueryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey) 
[**ZwQueryValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey) 
[**ZwSetValueKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)
