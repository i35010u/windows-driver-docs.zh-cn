---
title: IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时，将使用以下联合组件。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: efc6eec502b53238f152d6d0f2a1706ca568fe94
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063637"
---
# <a name="flt_parameters-for-irp_mj_acquire_for_section_synchronization-union"></a>IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合的 FLT_PARAMETERS

当 IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作的[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时，将使用以下联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    FS_FILTER_SECTION_SYNC_TYPE SyncType;
    ULONG POINTER_ALIGNMENT     PageProtection;
    PFS_FILTER_SECTION_SYNC_OUTPUT OutputInformation;
  } AcquireForSectionSynchronization;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

### <a name="synctype"></a>SyncType  

节请求的同步的类型。 如果正在创建一个节，此参数将设置为 **SyncTypeCreateSection** ;否则，将其设置为 **SyncTypeOther**。

### <a name="pageprotection"></a>PageProtection

节请求的页保护的类型。 如果 **SyncType** 为 SyncTypeOther，则必须为零。 否则，此参数必须为定义的 [内存保护常量值](/windows/win32/memory/memory-protection-constants)之一。

### <a name="outputinformation"></a>OutputInformation

一个 [**FS_FILTER_SECTION_SYNC_OUTPUT**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fs_filter_section_sync_output) 结构，它指定描述正在创建的节的特性的信息。

## <a name="remarks"></a>备注

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作的 [**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构包含回调数据所表示的 **AcquireForSectionSynchronization** 操作的参数 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT_IO_PARAMETER_BLOCK 结构中。

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 是 (FSFilter) 回调操作的文件系统。

如果 **SyncType** 成员的枚举值设置为 **SyncTypeOther**，则文件系统筛选器或旧筛选器驱动程序不能使此操作失败。 如果将 **SyncType** 设置为 **SyncTypeCreateSection**，则如果没有足够的内存来创建分区，则允许文件系统微筛选器或旧版筛选器驱动程序失败并出现 STATUS_INSUFFICIENT_RESOURCES 错误。

有关 FSFilter 回调操作的详细信息，请参阅 [**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

## <a name="requirements"></a>要求

**版本**：在 windows XP 和更高版本的 windows 操作系统中可用。

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>另请参阅

[**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)