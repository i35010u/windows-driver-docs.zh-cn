---
title: processirps
description: Processirps 扩展显示有关与进程相关联的 I/O 请求数据包 (Irp) 的信息。
ms.assetid: B7CC72A5-7D3F-4DE5-878D-ABD08BAF227C
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
ms.openlocfilehash: 0cb71473f05a9b37314bf709b23bade760e63a6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544207"
---
# <a name="processirps"></a>!processirps


**！ Processirps**扩展显示有关与进程相关联的 I/O 请求数据包 (Irp) 的信息。

```dbgcmd
!processirps
!processirps ProcessAddress [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_ProcessAddress"></span><span id="_processaddress"></span><span id="_PROCESSADDRESS"></span> **** *ProcessAddress*  
进程的地址。 如果指定*ProcessAddress*，将仅与关联 Irp，显示进程。 如果未指定*ProcessAddress*，显示的所有进程的 Irp。

<span id="_Flags"></span><span id="_flags"></span><span id="_FLAGS"></span> **** *标志*  
一个或多个下列标志的按位 OR。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示 Irp 排队到线程。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示 Irp 排队发送至文件对象。

如果指定*标志*，则还必须指定*ProcessAddress*。 如果未指定*标志*、 Irp 排队到两个线程和显示文件对象。

## <span id="ddk__processfields_dbg"></span><span id="DDK__PROCESSFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

kdexts.dll

<a name="remarks"></a>备注
-------

此命令，可快速确定的过程中，两个排队到线程的和要排队发送至文件对象的任何排队的 Irp。 文件对象具有与之关联的完成端口时，要排队 Irp 发送至文件对象。

<a name="examples"></a>示例
--------

可以使用[ **！ 过程**](-process.md)命令来获取进程的地址。 例如，您无法获取 explorer.exe 的进程地址。

```dbgcmd
2: kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
...
PROCESS fffffa800688c940
    SessionId: 1  Cid: 0bbc    Peb: 7f70da5e000  ParentCid: 0b84
    DirBase: 2db10000  ObjectTable: fffff8a0025bd440  HandleCount: 1056.
    Image: explorer.exe
```

现在可以将传递到 explorer.exe 的进程地址 **！ processirps**命令。 下面的输出显示该 explorer.exe 具有 Irp 排队到线程和 Irp 排队发送至文件对象。

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

 

 





