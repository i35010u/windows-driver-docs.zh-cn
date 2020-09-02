---
title: 'StorPortBuildIo 规则 (storport) '
description: 此规则验证如果 StorPort 微型端口的 StorPortBuildIo 例程返回 FALSE，则不会将相关 SRB 传递到 StartIo。
ms.assetid: C35954F9-9C59-408B-BF80-2B8DCD328F9C
ms.date: 05/21/2018
keywords:
- 'StorPortBuildIo 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortBuildIo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 180a728d296105c4a446f0403f73809a6efb331e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382568"
---
# <a name="storportbuildio-rule-storport"></a>StorPortBuildIo 规则 (storport) 


此规则验证如果 StorPort 微型端口的 **StorPortBuildIo** 例程返回 **FALSE**，则不会将相关 SRB 传递到 **StartIo**。  (在这种情况下，微型端口驱动程序必须通过**StorPortBuildIo**或其他) 的通知类型**RequestComplete**调用[**StorPortNotification**](/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)来完成 SRB。

> [!NOTE]
> 此规则测试 StorPort 的正确操作，而不是微型端口的正确操作。

 

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortBuildIo</strong> 规则。</p>
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

 

