---
title: Bug 检查 0xE8 INVALID_CANCEL_OF_FILE_OPEN
description: INVALID_CANCEL_OF_FILE_OPEN bug 检查的值为0x000000E8。 这表明传递到 IoCancelFileOpen 的文件对象无效。
keywords:
- Bug 检查 0xE8 INVALID_CANCEL_OF_FILE_OPEN
- INVALID_CANCEL_OF_FILE_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_CANCEL_OF_FILE_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e02eca07cb930a894cb312fe083af5dd93da355
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793271"
---
# <a name="bug-check-0xe8-invalid_cancel_of_file_open"></a>Bug 检查0xE8： \_ \_ \_ 打开的文件 \_ 取消无效


\_ \_ \_ 文件 \_ 打开 bug 检查无效，其值为0x000000E8。 这表明传递到 **IoCancelFileOpen** 的文件对象无效。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_cancel_of_file_open-parameters"></a>无效 \_ \_ 的 \_ 文件 \_ 打开参数取消


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
<td align="left"><p>传递给<strong>IoCancelFileOpen</strong>的文件对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>传递给<strong>IoCancelFileOpen</strong>的设备对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

传递给 **IoCancelFileOpen** 的文件对象无效。 它应该具有一个。 调用 **IoCancelFileOpen** 的驱动程序出错。

 

 




