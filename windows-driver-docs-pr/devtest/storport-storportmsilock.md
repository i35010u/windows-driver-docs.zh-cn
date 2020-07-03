---
title: StorPortMSILock 规则（storport）
description: 如果仅当端口 \_ 配置 \_ 信息（Storport）结构的 InterruptSynchronizationMode 成员设置为 InterruptSynchronizePerMessage，则需要使用微型端口驱动程序获取消息的 MSI 旋转锁。
ms.assetid: 99C45ADB-AFCC-4B9E-8EB9-DBD7C7F6D800
ms.date: 05/21/2018
keywords:
- StorPortMSILock 规则（storport）
topic_type:
- apiref
api_name:
- StorPortMSILock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9caf2ea799269b5cd5a1462b7db985bb211e6180
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917172"
---
# <a name="storportmsilock-rule-storport"></a>StorPortMSILock 规则（storport）


如果仅当[**端口 \_ 配置 \_ 信息（Storport）**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))结构的**InterruptSynchronizationMode**成员设置为**InterruptSynchronizePerMessage**，则需要使用微型端口驱动程序获取消息的 MSI 旋转锁。 此规则验证当同步模式为**InterruptSynchronizePerMessage**时，是否仅对[**StorPortAcquireMSISpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquiremsispinlock)进行调用。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>StorPortMSILock</strong>规则。</p>
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

 

 





