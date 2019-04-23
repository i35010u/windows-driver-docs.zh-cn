---
title: Bug 检查 0x48 CANCEL_STATE_IN_COMPLETED_IRP
description: CANCEL_STATE_IN_COMPLETED_IRP bug 检查具有 0x00000048 值。 这表示 I/O 请求数据包 (IRP) 已完成，且然后随后被取消。
ms.assetid: e706cf9b-8800-41ce-9bad-e4b9a8503051
keywords:
- Bug 检查 0x48 CANCEL_STATE_IN_COMPLETED_IRP
- CANCEL_STATE_IN_COMPLETED_IRP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CANCEL_STATE_IN_COMPLETED_IRP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ded2f30d55bfa8c58892e813b8fb224c0aa7f39
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903851"
---
# <a name="bug-check-0x48-cancelstateincompletedirp"></a>Bug 检查 0x48：取消\_状态\_IN\_COMPLETED\_IRP


取消\_状态\_IN\_COMPLETED\_IRP bug 检查的值为 0x00000048。 这表示 I/O 请求数据包 (IRP) 已完成，且然后随后被取消。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="cancelstateincompletedirp-parameters"></a>取消\_状态\_IN\_COMPLETED\_IRP 参数


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
<td align="left"><p>指向 IRP 的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>驱动程序设置在取消例程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

有 IRP*取消*例程集已完成，通常情况下，不取消。 但驱动程序已完成后，调用 IRP*取消*例程。

原因可能是完成 IRP，然后尝试将其取消的驱动程序。

它也可能导致两个驱动程序的每个尝试访问相同的 IRP 不正确的方式。

<a name="resolution"></a>分辨率
----------

可以使用取消例程参数来确定哪些驱动程序或堆栈导致的 bug 检查。

 

 




