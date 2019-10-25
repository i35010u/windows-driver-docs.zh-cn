---
title: SeStopImpersonatingClient 例程
description: SeStopImpersonatingClient 例程结束调用线程的用户模拟。
ms.assetid: 1aab384b-919c-4709-9ceb-66616c622714
keywords:
- SeStopImpersonatingClient 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- SeStopImpersonatingClient
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa5ff5053b13dfbcbd4e7740c33e621c2a245f95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840967"
---
# <a name="sestopimpersonatingclient-routine"></a>SeStopImpersonatingClient 例程


**SeStopImpersonatingClient**例程结束调用线程的用户模拟。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID SeStopImpersonatingClient(void);
```

<a name="parameters"></a>参数
----------

此例程没有参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

服务器线程可以通过调用[**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)例程来模拟用户。 当线程完成模拟用户时，它将调用**SeStopImpersonatingClient**例程来结束模拟。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SeImpersonateClientEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)

 

 






