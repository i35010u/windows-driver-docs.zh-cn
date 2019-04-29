---
title: FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL 和 IRP_MJ_INTERNAL_DEVICE_CONTROL 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_设备\_控件或 IRP\_MJ\_内部\_设备\_控件。
ms.assetid: ed2da1d5-838e-41a4-9a26-c61518da9cf3
keywords:
- FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL 和 IRP_MJ_INTERNAL_DEVICE_CONTROL 联合可安装文件系统驱动程序
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
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5968caf46cf9f62b4f79c3792022716b8d9707f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365011"
---
# <a name="fltparameters-for-irpmjdevicecontrol-and-irpmjinternaldevicecontrol-union"></a>FLT\_IRP 的参数\_MJ\_设备\_控制和 IRP\_MJ\_内部\_设备\_控件联合


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_设备\_控制**](irp-mj-device-control.md)或[ **IRP\_MJ\_内部\_设备\_控制**](irp-mj-internal-device-control.md)。

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
**Common**  
联合组件用于缓冲的所有方法。

**OutputBufferLength**  
缓冲区的长度，以字节为单位，该**Neither.OutputBuffer**， **Direct.OutputBuffer**，或**FastIo.OutputBuffer**成员指向。

**InputBufferLength**  
缓冲区的长度，以字节为单位，该**Neither.InputBuffer**， **Buffered.SystemBuffer**， **Direct.InputSystemBuffer**，或**FastIo.InputBuffer**成员指向。

**IoControlCode**  
IOCTL 函数代码要传递到设备驱动程序为目标设备。

有关 IOCTL 请求的详细信息，请参阅[使用的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)中*内核模式体系结构指南*和"设备输入和输出控制代码"Microsoft Windows SDK 中文档。 （此资源可能不会在某些语言和国家/地区中可用。）

**既不**  
缓冲的方法是方法时使用的联合组件\_NEITHER。 缓冲方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)中*内核模式体系结构指南*。

**InputBuffer**  
输入缓冲区的操作的原始请求者提供的用户模式虚拟地址。 I/O 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址都有效，微筛选器必须使用例程，例如[ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)， [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)，和[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)，封闭中的所有缓冲区引用**试用 / 除外**块。 有关详细信息，请参阅[使用既不缓冲 Nor 直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565432)并[引用用户空间地址中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputBuffer**  
输出缓冲区的操作的原始请求者提供的用户模式虚拟地址。 I/O 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址都有效，微筛选器必须使用例程，例如[ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)， [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)，和[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)，封闭中的所有缓冲区引用**试用 / 除外**块。 有关详细信息，请参阅[使用既不缓冲 Nor 直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565432)并[引用用户空间地址中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)中*内核模式体系结构指南*。

**OutputMdlAddress**  
描述缓冲区的内存描述符列表 (MDL) 的地址， *Neither.OutputBuffer*成员指向。 此成员是可选的可以是**NULL**。

**缓冲**  
缓冲的方法是方法时使用的联合组件\_缓冲。 缓冲方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**SystemBuffer**  
该操作所系统分配的缓冲区的地址。 在方法中\_缓冲 I/O，该缓冲区用于同时输入和输出。 有关详细信息，请参阅[方法的访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff554436)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**Direct**  
缓冲的方法是方法时使用的联合组件\_IN\_直接访问或通过方法\_出\_直接。 缓冲方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**InputSystemBuffer**  
该操作的输入缓冲区的地址。 此缓冲区已被锁定操作系统，以便安全地从内核模式下访问。 有关详细信息，请参阅[方法的访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff554436)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputBuffer**  
输出缓冲区的操作的原始请求者提供的用户模式虚拟地址。 在直接 I/O，方法与\_既不 I/O 操作系统锁定此缓冲区，这样就可以安全地从内核模式下访问，只要微筛选器是在原始请求方的 I/O 操作在同一进程上下文中。 (否则它必须调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)到从内存描述符列表 (MDL) 获取系统地址**OutputMdlAddress**成员将指向.)有关详细信息，请参阅[使用直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565372)并[直接 I/O 中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544300)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputMdlAddress**  
描述缓冲区 MDL 地址的**Direct.OutputBuffer**成员指向。 此成员是必需的不能**NULL**。

**FastIo**  
联合组件时使用[ **FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)结构表示快速 I/O IRP\_MJ\_设备\_控件操作。

**InputBuffer**  
输入缓冲区的操作的原始请求者提供的用户模式虚拟地址。 I/O 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址都有效，微筛选器必须使用例程，例如[ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)， [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)，和[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)，封闭中的所有缓冲区引用**试用 / 除外**块。 有关详细信息，请参阅[中引用用户空间地址错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputBuffer**  
输出缓冲区的操作的原始请求者提供的用户模式虚拟地址。 I/O 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址都有效，微筛选器必须使用例程，例如[ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)， [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)，和[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)，封闭中的所有缓冲区引用**试用 / 除外**块。 有关详细信息，请参阅[中引用用户空间地址错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_设备\_控件**](irp-mj-device-control.md)并[ **IRP\_MJ\_内部\_设备\_控件**](irp-mj-internal-device-control.md)操作包含基于 IRP 的参数表示的回调数据的设备-我/O-控制信息操作 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。

IRP\_MJ\_设备\_控件可以是基于 IRP 的操作或快速 I/O 操作。

IRP\_MJ\_内部\_设备\_控件是一个基于 IRP 的 I/O 操作。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542046)

[**FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL**](irp-mj-internal-device-control.md)

[**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)

[**MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)

[**ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)

[**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






