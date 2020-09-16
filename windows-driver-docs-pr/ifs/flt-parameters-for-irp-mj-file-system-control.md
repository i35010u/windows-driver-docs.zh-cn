---
title: IRP_MJ_FILE_SYSTEM_CONTROL 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_FILE_SYSTEM_CONTROL 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时使用的联合组件。
ms.assetid: d90b9f23-9fae-46e8-b68c-1ba11b3fa17a
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.openlocfilehash: 1592ffda779c5e5d3a7e6e8c79d591ad56702f5f
ms.sourcegitcommit: 9b4760aae390b36dbdf9e0dd729a4a643c3f7831
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90565263"
---
# <a name="flt_parameters-for-irp_mj_file_system_control-union"></a>IRP_MJ_FILE_SYSTEM_CONTROL 联合的 FLT_PARAMETERS

当[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)操作的[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段时使用的联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      PVPB           Vpb;
      PDEVICE_OBJECT DeviceObject;
    } VerifyVolume;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
    } Common;
    struct {
      ULONG                    OutputBufferLength;
      ULONG POINTER_ALIGNMENT  InputBufferLength;
      ULONG POINTER_ALIGNMENT  FsControlCode;
      PVOID                    InputBuffer;
      PVOID                    OutputBuffer;
      PMDL                     OutputMdlAddress;
    } Neither;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
      PVOID                   SystemBuffer;
    } Buffered;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
      PVOID                   InputSystemBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Direct;
  } FileSystemControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

**FileSystemControl**  
包含以下成员的结构。

**VerifyVolume**  
用于 IRP_MN_VERIFY_VOLUME 操作的联合组件。

**Vpb**  
指向卷参数块的指针 (要验证的卷的 VPB) 。

**DeviceObject**  
一个指针，指向要验证的卷的设备对象。

**通用**  
用于 IRP_MN_KERNEL_CALL 和 IRP_MN_USER_FS_REQUEST 操作的所有缓冲方法的联合组件。

**OutputBufferLength**  
**OutputBuffer**或**OutputBuffer**成员指向的缓冲区的长度（以字节为单位）。

**InputBufferLength**  
**InputBuffer**、 **Buffered.SystemBuffer**或**InputSystemBuffer**成员指向的缓冲区的长度（以字节为单位）。

**FsControlCode**  
要传递给目标设备的文件系统、文件系统筛选器或微筛选器驱动程序的 FSCTL 函数代码。

有关 IOCTL 和 FSCTL 请求的详细信息，请参阅在 Microsoft Windows SDK 文档中使用*内核模式体系结构指南*中的[i/o 控制代码](../kernel/introduction-to-i-o-control-codes.md)和 "设备输入和输出控制代码"。  (此资源可能在某些语言和国家/地区不可用。 ) 

**两者均未选中**  
METHOD_NEITHER 缓冲方法时用于 IRP_MN_KERNEL_CALL 和 IRP_MN_USER_FS_REQUEST 操作的联合组件。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**InputBuffer**  
输入缓冲区的用户模式虚拟地址，该地址提供了操作的原始请求者。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)等例程，并将所有缓冲区引用包含在 **try/except** 块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](../kernel/errors-in-referencing-user-space-addresses.md)中[使用缓冲和直接 i/o](../kernel/using-neither-buffered-nor-direct-i-o.md)和错误。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)等例程，并将所有缓冲区引用包含在 **try/except** 块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](../kernel/errors-in-referencing-user-space-addresses.md)中[使用缓冲和直接 i/o](../kernel/using-neither-buffered-nor-direct-i-o.md)和错误。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputBuffer** 是可选的，如果 **不在 OUTPUTMDLADDRESS**中提供 MDL，则可以为 NULL。 请参阅 " **备注**"。

**OutputMdlAddress**  
 (MDL) 描述 **两个 OutputBuffer** 成员指向的缓冲区的内存描述符列表的地址。 此成员是可选的，如果**不在 OutputBuffer**中提供缓冲区，则可以为**NULL** 。

**缓冲区**  
METHOD_BUFFERED 缓冲方法时用于 IRP_MN_KERNEL_CALL 和 IRP_MN_USER_FS_REQUEST 操作的联合组件。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**SystemBuffer**  
操作的系统分配的缓冲区的地址。 在 METHOD_BUFFERED i/o 中，此缓冲区用于输入和输出。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**直接**  
METHOD_IN_DIRECT 或 METHOD_OUT_DIRECT 缓冲方法时用于 IRP_MN_KERNEL_CALL 和 IRP_MN_USER_FS_REQUEST 操作的联合组件。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)。

**InputSystemBuffer**  
操作的输入缓冲区的地址。 此缓冲区已被操作系统锁定，以便可以安全地从内核模式进行访问。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 与 METHOD_NEITHER i/o 不同，操作系统会锁定此缓冲区，以便可以安全地从内核模式进行访问，只要微筛选器与 i/o 操作的原始请求者处于相同的进程上下文中即可。 否则 (它必须调用[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) ，以从**OutputMdlAddress**成员指向的 MDL 获取系统地址。 ) 有关详细信息，请参阅*内核模式体系结构指南*中的[使用](../kernel/using-direct-i-o.md)直接 i/o 和[直接 i/o 中的错误](../kernel/errors-in-direct-i-o.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputMdlAddress**  
 (MDL 的内存描述符列表的地址) 描述 **OutputBuffer** 成员指向的缓冲区。 此成员是必需的，不能为 **NULL**。

## <a name="remarks"></a>备注

[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)操作的[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调数据表示的文件系统控件信息操作的参数 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 [**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 结构中。

如果同时提供两个 **OutputBuffer** 和 **MdlAddress** 缓冲区，则建议 minifilters 使用 MDL。

如果微筛选器的值 **都不是 MdlAddress**，则在其后回拨后，筛选器管理器将释放当前同时存储在 **MDLADDRESS** 中的 MDL，并将以前的值还原为 **MdlAddress**。

IRP_MJ_FILE_SYSTEM_CONTROL 是基于 IRP 的操作。

## <a name="requirements"></a>要求

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>请参阅

[**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoVerifyVolume**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioverifyvolume)

[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)

[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)

[**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))