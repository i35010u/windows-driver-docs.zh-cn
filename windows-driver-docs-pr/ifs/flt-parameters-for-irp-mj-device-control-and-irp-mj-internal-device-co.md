---
title: FLT_PARAMETERS for IRP_MJ_DEVICE_CONTROL and IRP_MJ_INTERNAL_DEVICE_CONTROL union
description: 在 FLT 的 MajorFunction 字段\_IO\_参数\_操作的块结构时使用的联合组件是 IRP\_MJ\_设备\_控件，或 IRP\_内部\_获取\_t_9_ 控件。
ms.assetid: ed2da1d5-838e-41a4-9a26-c61518da9cf3
keywords:
- FLT_PARAMETERS for IRP_MJ_DEVICE_CONTROL 和 IRP_MJ_INTERNAL_DEVICE_CONTROL union 可安装的文件系统驱动程序
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
ms.openlocfilehash: a217db598899e9206e3bcf405d79c39aed7cd538
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841386"
---
# <a name="flt_parameters-for-irp_mj_device_control-and-irp_mj_internal_device_control-union"></a>FLT\_IRP\_MJ\_设备\_控制和 IRP\_MJ\_内部\_设备\_控制联合


在 FLT 的**MajorFunction**字段[ **\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的块结构时使用的联合组件是[**IRP\_mj\_设备\_控件**](irp-mj-device-control.md)或[**IRP\_mj\_内部\_设备\_控制**](irp-mj-internal-device-control.md)。

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
**常见问题解答**  
用于所有缓冲方法的联合组件。

**OutputBufferLength**  
**不是 OutputBuffer**、 **OutputBuffer**或**FastIo**成员指向的缓冲区的长度（以字节为单位）。

**InputBufferLength**  
**InputBuffer**、 **SystemBuffer**、 **InputSystemBuffer**或**FastIo**成员指向的缓冲区的长度（以字节为单位）。

**IoControlCode**  
要传递给目标设备的设备驱动程序的 IOCTL 函数代码。

有关 IOCTL 请求的详细信息，请参阅 Microsoft Windows SDK 文档中的使用*内核模式体系结构指南*中的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)和 "设备输入和输出控制代码"。 （此资源可能在某些语言和国家/地区不可用。）

**但**  
缓冲方法为方法时使用的联合组件\_都不是。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。

**InputBuffer**  
输入缓冲区的用户模式虚拟地址，该地址提供了操作的原始请求者。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在**try/except**块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)中[使用缓冲和直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)和错误。 （此资源可能在某些语言和国家/地区不可用。）

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在**try/except**块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)中[使用缓冲和直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)和错误。

**OutputMdlAddress**  
描述*两个 OutputBuffer*成员指向的缓冲区的内存描述符列表（MDL）的地址。 此成员是可选的，并且可以为**NULL**。

**缓冲区**  
\_缓冲缓存方法时使用的联合组件。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。 （此资源可能在某些语言和国家/地区不可用。）

**SystemBuffer**  
操作的系统分配的缓冲区的地址。 在\_缓冲 i/o 的方法中，此缓冲区用于输入和输出。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。 （此资源可能在某些语言和国家/地区不可用。）

**直**  
当缓存方法是方法\_\_直接或方法\_OUT\_直接时使用的联合组件。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。 （此资源可能在某些语言和国家/地区不可用。）

**InputSystemBuffer**  
操作的输入缓冲区的地址。 此缓冲区已被操作系统锁定，以便可以安全地从内核模式进行访问。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。 （此资源可能在某些语言和国家/地区不可用。）

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 在直接 i/o 中，与方法\_i/o 不同时，操作系统会锁定此缓冲区，以便可以安全地从内核模式进行访问，只要微筛选器与 i/o 操作的原始请求者处于相同的进程上下文中即可。 （否则它必须调用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)以从**OutputMdlAddress**成员指向的内存描述符列表（MDL）中获取系统地址。）有关详细信息，请参阅*内核模式体系结构指南*中的[直接 I/o 中](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)的[使用直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)和错误。 （此资源可能在某些语言和国家/地区不可用。）

**OutputMdlAddress**  
描述**OutputBuffer**成员指向的缓冲区的 MDL 地址。 此成员是必需的，不能为**NULL**。

**FastIo**  
当[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)结构表示快速 i/o IRP\_MJ\_设备\_控制操作时使用的联合组件。

**InputBuffer**  
输入缓冲区的用户模式虚拟地址，该地址提供了操作的原始请求者。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在**try/except**块中。 有关详细信息，请参阅*内核模式体系结构指南*中的[引用用户空间地址中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)。 （此资源可能在某些语言和国家/地区不可用。）

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)等例程，并将所有缓冲区引用包含在**try/except**块中。 有关详细信息，请参阅*内核模式体系结构指南*中的[引用用户空间地址中的错误](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)。 （此资源可能在某些语言和国家/地区不可用。）

<a name="remarks"></a>备注
-------

[**Irp\_mj\_设备\_控制**](irp-mj-device-control.md)和 IRP\_[**FLT 的\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构\_[**内部\_设备\_控件**](irp-mj-internal-device-control.md)操作包含基于 IRP 的设备 i/o 控制信息操作，由回调数据（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构表示。 它包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

IRP\_MJ\_设备\_控制可以是基于 IRP 的操作，也可以是快速的 i/o 操作。

IRP\_MJ\_内部\_设备\_控件是基于 IRP 的 i/o 操作。

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

[**FltDeviceIoControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IRP\_MJ\_设备\_控件**](irp-mj-device-control.md)

[**IRP\_MJ\_内部\_设备\_控制**](irp-mj-internal-device-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






