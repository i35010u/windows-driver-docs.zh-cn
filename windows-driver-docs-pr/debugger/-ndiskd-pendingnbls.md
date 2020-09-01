---
title: ndiskd.pendingnbls
description: Pendingnbls 扩展显示正在传输 (NET_BUFFER_LISTs) 挂起的 Nbl。
ms.assetid: 9137B995-FCCA-4E25-85D3-FCB5B717EBDF
keywords:
- ndiskd pendingnbls Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pendingnbls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5e79b3a9f4f0772de83a179fd4a76fe2618b079
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217949"
---
# <a name="ndiskdpendingnbls"></a>!ndiskd.pendingnbls

**！ Ndiskd pendingnbls**将显示正在传输中的挂起 Nbl ([**NET \_ BUFFER \_ 列表**](../network/net-buffer-list-structure.md)) 。

```console
!ndiskd.pendingnbls [-handle <x>] [-fullstack] [-verbosity <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 微型端口、筛选器或打开的句柄。

<span id="_______-fullstack______"></span><span id="_______-FULLSTACK______"></span>*-fullstack*   
显示与句柄关联的整个堆栈中的挂起 Nbl。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span>*-详细级别*   
要显示的详细信息的级别。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

**！ ndiskd。 pendingnbls** 可以传递 NDIS 微型端口、筛选器或打开的句柄。 以下一系列示例使用微型端口句柄。 若要查看所有微型端口及其关联微型驱动程序的列表，请运行不带参数的[**！ ndiskd。**](-ndiskd-netadapter.md) 在下面的示例输出中，查找 "Microsoft 内核调试" 网络适配器，其句柄为 ffffe00bc3f701a0。 其微型驱动程序句柄为 ffffe00bc51b9ae0。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffe00bc6e12ae0   ffffe00bc6e4e1a0    Microsoft ISATAP Adapter #2
    ffffe00bc51b9ae0   ffffe00bc3f701a0    Microsoft Kernel Debug Network Adapter
```

若要查看微型端口的挂起 Nbl，请在其微型驱动程序的 SendNetBufferListsHandler 上设置断点。 使用微型驱动程序的句柄运行 [**！ ndiskd**](-ndiskd-minidriver.md) 命令来查看其处理程序的列表，然后单击 SendNetBufferListsHandler 右侧的 "最佳实践" 链接。 也可以在命令行中输入 [**bp 处理**](bp--bu--bm--set-breakpoint-.md) 命令。

```console
0: kd> !ndiskd.minidriver ffffe00bc51b9ae0 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80ae9618230  bp
    SetOptionsHandler                      fffff80ae9612800  bp
    HaltHandlerEx                          fffff80ae9618040  bp
    ShutdownHandlerEx                      fffff80ae96122c0  bp

    CheckForHangHandlerEx                  fffff80ae9612810  bp
    ResetHandlerEx                         fffff80ae9612f70  bp

    PauseHandler                           fffff80ae9618000  bp
    RestartHandler                         fffff80ae9618940  bp

    OidRequestHandler                      fffff80ae9611c90  bp
    CancelOidRequestHandler                fffff80ae96122c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80ae96189a0  bp

    SendNetBufferListsHandler              fffff80ae9611870  bp
    ReturnNetBufferListsHandler            fffff80ae9611b50  bp
    CancelSendHandler                      fffff80ae96122c0  bp
```

在 SendNetBufferListsHandler 上设置断点后，输入 **g** 命令，让调试对象目标计算机运行并命中断点。

```console
0: kd> bp fffff80ae9611870
0: kd> g
Breakpoint 0 hit
fffff80a`e9611870 4053            push    rbx
```

现在，在命中微型驱动程序的 SendNetBufferListsHandler 断点之后，可以通过使用微型端口的句柄输入 **！ ndiskd** 命令，查看微型端口的任何挂起的 nbl。

**注意**   在此示例中，调试对象目标计算机已在遇到断点时加载网页，因此流量已通过微型端口的数据路径流动。 因此，它有一个要发送的挂起 NBL。 即使在对微型驱动程序的一个或多个 NBL 处理程序设置断点之后，在数据路径中没有活动的情况下，也可能看不到任何挂起的 Nbl。


```console
0: kd> !ndiskd.pendingnbls ffffe00bc3f701a0

PHASE 1/3: Found 20 NBL pool(s).                 
PHASE 2/3: Found 342 freed NBL(s).                                    

    Pending Nbl        Currently held by                                        
    ffffe00bc5545c60   ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter  [NetAdapter]                    
    

PHASE 3/3: Found 1 pending NBL(s) of 4817 total NBL(s).                      
Search complete.
```

## <a name="see-also"></a>另请参阅


[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0) **](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**网络 \_ 缓冲区 \_ 列表**](../network/net-buffer-list-structure.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)

[**bp、bu、bm（设置断点）**](bp--bu--bm--set-breakpoint-.md)