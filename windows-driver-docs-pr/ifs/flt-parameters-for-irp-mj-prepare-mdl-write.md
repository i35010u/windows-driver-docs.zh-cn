---
title: FLT_PARAMETERS for IRP_MJ_PREPARE_MDL_WRITE union
description: 当 FLT\_IO\_参数\_块结构的操作的块结构为 IRP\_MJ 时，将使用以下联合组件，\_写入\_准备\_MDL。
ms.assetid: eebbb8d4-f46d-4aee-aeb3-7edcbd23207a
keywords:
- FLT_PARAMETERS for IRP_MJ_PREPARE_MDL_WRITE union 可安装的文件系统驱动程序
- FLT_PARAMETERS 可安装的可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
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
ms.openlocfilehash: 7ecac2eb0a8ec29bc823be0fbfa6f0c203185676
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841367"
---
# <a name="flt_parameters-for-irp_mj_prepare_mdl_write-union"></a>用于 IRP\_MJ\_准备\_MDL\_写入联合的 FLT\_参数


当[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**操作的**块结构为 IRP\_MJ 时，将使用以下联合组件，\_写入\_准备\_MDL。

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
  } PrepareMdlWrite;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**PrepareMdlWrite**  
包含以下成员的结构。

**FileOffset**  
缓存文件中的起始字节。

**长度**  
要写入缓存文件的数据的长度（以字节为单位）。

**Key**  
与目标文件的字节范围锁关联的键值。 如果要写入的范围重叠，或者是文件内独占锁定范围的子范围，则此参数必须是该排他锁的键。 排他锁必须由调用线程的父进程持有;否则，将忽略此参数。

**MdlChain**  
指向一个变量的指针，该变量接收指向包含要写入的数据的页的一个或多个内存描述符列表（MDL）链的指针。

<a name="remarks"></a>备注
-------

IRP 的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构\_MJ\_准备\_MDL\_写入操作包含回调数据表示的快速 i/o **PrepareMdlWrite**操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在 FLT\_IO\_参数\_块结构。

如果快速 i/o IRP\_MJ\_准备\_MDL\_写入请求失败，则 i/o 的颁发者确定如何重新发出该请求。 微筛选器可能不会始终获取基于 IRP 的 IRP\_MJ\_MDL\_写入。 例如，可以将 IRP 请求重新颁发为 IRP\_MJ\_WRITE/IRP\_MN\_MDL。

IRP\_MJ\_准备\_MDL\_写入是一种快速的 i/o 操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel （包括 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_\_FS\_筛选器\_操作**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

 

 






