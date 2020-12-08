---
title: processirps
description: Processirps 扩展显示与进程关联 (Irp) 的 i/o 请求包的相关信息。
keywords:
- processirps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- processirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a32457eb36304320a34db7a40c544b04e0c3c119
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787049"
---
# <a name="processirps"></a>!processirps


**！ Processirps** extension 显示与进程关联 (irp) 的 i/o 请求包的相关信息。

```dbgcmd
!processirps
!processirps ProcessAddress [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_ProcessAddress"></span><span id="_processaddress"></span><span id="_PROCESSADDRESS"></span> **** *ProcessAddress*  
进程的地址。 如果指定 *ProcessAddress*，则只显示与该进程关联的 irp。 如果未指定 *ProcessAddress*，则会显示所有进程的 irp。

<span id="_Flags"></span><span id="_flags"></span><span id="_FLAGS"></span> **** *随意*  
以下一个或多个标志的按位 "或"。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示排队到线程的 Irp。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示排队到文件对象的 Irp。

如果指定 *标志*，则还必须指定 *ProcessAddress*。 如果未指定 *标志*，则会显示排队到线程和文件对象的 irp。

## <span id="ddk__processfields_dbg"></span><span id="DDK__PROCESSFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

kdexts.dll

<a name="remarks"></a>备注
-------

使用此命令可以快速标识进程的任何已排队的 Irp，这两种 Irp 都排队到线程中，后者排队到文件对象。 当文件对象具有与之关联的完成端口时，Irp 将排队到文件对象。

<a name="examples"></a>示例
--------

可以使用 [**！ process**](-process.md) 命令获取进程地址。 例如，可以获取 explorer.exe 的进程地址。

```dbgcmd
2: kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
...
PROCESS fffffa800688c940
    SessionId: 1  Cid: 0bbc    Peb: 7f70da5e000  ParentCid: 0b84
    DirBase: 2db10000  ObjectTable: fffff8a0025bd440  HandleCount: 1056.
    Image: explorer.exe
```

现在，你可以将 explorer.exe 的进程地址传递给 **！ processirps** 命令。 以下输出显示，explorer.exe 将 Irp 列队给排队到文件对象的线程和 Irp。

```dbgcmd
2: kd> !processirps fffffa800688c940
**** PROCESS fffffa800688c940 (Image: explorer.exe) ****

Checking threads for IRPs.

  Thread fffffa800689f080:

    IRP fffffa80045ccc10 - Owned by \FileSystem\Ntfs for device fffffa8004f5c030
    IRP fffffa800454f650 - Owned by \FileSystem\Ntfs for device fffffa8004f5c030
    ...
    IRP fffffa80068e9c10 - Owned by \FileSystem\Ntfs for device fffffa8004f5c030

Checking file objects for IRPs.

  FileObject fffffa80068795e0 (handle 8bc):

    IRP fffffa8006590cf0 - Owned by \Driver\DeviceApi for device DeviceApi (fffffa800363ae40)

  ...

  FileObject fffffa8005bf59c0 (handle 900):

    IRP fffffa8006659010 - Owned by \Driver\DeviceApi for device DeviceApi (fffffa800363ae40)
```

 

 





