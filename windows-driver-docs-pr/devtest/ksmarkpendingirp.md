---
title: 'KsMarkPendingIrp 规则 ( # A1'
description: KsMarkPendingIrp 规则指定内核流 (KS) 微型端口驱动程序应将 Irp 标记为 "挂起"，同时返回 \_ 以下回调函数 AVStrMiniFilterCloseAVStrMiniPinCloseAVStrMiniPinCreate 中的状态 "挂起"。
ms.assetid: 88612656-0068-41B8-9A0D-4DDC98AD2435
ms.date: 05/21/2018
keywords:
- 'KsMarkPendingIrp 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsMarkPendingIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 89a94cc702e5a91519666beff2c3e1a542208fda
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103414"
---
# <a name="ksmarkpendingirp-rule-"></a>KsMarkPendingIrp 规则 ( # A1


KsMarkPendingIrp 规则指定内核流 (KS) 微型端口驱动程序应将 Irp 标记为 "挂起"，同时返回 \_ 以下回调函数中的状态 "挂起"：

-   AVStrMiniFilterClose
-   AVStrMiniPinClose
-   AVStrMiniPinCreate

若要将 IRP 标记为挂起，请使用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 例程。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00081008) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>KsMarkPendingIrp</strong> 规则。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em> &lt; &gt; yourdriver</em></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>另请参阅
--------

[*AVStrMiniFilterClose*](/previous-versions/ff556307(v=vs.85)) 
[*AVStrMiniPinClose*](/previous-versions/ff556329(v=vs.85)) 
[*AVStrMiniPinCreate*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinirp)
