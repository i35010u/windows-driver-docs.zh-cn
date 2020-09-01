---
title: 启用应用程序验证工具
description: 启用应用程序验证工具
ms.assetid: a91e244e-e3b6-4975-8385-1da06cc3ae83
keywords:
- '启用应用程序验证器 (全局标志) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8faaa703dfeaf1093bf5329a4146b27e5e60ad64
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211177"
---
# <a name="enable-application-verifier"></a>启用应用程序验证工具


## <span id="ddk_enable_application_verifier_dtools"></span><span id="DDK_ENABLE_APPLICATION_VERIFIER_DTOOLS"></span>


**启用应用程序验证程序**标志可启用用于用户模式应用程序测试的系统功能，如页堆验证、锁定检查和处理检查。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>vrf</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x100</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_APPLICATION_VERIFIER</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

此标志仅启用最基本的检测功能。 若要可靠地测试用户模式的应用程序，请使用 ( # A0) 应用程序验证工具。 有关详细信息，请参阅 [应用程序验证工具](../devtest/application-verifier.md)。