---
title: SeStopImpersonatingClient 例程
description: SeStopImpersonatingClient 例程结束用户的调用线程的模拟。
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
ms.openlocfilehash: 2dfd01a7cb7c1768eef553b4137c3ddf763ee1fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548095"
---
# <a name="sestopimpersonatingclient-routine"></a>SeStopImpersonatingClient 例程


**SeStopImpersonatingClient**例程结束用户的调用线程的模拟。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID SeStopImpersonatingClient(void);
```

<a name="parameters"></a>参数
----------

此例程没有任何参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

服务器线程可以模拟用户，通过调用[ **SeImpersonateClientEx** ](https://msdn.microsoft.com/library/windows/hardware/ff556659)例程。 线程完成时模拟用户，它会调用**SeStopImpersonatingClient**例程，以结束模拟。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SeImpersonateClientEx**](https://msdn.microsoft.com/library/windows/hardware/ff556659)

 

 






