---
title: FLT_PARAMETERS for IRP_MJ_FILE_SYSTEM_CONTROL union
description: 在 FLT 的 MajorFunction 字段\_IO\_参数\_操作的块结构时使用的联合组件是 IRP\_MJ\_\_SYSTEM\_控件。
ms.assetid: d90b9f23-9fae-46e8-b68c-1ba11b3fa17a
keywords:
- FLT_PARAMETERS for IRP_MJ_FILE_SYSTEM_CONTROL union 可安装的文件系统驱动程序
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
ms.openlocfilehash: 45c677b8b3f6899f54b3258b808681f6ac69a64f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841395"
---
# <a name="flt_parameters-for-irp_mj_file_system_control-union"></a>用于 IRP\_MJ\_文件\_系统\_控制联合的 FLT\_参数


在 FLT 的**MajorFunction**字段[ **\_IO\_参数\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作的块结构时使用的联合组件是[**IRP\_MJ\_\_SYSTEM\_控件**](irp-mj-file-system-control.md)。

<a name="syntax"></a>语法
------

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

<a name="members"></a>成员
-------

**FileSystemControl**  
包含以下成员的结构。

**VerifyVolume**  
用于 IRP\_MN 的联合组件\_验证\_批量操作。

**Vpb**  
指向要验证的卷的卷参数块（VPB）的指针。

**DeviceObject**  
一个指针，指向要验证的卷的设备对象。

**常见问题解答**  
用于 IRP 的所有缓冲方法的联合组件\_MN\_内核\_调用并使用 IRP\_MN\_用户\_FS\_请求操作。

**OutputBufferLength**  
**OutputBuffer**或**OutputBuffer**成员指向的缓冲区的长度（以字节为单位）。

**InputBufferLength**  
**InputBuffer**、 **SystemBuffer**或**InputSystemBuffer**成员指向的缓冲区的长度（以字节为单位）。

**FsControlCode**  
要传递给目标设备的文件系统、文件系统筛选器或微筛选器驱动程序的 FSCTL 函数代码。

有关 IOCTL 和 FSCTL 请求的详细信息，请参阅在 Microsoft Windows SDK 文档中使用*内核模式体系结构指南*中的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)和 "设备输入和输出控制代码"。 （此资源可能在某些语言和国家/地区不可用。）

**但**  
用于 IRP\_MN\_内核\_调用并使用 IRP\_MN\_用户\_FS 的联合组件\_在缓存方法为方法\_时请求操作。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。 （此资源可能在某些语言和国家/地区不可用。）

**InputBuffer**  
输入缓冲区的用户模式虚拟地址，该地址提供了操作的原始请求者。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)等例程，并将所有缓冲区引用包含在**try/except**块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)中[使用缓冲和直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)和错误。 （此资源可能在某些语言和国家/地区不可用。）

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 I/o 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址有效，微筛选器必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)和[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)等例程，并将所有缓冲区引用包含在**try/except**块中。 有关详细信息，请参阅*内核模式体系结构指南*中的在[引用用户空间地址](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)中[使用缓冲和直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)和错误。 （此资源可能在某些语言和国家/地区不可用。）

**OutputMdlAddress**  
描述**两个 OutputBuffer**成员指向的缓冲区的内存描述符列表（MDL）的地址。 此成员是可选的，并且可以为**NULL**。

**缓冲区**  
用于 IRP\_MN 的联合组件\_内核\_调用，并在缓冲方法\_缓存方法时 IRP\_MN\_请求操作。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。 （此资源可能在某些语言和国家/地区不可用。）

**SystemBuffer**  
操作的系统分配的缓冲区的地址。 在\_缓冲 i/o 的方法中，此缓冲区用于输入和输出。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。 （此资源可能在某些语言和国家/地区不可用。）

**直**  
用于 IRP\_MN 的联合组件\_内核\_调用和 IRP\_MN\_用户\_FS\_直接或方法\_中的方法\_时\_请求操作OUT\_DIRECT。 有关缓冲方法的详细信息，请参阅在*内核模式体系结构指南*中[定义 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。

**InputSystemBuffer**  
操作的输入缓冲区的地址。 此缓冲区已被操作系统锁定，以便可以安全地从内核模式进行访问。 有关详细信息，请参阅*内核模式体系结构指南*中的[访问数据缓冲区的方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。 （此资源可能在某些语言和国家/地区不可用。）

**OutputBuffer**  
所提供操作的原始请求者的输出缓冲区的用户模式虚拟地址。 在直接 i/o 中，与方法\_i/o 不同时，操作系统会锁定此缓冲区，以便可以安全地从内核模式进行访问，只要微筛选器与 i/o 操作的原始请求者处于相同的进程上下文中即可。 （否则它必须调用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，以从**OutputMdlAddress**成员指向的 MDL 获取系统地址。）有关详细信息，请参阅*内核模式体系结构指南*中的[直接 I/o 中](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)的[使用直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)和错误。 （此资源可能在某些语言和国家/地区不可用。）

**OutputMdlAddress**  
描述**OutputBuffer**成员指向的缓冲区的 MDL 地址。 此成员是必需的，不能为**NULL**。

<a name="remarks"></a>备注
-------

[**IRP\_MJ\_文件\_系统\_控制**](irp-mj-file-system-control.md)操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含回调数据表示的文件系统控制信息操作的参数（[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)）结构。 它包含在[**FLT\_IO\_参数\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构。

IRP\_MJ\_文件\_系统\_控件是基于 IRP 的操作。

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

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoVerifyVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioverifyvolume)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






