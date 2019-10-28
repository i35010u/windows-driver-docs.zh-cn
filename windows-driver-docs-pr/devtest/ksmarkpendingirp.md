---
title: KsMarkPendingIrp 规则（）
description: KsMarkPendingIrp 规则指定内核流（KS）微型端口驱动程序应将 Irp 标记为 "挂起"，同时返回以下回调函数 AVStrMiniFilterCloseAVStrMiniPinCloseAVStrMiniPinCreate 中的状态\_"挂起"。
ms.assetid: 88612656-0068-41B8-9A0D-4DDC98AD2435
ms.date: 05/21/2018
keywords:
- KsMarkPendingIrp 规则（）
topic_type:
- apiref
api_name:
- KsMarkPendingIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c82d2d590fe3a0a548b5005d5fa89e59c103641e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839418"
---
# <a name="ksmarkpendingirp-rule-"></a>KsMarkPendingIrp 规则（）


KsMarkPendingIrp 规则指定内核流（KS）微型端口驱动程序应将 Irp 标记为 "挂起"，同时返回以下回调函数中的状态\_"挂起"：

-   AVStrMiniFilterClose
-   AVStrMiniPinClose
-   AVStrMiniPinCreate

若要将 IRP 标记为挂起，请使用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)例程。

|              |     |
|--------------|-----|
| 驱动程序型号 | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：检测到\_冲突的驱动程序\_验证程序\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （0x00081008） |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>KsMarkPendingIrp</strong>规则。</p>
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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>另请参阅
--------

[*AVStrMiniFilterClose*](https://docs.microsoft.com/previous-versions/ff556307(v=vs.85))
[*AVStrMiniPinClose*](https://docs.microsoft.com/previous-versions/ff556329(v=vs.85))
[*AVStrMiniPinCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinirp)
 

 





