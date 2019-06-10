---
title: 启用应用程序验证工具
description: 启用应用程序验证工具
ms.assetid: a91e244e-e3b6-4975-8385-1da06cc3ae83
keywords:
- 启用应用程序验证器 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0e9aa47c3832d6a49f8501fb277568954faf932
ms.sourcegitcommit: a70dcf63a439d278ae0194733d9fa2adfe496c89
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66813589"
---
# <a name="enable-application-verifier"></a>启用应用程序验证工具


## <span id="ddk_enable_application_verifier_dtools"></span><span id="DDK_ENABLE_APPLICATION_VERIFIER_DTOOLS"></span>


**启用应用程序验证工具**标志启用系统功能，可用于用户模式应用程序测试，如页堆验证锁定检查，并且处理检查。

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
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

此标志可使只有最基本的检测功能。 若要可靠地测试用户模式应用程序，请使用应用程序验证器 (appverif.exe)。 有关详细信息，请参阅[应用程序验证工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/application-verifier)。
