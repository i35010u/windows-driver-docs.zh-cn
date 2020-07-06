---
title: KsProcessingMutex 规则（）
ms.assetid: AD73B241-7B08-4E48-94A1-B6BDE78590E6
ms.date: 05/21/2018
description: ''
keywords:
- KsProcessingMutex 规则（）
topic_type:
- apiref
api_name:
- KsProcessingMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b30f77019b29dfab72d5f14cf9e761db13248a2
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968146"
---
# <a name="ksprocessingmutex-rule-"></a>KsProcessingMutex 规则（）


KsProcessingMutex 规则指定一个 KS 微型端口驱动程序按正确的顺序使用处理互斥体：

-   不能以递归方式获取处理互斥体。
-   已获取处理互斥体的线程以后不应尝试获取筛选器控件互斥体。
-   如果不首先获取处理互斥体，则该线程不应释放它。

**驱动程序模型： KS**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x0008100B）


<a name="how-to-test"></a>如何测试
-----------

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
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em> &lt; &gt; yourdriver</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>另请参阅
--------

[在 AVStream 中处理互斥](https://docs.microsoft.com/windows-hardware/drivers/stream/processing-mutex-in-avstream)
 

 





