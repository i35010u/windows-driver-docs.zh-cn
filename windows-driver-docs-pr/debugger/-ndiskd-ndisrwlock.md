---
title: ndiskd.ndisrwlock
description: Ndiskd.ndisrwlock 扩展显示 NDIS_RW_LOCK_EX 锁结构的信息。
ms.assetid: 853CBAFE-3899-4983-BFC7-933D3BC7ADA1
keywords:
- ndiskd.ndisrwlock Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisrwlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5eade89a5ee63a7148921a15397a2e507ded645e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335921"
---
# <a name="ndiskdndisrwlock"></a>!ndiskd.ndisrwlock


**！ Ndiskd.ndisrwlock**扩展显示有关的信息[ **NDIS\_RW\_锁\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff567279)锁定结构。

```console
!ndiskd.ndisrwlock [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 锁结构的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

使用 **！ ndiskd.ndisrwlock**扩展，如果创建自己的读写锁，并且想对其进行检查。 若要获取的读写锁的句柄，请使用*poi*命令来取消引用的驱动程序的锁的地址。 以下代码片段演示如何查看 TCIPIP 协议已在该示例时使用的锁。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   0 references

    Set a breakpoint on acquire/release
```

若要发现使用此 RW 锁的驱动程序，请单击底部的读写锁的详细信息的"获取/释放上设置断点"链接。 设置断点后, 输入**g**命令，以使调试对象机器运行并命中断点。

```console
0: kd> ba r4 ffffe00bc3fc22f8
0: kd> g
Breakpoint 0 hit
nt!KeTestSpinLock+0x3:
fffff802`0d69eb53 4885c0          test    rax,rax
```

现在可以重新运行相同 **！ ndiskd.ndisrwlock**命令以查看此 RW 锁具有只读访问权限的一个引用。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   1 reference

    Set a breakpoint on acquire/release
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS\_RW\_LOCK\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff567279)

 

 






