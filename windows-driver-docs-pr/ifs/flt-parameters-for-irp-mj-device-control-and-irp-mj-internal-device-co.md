---
title: IRP_MJ_DEVICE_CONTROL 和 IRP_MJ_INTERNAL_DEVICE_CONTROL 联合的 FLT_PARAMETERS
description: 操作的 FLT \_ IO \_ 参数块结构的 MajorFunction 字段 \_ 为 irp \_ MJ \_ 设备 \_ 控制或 irp \_ mj \_ 内部 \_ 设备 \_ 控制时使用的联合组件。
ms.assetid: ed2da1d5-838e-41a4-9a26-c61518da9cf3
keywords:
- FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL 和 IRP_MJ_INTERNAL_DEVICE_CONTROL 联合可安装的文件系统驱动程序
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
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a014ec35c69fb377a4df508b726ce62561a0e358
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065974"
---
# <a name="flt_parameters-for-irp_mj_device_control-and-irp_mj_internal_device_control-union"></a>\_Irp \_ mj \_ 设备 \_ 控制和 irp \_ mj \_ 内部 \_ 设备 \_ 控制联合的 FLT 参数


操作的[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的**MajorFunction**字段为[**irp \_ mj \_ 设备 \_ 控制**](irp-mj-device-control.md)或[**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md)时使用的联合组件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
    } Common;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Neither;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   SystemBuffer;
    } Buffered;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputSystemBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Direct;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputBuffer;
      PVOID                   OutputBuffer;
    } FastIo;
  } DeviceIoControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**DeviceIoControl**  
**通用**  
用于所有缓冲方法的联合组件。

**OutputBufferLength**  
**不是 OutputBuffer**、 **OutputBuffer**或**FastIo**成员指向的缓冲区的长度（以字节为单位）。

**InputBufferLength**  
**InputBuffer**、 **Buffered.SystemBuffer**、 **InputSystemBuffer**或**FastIo**成员指向的缓冲区的长度（以字节为单位）。

**IoControlCode**  
要传递给目标设备的设备驱动程序的 IOCTL 函数代码。

有关 IOCTL 请求的详细信息，请参阅 Microsoft Windows SDK 文档中的使用*内核模式体系结构指南*中的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)和 "设备输入和输出控制代码"。  (此资源可能在某些语言和国家/地区不可用。 ) 

**两者均未选中**  
缓存方法为方法时使用的联合组件 \_ 。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)。

**InputBuffer**  
输入缓冲区的用户模式虚拟地址，该地址提供了操作的原始请求者。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在 **try/except** 块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](../kernel/errors-in-referencing-user-space-addresses.md)中[使用缓冲和直接 i/o](../kernel/using-neither-buffered-nor-direct-i-o.md)和错误。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在 **try/except** 块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](../kernel/errors-in-referencing-user-space-addresses.md)中[使用缓冲和直接 i/o](../kernel/using-neither-buffered-nor-direct-i-o.md)和错误。

**OutputMdlAddress**  
 (MDL) 描述 *两个 OutputBuffer* 成员指向的缓冲区的内存描述符列表的地址。 此成员是可选的，并且可以为 **NULL**。

**缓冲区**  
缓冲方法被缓存方法时使用的联合组件 \_ 。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**SystemBuffer**  
操作的系统分配的缓冲区的地址。 在方法 \_ 缓冲 i/o 中，此缓冲区用于输入和输出。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**直接**  
当缓存方法为 \_ \_ 直接方法或方法 \_ OUT \_ 直接时使用的联合组件。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**InputSystemBuffer**  
操作的输入缓冲区的地址。 此缓冲区已被操作系统锁定，以便可以安全地从内核模式进行访问。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 在直接 i/o 中，与方法不是 i/o 不同， \_ 操作系统会锁定此缓冲区，以便可以安全地从内核模式进行访问，只要微筛选器与 i/o 操作的原始请求者处于相同的进程上下文中即可。 否则 (它必须调用[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) ，以从**OutputMdlAddress**成员指向 ) 的内存描述符列表 (MDL) 获取系统地址。有关详细信息，请参阅*内核模式体系结构指南*中的[直接 i/o 中](../kernel/errors-in-direct-i-o.md)[的直接 i/o](../kernel/using-direct-i-o.md)和错误。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputMdlAddress**  
描述 **OutputBuffer** 成员指向的缓冲区的 MDL 地址。 此成员是必需的，不能为 **NULL**。

**FastIo**  
[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)结构表示快速 I/o IRP \_ MJ \_ 设备控制操作时使用的联合组件 \_ 。

**InputBuffer**  
输入缓冲区的用户模式虚拟地址，该地址提供了操作的原始请求者。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在 **try/except** 块中。 有关详细信息，请参阅*内核模式体系结构指南*中的[引用用户空间地址中的错误](../kernel/errors-in-referencing-user-space-addresses.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在 **try/except** 块中。 有关详细信息，请参阅*内核模式体系结构指南*中的[引用用户空间地址中的错误](../kernel/errors-in-referencing-user-space-addresses.md)。  (此资源可能在某些语言和国家/地区不可用。 ) 

<a name="remarks"></a>备注
-------

[**Irp \_ mj \_ 设备 \_ 控制**](irp-mj-device-control.md)和[**IRP \_ mj \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md)操作的[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调 (数据表示的基于 IRP 的设备 i/o 控制信息操作的[**参数) 结构 \_ \_ **](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 。 它包含在 [**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 结构中。

IRP \_ MJ \_ 设备 \_ 控制可以是基于 IRP 的操作，也可以是快速的 i/o 操作。

IRP \_ MJ \_ 内部 \_ 设备 \_ 控制是基于 IRP 的 i/o 操作。

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
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT \_ 是 \_ FASTIO \_ 操作**](/windows-hardware/drivers/ddi/index)

[**FLT \_ 为 \_ FS \_ 筛选器 \_ 操作**](/previous-versions/ff544648(v=vs.85))

[**FLT \_ 是 \_ IRP \_ 操作**](/previous-versions/ff544654(v=vs.85))

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltDeviceIoControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)

[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IRP \_ MJ \_ 设备 \_ 控制**](irp-mj-device-control.md)

[**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md)

[**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)

[**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwDeviceIoControlFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwdeviceiocontrolfile)

 

