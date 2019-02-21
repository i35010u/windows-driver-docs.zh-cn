---
title: FLT_PARAMETERS IRP_MJ_FILE_SYSTEM_CONTROL 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_文件\_系统\_控件。
ms.assetid: d90b9f23-9fae-46e8-b68c-1ba11b3fa17a
keywords:
- FLT_PARAMETERS IRP_MJ_FILE_SYSTEM_CONTROL 联合可安装文件系统驱动程序
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
ms.openlocfilehash: 0ca2f3ef8578319931d84f71dbd22abeac525f88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524214"
---
# <a name="fltparameters-for-irpmjfilesystemcontrol-union"></a>FLT\_IRP 的参数\_MJ\_文件\_系统\_控件联合


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构操作已[ **IRP\_MJ\_文件\_系统\_控制**](irp-mj-file-system-control.md)。

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
结构，它包含以下成员。

**VerifyVolume**  
联合组件用于 IRP\_MN\_验证\_批量操作。

**Vpb**  
要验证的卷的卷参数块 (VPB) 的指针。

**DeviceObject**  
指向要验证的卷的设备对象指针。

**Common**  
联合的组件的所有缓冲的方法用于 IRP\_MN\_内核\_调用和 IRP\_MN\_用户\_FS\_请求操作。

**OutputBufferLength**  
缓冲区的长度，以字节为单位，该**Neither.OutputBuffer**或**Direct.OutputBuffer**成员指向。

**InputBufferLength**  
缓冲区的长度，以字节为单位，该**Neither.InputBuffer**， **Buffered.SystemBuffer**，或**Direct.InputSystemBuffer**成员指向。

**FsControlCode**  
要传递到文件系统、 文件系统筛选器或微筛选器驱动程序为目标设备的 FSCTL 函数代码。

IOCTL 和 FSCTL 请求有关的详细信息，请参阅[使用的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565406)中*内核模式体系结构指南*和"设备输入和输出控制代码"Microsoft Windows SDK 中文档。 （此资源可能不会在某些语言和国家/地区中可用。）

**既不**  
联合组件用于 IRP\_MN\_内核\_调用和 IRP\_MN\_用户\_FS\_请求操作的缓冲方法方法时\_NEITHER. 缓冲方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**InputBuffer**  
输入缓冲区的操作的原始请求者提供的用户模式虚拟地址。 I/O 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址都有效，微筛选器必须使用例程，例如[ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)， [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)，和[ **MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)，封闭中的所有缓冲区引用**试用 / 除外**块。 有关详细信息，请参阅[使用既不缓冲 Nor 直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565432)并[引用用户空间地址中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputBuffer**  
输出缓冲区的操作的原始请求者提供的用户模式虚拟地址。 I/O 管理器和筛选器管理器不会验证这些地址。 若要确保用户空间地址都有效，微筛选器必须使用例程，例如[ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)， [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)，和[ **MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)，封闭中的所有缓冲区引用**试用 / 除外**块。 有关详细信息，请参阅[使用既不缓冲 Nor 直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565432)并[引用用户空间地址中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544308)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputMdlAddress**  
描述缓冲区的内存描述符列表 (MDL) 的地址， **Neither.OutputBuffer**成员指向。 此成员是可选的可以是**NULL**。

**缓冲**  
联合组件用于 IRP\_MN\_内核\_调用和 IRP\_MN\_用户\_FS\_请求操作的缓冲方法方法时\_缓冲处理。 缓冲方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**SystemBuffer**  
该操作所系统分配的缓冲区的地址。 在方法中\_缓冲 I/O，该缓冲区用于同时输入和输出。 有关详细信息，请参阅[方法的访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff554436)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**Direct**  
联合组件用于 IRP\_MN\_内核\_调用和 IRP\_MN\_用户\_FS\_请求操作的缓冲方法方法时\_中\_直接或方法\_出\_直接。 缓冲方法的详细信息，请参阅[定义的 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff543023)中*内核模式体系结构指南*。

**InputSystemBuffer**  
该操作的输入缓冲区的地址。 此缓冲区已被锁定操作系统，以便安全地从内核模式下访问。 有关详细信息，请参阅[方法的访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff554436)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputBuffer**  
输出缓冲区的操作的原始请求者提供的用户模式虚拟地址。 在直接 I/O，方法与\_既不 I/O 操作系统锁定此缓冲区，这样就可以安全地从内核模式下访问，只要微筛选器是在原始请求方的 I/O 操作在同一进程上下文中。 (否则它必须调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)到从 MDL 获取系统地址**OutputMdlAddress**成员指向。)有关详细信息，请参阅[使用直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565372)并[直接 I/O 中的错误](https://msdn.microsoft.com/library/windows/hardware/ff544300)中*内核模式体系结构指南*。 （此资源可能不会在某些语言和国家/地区中可用。）

**OutputMdlAddress**  
描述缓冲区 MDL 地址的**Direct.OutputBuffer**成员指向。 此成员是必需的不能**NULL**。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构[ **IRP\_MJ\_文件\_系统\_控件** ](irp-mj-file-system-control.md)操作包含回调数据所表示的文件系统控制信息操作的参数 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 结构。 包含在[ **FLT\_IO\_参数\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff544638)结构。

IRP\_MJ\_文件\_系统\_控件是一个基于 IRP 的操作。

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
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)

[**IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)

[**IoVerifyVolume**](https://msdn.microsoft.com/library/windows/hardware/ff548559)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)

[**MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)

[**ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)

[**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






