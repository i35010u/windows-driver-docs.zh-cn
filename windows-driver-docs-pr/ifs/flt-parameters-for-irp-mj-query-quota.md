---
title: IRP_MJ_QUERY_QUOTA 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_QUERY_QUOTA 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时使用的联合组件。
ms.assetid: b87b008d-f1ce-4dab-9afa-df67aa3dc596
keywords:
- IRP_MJ_QUERY_QUOTA 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: d2796a23552d9f1039eb541dc514357dca6f2b1c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063616"
---
# <a name="flt_parameters-for-irp_mj_query_quota-union"></a>IRP_MJ_QUERY_QUOTA 联合的 FLT_PARAMETERS

当[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)操作的[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时使用的联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                       Length;
    PSID                        StartSid;
    PFILE_GET_QUOTA_INFORMATION SidList;
    ULONG                       SidListLength;
    PVOID                       QuotaBuffer;
    PMLD                        MdlAddress;
  } QueryQuota;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

**QueryQuota**  
包含以下成员的结构。

**长度**  
**QuotaBuffer**指向的缓冲区的长度（以字节为单位）。

**StartSid**  
指向用于开始扫描配额列表的条目的安全标识符 (SID) 的可选指针。 如果未在操作的 FLT_IO_PARAMETER_BLOCK 结构中设置 SL_INDEX_SPECIFIED 标志，或者如果 **SidList** 指向非空列表，则忽略此参数。

**SidList**  
指向调用方提供的 FILE_GET_QUOTA_INFORMATION 结构化输入缓冲区的指针，该缓冲区指定要查询其配额信息的 Sid。

**SidListLength**  
**SidList**指向的缓冲区的长度（以字节为单位）。

**QuotaBuffer**  
指向调用方提供的、要返回其配额信息 [**FILE_QUOTA_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)结构化输出缓冲区的指针。 此成员是可选的，如果 **MdlAddress**中提供 MDL，此成员可以为 NULL。 请参阅 " **备注**"。

**MdlAddress**  
 (MDL 的内存描述符列表的地址) 描述 **QuotaBuffer** 指向的缓冲区。 此成员是可选的，如果**QuotaBuffer**中提供了缓冲区，则可以为**NULL** 。 请参阅 " **备注**"。

## <a name="remarks"></a>备注

[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)操作的[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调数据表示的基于 IRP 的查询配额信息操作的参数 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT_IO_PARAMETER_BLOCK 结构中。

如果同时提供了 **QuotaBuffer** 和 **MdlAddress** 缓冲区，则建议 minifilters 使用 MDL。 当 **QuotaBuffer** 指向的内存是在调用进程的上下文中访问的用户模式地址时，或者如果它是内核模式地址，则它是有效的。

如果微筛选器更改 **MdlAddress**的值，则在其后回拨后，筛选器管理器将释放当前存储在 **MDLADDRESS** 中的 MDL，并还原以前的 **MdlAddress**值。

IRP_MJ_QUERY_QUOTA 是基于 IRP 的操作。

## <a name="requirements"></a>要求

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>另请参阅

[**FILE_QUOTA_INFORMATION**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_quota_information)

[**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckQuotaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckquotabuffervalidity)

[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)

[**SID**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)