---
title: ndiskd.ndisrwlock
description: Ndiskd. ndisrwlock 扩展显示 NDIS_RW_LOCK_EX 锁结构的相关信息。
ms.assetid: 853CBAFE-3899-4983-BFC7-933D3BC7ADA1
keywords:
- ndiskd ndisrwlock Windows 调试
ms.date: 06/18/2020
topic_type:
- apiref
api_name:
- ndiskd.ndisrwlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6ce40c0652d57e6a941f19bc1f99e7673cb92bbb
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593923"
---
# <a name="ndiskdndisrwlock"></a>!ndiskd.ndisrwlock

**！ Ndiskd ndisrwlock**扩展显示有关[**NDIS \_ RW \_ 锁 \_ EX**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567279(v=vs.85))锁结构的信息。

```console
!ndiskd.ndisrwlock -handle <x>
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 锁结构的句柄。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

如果创建自己的 RW 锁并想要对其进行检查，请使用 **！ ndiskd。** 若要获取 RW 锁的句柄，请使用*poi*命令取消引用驱动程序的锁定地址。 以下代码片段演示了如何在示例中查看 TCIPIP 协议使用的锁定。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   0 references

    Set a breakpoint on acquire/release
```

若要使用此 RW 锁观察驱动程序，请单击 RW 锁详细信息底部的 "获取/释放时设置断点" 链接。 设置断点后，输入**g**命令，让调试对象计算机运行并命中断点。

```console
0: kd> ba r4 ffffe00bc3fc22f8
0: kd> g
Breakpoint 0 hit
nt!KeTestSpinLock+0x3:
fffff802`0d69eb53 4885c0          test    rax,rax
```

现在，你可以重新运行同一 **！ ndiskd**命令，以查看此 RW 锁定是否有一个只读访问引用。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   1 reference

    Set a breakpoint on acquire/release
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd.dll）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS \_ RW \_ LOCK （ \_ EX）**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567279(v=vs.85))
