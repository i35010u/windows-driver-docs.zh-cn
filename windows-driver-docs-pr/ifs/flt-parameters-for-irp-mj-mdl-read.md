---
title: FLT_PARAMETERS IRP_MJ_MDL_READ 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_MDL\_读取。
ms.assetid: d07d3ba2-a405-481c-986b-7e26cda61909
keywords:
- FLT_PARAMETERS IRP_MJ_MDL_READ 联合可安装文件系统驱动程序
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a668010517364b7594fb0d58d736bc6af7442512
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561878"
---
# <a name="fltparameters-for-irpmjmdlread-union"></a>FLT\_IRP 的参数\_MJ\_MDL\_读取联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构，该操作是 IRP\_MJ\_MDL\_读取。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    LARGE_INTEGER           FileOffset;
    ULONG POINTER_ALIGNMENT Length;
    ULONG POINTER_ALIGNMENT Key;
    PMDL                    *MdlChain;
  } MdlRead;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**MdlRead**  
结构，它包含以下成员。

**FileOffset**  
缓存文件中的起始字节。

**长度**  
长度，以字节为单位，从缓存文件读取的数据。

**Key**  
目标文件的字节范围锁与关联的密钥值。 如果要读取的范围重叠，或者是在文件中以独占方式锁定范围的子范围，此参数必须是该排他锁的键。 必须通过调用线程; 的父进程持有排他锁否则，将忽略此参数。

**MdlChain**  
指向一个变量来接收到一系列一个或多个内存描述符 (MDL) 的列表介绍了包含要读取的数据页的指针的指针。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构 IRP\_MJ\_MDL\_读取操作包含的参数的快速 I/O **MdlRead**表示的回调数据操作 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在 FLT\_IO\_参数\_块结构。

如果快速 I/O IRP\_MJ\_MDL\_读取请求失败，则的 I/O 操作的颁发者确定如何重新发出请求。 微筛选器可能无法始终达到基于 IRP 的 IRP\_MJ\_MDL\_读取。 例如，IRP 请求也可以作为 IRP 重新颁发\_MJ\_IRP 读取/\_MN\_MDL。

IRP\_MJ\_MDL\_读取是一个快速的 I/O 操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

 

 






