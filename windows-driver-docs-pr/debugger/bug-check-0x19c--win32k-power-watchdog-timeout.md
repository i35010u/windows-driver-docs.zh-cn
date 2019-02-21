---
title: Bug 检查 0x19C WIN32K_POWER_WATCHDOG_TIMEOUT
description: WIN32K_POWER_WATCHDOG_TIMEOUT bug 检查具有 0x0000019C 值。 这表示，Win32k 不能打开监视器及时。
ms.assetid: 55907359-C282-43F0-92FE-5DC248BF9D02
keywords:
- Bug 检查 0x19C WIN32K_POWER_WATCHDOG_TIMEOUT
- WIN32K_POWER_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_POWER_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c94ea7487ea72fb341fda61b4e727bd45c3ae6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542427"
---
# <a name="bug-check-0x19c-win32kpowerwatchdogtimeout"></a>Bug 检查 0x19C:WIN32K\_电源\_监视器\_超时


WIN32K\_电源\_监视器\_超时错误检查的值为 0x0000019C。 这表示，Win32k 不能打开监视器及时。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="win32kpowerwatchdogtimeout-parameters"></a>WIN32K\_电源\_监视器\_超时参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>失败类型 (win32kbase ！POWER_WATCHDOG_TYPE)</p>
<div class="code">
<code>0x10 : The power request queue is not making progress
              2 - Pointer to the thread processing power requests, if any
              3 - Pointer to the win32k user lock
              4 - Pointer to the power request (win32kbase!PPOWERREQUEST) being
                  processed, if any
          0x20 : Calling PO to set power state
              2 - Pointer to the power request worker thread              
              3 - Reserved
              4 - Reserved
          0x30 : Calling GDI to power on
              2 - Pointer to the power request worker thread
              3 - Reserved
              4 - Reserved
          0x40 : Calling DWM to render
              2 - Pointer to the power request worker thread
              3 - Reserved
              4 - Reserved
          0x50 : Calling monitor driver to power on
              2 - Pointer to the power request worker thread
              3 - Reserved
              4 - Reserved</code>
</div></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>










