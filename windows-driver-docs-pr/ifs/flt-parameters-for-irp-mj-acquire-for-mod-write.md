---
title: FLT_PARAMETERS for IRP_MJ_ACQUIRE_FOR_MOD_WRITE union
description: 当操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段为 IRP_MJ_ACQUIRE_FOR_MOD_WRITE 时，使用以下联合组件。
ms.assetid: f950f8df-fcaa-4af7-9227-eb069f289176
keywords:
- FLT_PARAMETERS for IRP_MJ_ACQUIRE_FOR_MOD_WRITE union 可安装的文件系统驱动程序
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
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ef132102cea92756c9c252307b78b47ce763560
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841407"
---
# <a name="flt_parameters-for-irp_mj_acquire_for_mod_write-union"></a>FLT_PARAMETERS for IRP_MJ_ACQUIRE_FOR_MOD_WRITE union

当操作的[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MAJORFUNCTION**字段为 IRP_MJ_ACQUIRE_FOR_MOD_WRITE 时，使用以下联合组件。

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

指向要获取的资源（[ERESOURCE](https://docs.microsoft.com/windows-hardware/drivers/kernel/eresource-structures)）的指针的指针。

## <a name="remarks"></a>备注

IRP_MJ_ACQUIRE_FOR_MOD_WRITE 操作的[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据（[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构所表示的**AcquireForModifiedPageWriter**操作的参数。 它包含在[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构中。

IRP_MJ_ACQUIRE_FOR_MOD_WRITE 是一个文件系统（FSFilter）回调操作。 在此操作中， *ResourceToRelease*是指向要获取的资源的指针的指针（操作前）或获取的（操作后）。 资源将在 IRP_MJ_RELEASE_FOR_MOD_WRITE 回调操作中释放。

有关 FSFilter 回调操作的详细信息，请参阅[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)的参考条目。

## <a name="requirements"></a>要求

|   |   |
| - | - |
| 标头 | *Fltkernel* （包括*Fltkernel*） |

## <a name="see-also"></a>另请参阅

[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
