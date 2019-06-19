---
title: FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合
description: 该操作的 FLT_IO_PARAMETER_BLOCK 结构在 MajorFunction 字段 IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 时使用以下联合组件。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合可安装文件系统驱动程序
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
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6edcc43a6644c853cd43170ea4858a6a95ccee6b
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161575"
---
# <a name="fltparameters-for-irpmjacquireforsectionsynchronization-union"></a>FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 联合

使用以下联合组件时**MajorFunction**字段[ **FLT_IO_PARAMETER_BLOCK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构，该操作是 IRP_MJ_ACQUIRE_FOR_SECTION_同步。

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

请求的部分的同步的类型。 此参数设置为**SyncTypeCreateSection**如果要创建一个部分; 否则，它设置为**SyncTypeOther**。

### <a name="pageprotection"></a>PageProtection

为部分中请求的页保护类型。 必须为零**SyncType**是 SyncTypeOther。 否则，此参数可以是下列标志，可能需要合并使用 PAGE_NOCACHE 之一：

| 值 | 含义 |
| ----- | ------- |
| PAGE_READONLY | 为只读或写入时复制的访问。 |
| PAGE_READWRITE | 为只读的副本上写入或读/写访问。 |
| PAGE_WRITECOPY | 为只读或写入时复制的访问。 等效于 PAGE_READONLY。 |
| PAGE_EXECUTE | 用于执行访问。 |

### <a name="outputinformation"></a>OutputInformation

一个[ **FS_FILTER_SECTION_SYNC_OUTPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fs_filter_section_sync_output)结构，它指定描述正在创建的节的属性的信息。

## <a name="remarks"></a>备注

[ **FLT_PARAMETERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作的结构中包含的参数**AcquireForSectionSynchronization**表示的回调数据操作 ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT_IO_PARAMETER_BLOCK 结构。

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 是文件系统 (FSFilter) 回调操作。

如果的枚举的值**SyncType**成员设置为**SyncTypeOther**，文件系统微筛选器或旧版的筛选器驱动程序不能使此操作失败。 如果**SyncType**设置为**SyncTypeCreateSection**，允许文件系统微筛选器或旧版筛选器驱动程序如果不存在内存不足，无法创建 STATUS_INSUFFICIENT_RESOURCES 错误而失败部分。

有关 FSFilter 回调操作的详细信息，请参阅引用条目[ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)。

## <a name="requirements"></a>要求

| | |
| ------- | ------- |
| Version | 在 Windows XP 和更高版本的 Windows 操作系统中可用。 |
| Header    | Fltkernel.h （包括 Fltkernel.h） |

## <a name="see-also"></a>请参阅

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
