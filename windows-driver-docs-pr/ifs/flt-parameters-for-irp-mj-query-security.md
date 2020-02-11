---
title: IRP_MJ_QUERY_SECURITY 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_QUERY_SECURITY 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时使用的联合组件。
ms.assetid: 7707fec2-9fe8-40f6-9f34-f43403551440
keywords:
- IRP_MJ_QUERY_SECURITY 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: f85f46bc878aa75a45a81a7a575f634f8eda1cdb
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072230"
---
# <a name="flt_parameters-for-irp_mj_query_security-union"></a>IRP_MJ_QUERY_SECURITY 联合的 FLT_PARAMETERS

当[**IRP_MJ_QUERY_SECURITY**](irp-mj-query-security.md)操作的[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时使用的联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    SECURITY_INFORMATION    SecurityInformation;
    ULONG POINTER_ALIGNMENT Length;
    PVOID                   SecurityBuffer;
    PDML                    MdlAddress;
  } QuerySecurity;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

**QuerySecurity**  
包含以下成员的结构。

**SecurityInformation**  
指向调用方提供的[**SECURITY_INFORMATION**](security-information.md)值的指针，该值指定要查询的安全信息。 下列情况之一：

| SecurityInformation 值 | 含义 |
| ------------------------- | ------- |
| OWNER_SECURITY_INFORMATION | 正在查询对象的所有者标识符。 需要 READ_CONTROL 访问权限。 |
| GROUP_SECURITY_INFORMATION | 正在查询对象的主要组标识符。 需要 READ_CONTROL 访问权限。 |
| DACL_SECURITY_INFORMATION | 正在查询对象的随机访问控制列表（DACL）。 需要 READ_CONTROL 访问权限。 |
| SACL_SECURITY_INFORMATION | 正在查询对象的系统 ACL （SACL）。 需要 ACCESS_SYSTEM_SECURITY 访问权限。 |

**长度**  
**SecurityBuffer**指向的缓冲区的长度（以字节为单位）。

**SecurityBuffer**  
指向调用方提供的输出缓冲区的指针，该缓冲区接收指定对象的安全描述符的副本。 调用进程必须具有查看对象安全状态的指定方面的权限。 以自相关格式返回[**SECURITY_DESCRIPTOR**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))结构。 此成员是可选的，如果**MdlAddress**中提供 MDL，此成员可以为 NULL。 请参阅 "**备注**"。

**MdlAddress**  
描述**SecurityBuffer**指向的缓冲区的内存描述符列表（MDL）的地址。 此成员是可选的，如果**SecurityBuffer**中提供了缓冲区，则可以为**NULL** 。 请参阅 "**备注**"。

## <a name="remarks"></a>备注

[**IRP_MJ_QUERY_SECURITY**](irp-mj-query-security.md)操作的[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调数据（[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构表示的基于 IRP 的查询安全信息操作的参数。 它包含在[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构中。

如果同时提供了**SecurityBuffer**和**MdlAddress**缓冲区，则建议 minifilters 使用 MDL。 当**SecurityBuffer**指向的内存是在调用进程的上下文中访问的用户模式地址时，或者如果它是内核模式地址，则它是有效的。

如果微筛选器更改**MdlAddress**的值，则在其后回拨后，筛选器管理器将释放当前存储在**MDLADDRESS**中的 MDL，并还原以前的**MdlAddress**值。

在 Windows XP 和更高版本中，FLT_IO_PARAMETER_BLOCK 结构的**TargetFileObject**成员指向的对象可以表示已命名的数据流。 有关命名数据流的详细信息，请参阅[**FILE_STREAM_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)。

IRP_MJ_QUERY_SECURITY 是基于 IRP 的操作。

## <a name="requirements"></a>要求

|   |   |
| - | - |
| 标头 | Fltkernel （包括 Fltkernel） |

## <a name="see-also"></a>另请参阅

[**FILE_STREAM_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP_MJ_QUERY_SECURITY**](irp-mj-query-security.md)

[**SECURITY_DESCRIPTOR**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**SECURITY_INFORMATION**](security-information.md)
