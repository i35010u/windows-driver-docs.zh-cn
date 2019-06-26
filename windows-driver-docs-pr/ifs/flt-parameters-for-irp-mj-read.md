---
title: FLT_PARAMETERS IRP_MJ_READ 联合
description: 使用以下联合组件时 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_读取。
ms.assetid: 48674db7-c0cc-45a0-bce9-eaf1a4cec362
keywords:
- FLT_PARAMETERS IRP_MJ_READ 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 6667987b44f958f4d1c95a499ac67b204685839b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365071"
---
# <a name="fltparameters-for-irpmjread-union"></a>FLT\_IRP 的参数\_MJ\_读取联合


使用以下联合组件时**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构操作[ **IRP\_MJ\_读取**](irp-mj-read.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                   Length;
    ULONG POINTER_ALIGNMENT Key;
    LARGE_INTEGER           ByteOffset;
    PVOID                   ReadBuffer;
    PMDL                    MdlAddress;
  } Read;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**读取**  
结构，它包含以下成员。

**长度**  
长度 （字节），要读取的数据。

**Key**  
目标文件的字节范围锁与关联的密钥值。

**ByteOffset**  
要读取的数据文件中的起始字节偏移量。

**ReadBuffer**  
指向该缓冲区用于接收从文件读取的数据。

**MdlAddress**  
描述缓冲区的内存描述符列表 (MDL) 的地址， **ReadBuffer**成员指向。 此成员是可选的可以是**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构 IRP\_MJ\_读取操作包含回调数据 (所表示的读操作的参数[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_读取可以是基于 IRP 的操作或快速 I/O 操作。

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


[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreadfile)

[**IRP\_MJ\_READ**](irp-mj-read.md)

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)

 

 






