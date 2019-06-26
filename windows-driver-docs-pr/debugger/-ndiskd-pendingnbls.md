---
title: ndiskd.pendingnbls
description: Ndiskd.pendingnbls 扩展显示功能的 Nbl (NET_BUFFER_LISTs) 在传输过程中所做的挂起。
ms.assetid: 9137B995-FCCA-4E25-85D3-FCB5B717EBDF
keywords:
- ndiskd.pendingnbls Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pendingnbls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d160bc4300164e477624716ca41f5c989f599a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362459"
---
# <a name="ndiskdpendingnbls"></a>!ndiskd.pendingnbls


**！ Ndiskd.pendingnbls**扩展插件都会显示挂起的功能的 Nbl ([**NET\_缓冲区\_列出**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)) 位于在传输过程中。

```console
!ndiskd.pendingnbls [-handle <x>] [-fullstack] [-verbosity <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 微型端口、 筛选器或打开的句柄。

<span id="_______-fullstack______"></span><span id="_______-FULLSTACK______"></span> *-fullstack*   
显示挂起的功能的 Nbl 从整个堆栈与句柄关联。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-verbosity*   
要显示的详细信息级别。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

**！ ndiskd.pendingnbls**可以传递 NDIS 微型端口、 筛选器或打开的句柄。 以下一系列示例使用微型端口句柄。 若要查看所有微型端口和其关联的微型驱动程序的列表，请运行[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)不带任何参数的扩展。 在以下示例输出中，查找 Microsoft 内核调试网络适配器，其句柄是 ffffe00bc3f701a0。 其微型驱动程序的句柄是 ffffe00bc51b9ae0。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffe00bc6e12ae0   ffffe00bc6e4e1a0    Microsoft ISATAP Adapter #2
    ffffe00bc51b9ae0   ffffe00bc3f701a0    Microsoft Kernel Debug Network Adapter
```

若要查看的微型端口挂起功能的 Nbl，请在其微型驱动程序 SendNetBufferListsHandler 上设置断点。 使用微型驱动程序的句柄来运行[ **！ ndiskd.minidriver-处理的处理程序**](-ndiskd-minidriver.md)命令以查看其处理程序的列表，然后单击 SendNetBufferListsHandler 右侧的"最佳实践"链接。 或者，可以输入[**最佳实践-处理**](bp--bu--bm--set-breakpoint-.md)命令在命令行中。

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

在后 SendNetBufferListsHandler 上设置断点，请输入**g**命令，以使调试对象目标计算机运行并命中断点。

```console
0: kd> bp fffff80ae9611870
0: kd> g
Breakpoint 0 hit
fffff80a`e9611870 4053            push    rbx
```

现在，达到后微型驱动程序的 SendNetBufferListsHandler 断点，可以查看所有挂起的功能的 Nbl 微型端口通过输入 **！ ndiskd.pendingnbls-处理**命令与微型端口的句柄。

**请注意**  调试对象目标计算机在此示例中加载网页时它命中了断点，因此流量已流经微型端口的数据路径。 因此，它必须发送挂起 NBL。 即使微型驱动程序的一个或多个 NBL 处理程序上设置断点，您可能无法看到任何挂起功能的 Nbl 数据路径中没有任何活动。

 

```console
0: kd> !ndiskd.pendingnbls ffffe00bc3f701a0

PHASE 1/3: Found 20 NBL pool(s).                 
PHASE 2/3: Found 342 freed NBL(s).                                    

    Pending Nbl        Currently held by                                        
    ffffe00bc5545c60   ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter  [NetAdapter]                    
    

PHASE 3/3: Found 1 pending NBL(s) of 4817 total NBL(s).                      
Search complete.
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[ **!ndiskd.netadapter**](-ndiskd-netadapter.md)

[ **!ndiskd.minidriver**](-ndiskd-minidriver.md)

[**最佳实践，bu，bm （设置断点）** ](bp--bu--bm--set-breakpoint-.md)

 

 






