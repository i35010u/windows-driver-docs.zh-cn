---
title: Bug Check 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
description: The DRIVER_PORTION_MUST_BE_NONPAGED bug check has a value of 0x000000D3. This indicates that the system attempted to access pageable memory at a process IRQL that was too high.
ms.assetid: 8b33dd20-9faa-4c02-96b7-89f55e69aeec
keywords:
- Bug Check 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
- DRIVER_PORTION_MUST_BE_NONPAGED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PORTION_MUST_BE_NONPAGED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc8576fb13e085fa76a031f57bee0902f365cebd
ms.sourcegitcommit: 22ab407df553db6d917b5ad3c9531a2dadfafc25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74411168"
---
# <a name="bug-check-0xd3-driver_portion_must_be_nonpaged"></a>Bug Check 0xD3: DRIVER\_PORTION\_MUST\_BE\_NONPAGED


The DRIVER\_PORTION\_MUST\_BE\_NONPAGED bug check has a value of 0x000000D3. This indicates that the system attempted to access pageable memory at a process IRQL that was too high.

> [!IMPORTANT]
> 本主题面向程序员。 If you are a customer who has received a blue screen error code while using your computer, see [Troubleshoot blue screen errors](https://www.windows.com/stopcode).


## <a name="driver_portion_must_be_nonpaged-parameters"></a>DRIVER\_PORTION\_MUST\_BE\_NONPAGED Parameters


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
<td align="left"><p>1</p></td>
<td align="left"><p>Memory referenced</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL at time of reference</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong> Read</p>
<p><strong>1:</strong> Write</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>Address that referenced memory</p></td>
</tr>
</tbody>
</table>

 

If the driver responsible for the error can be identified, its name is printed on the blue screen and stored in memory at the location (PUNICODE\_STRING) **KiBugCheckDriver**.

<a name="cause"></a>原因
-----

This bug check is usually caused by drivers that have incorrectly marked their own code or data as pageable.

<a name="resolution"></a>分辨率
----------

To begin debugging, use a kernel debugger to get a stack trace: the [ **!analyze**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze) debug extension displays information about the bug check and can be helpful in determining the root cause, then use the [**kb (Display Stack Backtrace)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-) command to get a stack trace.

 

 




