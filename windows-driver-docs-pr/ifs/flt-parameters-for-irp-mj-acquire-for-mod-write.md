---
title: IRP_MJ_ACQUIRE_FOR_MOD_WRITE 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_ACQUIRE_FOR_MOD_WRITE 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时，将使用以下联合组件。
ms.assetid: f950f8df-fcaa-4af7-9227-eb069f289176
keywords:
- IRP_MJ_ACQUIRE_FOR_MOD_WRITE 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: 3ecc0e98ba2aeaf14fc291899f0a2c84eb49a477
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063644"
---
# <a name="flt_parameters-for-irp_mj_acquire_for_mod_write-union"></a>IRP_MJ_ACQUIRE_FOR_MOD_WRITE 联合的 FLT_PARAMETERS

当 IRP_MJ_ACQUIRE_FOR_MOD_WRITE 操作的[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时，将使用以下联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PLARGE_INTEGER EndingOffset;
    PERESOURCE     *ResourceToRelease;
  } AcquireForModifiedPageWriter;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

```AcquireForModifiedPageWriter```

包含以下成员的结构。

```EndingOffset```

指向一个变量的指针，该变量包含要写入的最后一个字节的偏移量加1。

```ResourceToRelease```

指向要 [获取 () ](../kernel/eresource-structures.md) 资源的指针的指针。

## <a name="remarks"></a>备注

IRP_MJ_ACQUIRE_FOR_MOD_WRITE 操作的 [**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构包含回调数据所表示的 **AcquireForModifiedPageWriter** 操作的参数 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 [**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 结构中。

IRP_MJ_ACQUIRE_FOR_MOD_WRITE 是 (FSFilter) 回调操作的文件系统。 在此操作中， *ResourceToRelease* 是指向资源的指针的指针，该指针指向要 () 操作) 获取 (的资源。 资源将在 IRP_MJ_RELEASE_FOR_MOD_WRITE 回调操作中释放。

有关 FSFilter 回调操作的详细信息，请参阅 [**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

## <a name="requirements"></a>要求

**标头**： *Fltkernel* (包含 *Fltkernel*) 


## <a name="see-also"></a>另请参阅

[FLT_CALLBACK_DATA](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](/previous-versions/ff544654(v=vs.85))

[FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)