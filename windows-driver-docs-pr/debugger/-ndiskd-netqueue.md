---
title: ndiskd.netqueue
description: Ndiskd. netqueue 扩展显示有关 NETTXQUEUE 或 NETRXQUEUE 对象的信息。
ms.assetid: 101F29AA-5CEE-41F8-A3EC-AA2E74B8E074
keywords:
- ndiskd netqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a49ac36a65d06b194152e8c04aa07528de5cd5e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826550"
---
# <a name="ndiskdnetqueue"></a>!ndiskd.netqueue


**！ Ndiskd netqueue**扩展显示有关 NETTXQUEUE 或 NETRXQUEUE 对象的信息。

有关网络适配器 WDF 类扩展（NetAdapterCx）的详细信息，请参阅[网络适配器 Wdf 类扩展（Cx）](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.netqueue [-handle <x>] [-basic] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 NETTXQUEUE 或 NETRXQUEUE 的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
显示基本信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

**注意**  查看[对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)，以查看一个关系图，该关系图说明了 NETTXQUEUE 和 NETRXQUEUE 对象与 NetAdapterCx 中的其他对象之间的关系。

 

若要获取 NETTXQUEUE 或 NETRXQUEUE 的句柄，请执行以下步骤：

1.  运行[ **！ ndiskd. get-netadapter**](-ndiskd-netadapter.md)扩展。
2.  单击安装了 NetAdapterCx 驱动程序的 Get-netadapter 的句柄。
3.  单击 Get-netadapter 的 GET-NETADAPTER 对象右侧的 "详细信息" 链接，以运行[ **！ ndiskd. cxadapter**](-ndiskd-cxadapter.md)扩展。
4.  输入包含 *-数据路径*参数的 **！ cxadapter**命令，以查看 get-netadapter 的数据路径队列。

有关此过程的详细信息，请参阅 **！ ndiskd. cxadapter**主题中的示例。
在下面的示例中，查找此 GET-NETADAPTER 的 NETTXQUEUE，ffffd1022f512700 的句柄。

```console
0: kd> !ndiskd.cxadapter ffffd1022f1a0720 -basic -datapath


NETADAPTER

    Miniport           ffffd1022d048030 - Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    NETADAPTER         00002efdd0e5f988    
    WDFDEVICE          00002efdcf45f2f8   

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtAdapterCreateTxQueue                fffff80034151508   RtEthSample+1508
    EvtAdapterCreateRxQueue                fffff800341510ec   RtEthSample+10ec


DATAPATH QUEUES

    NETTXQUEUE         ffffd1022f512700
    NETRXQUEUE         ffffd1022cc7b0d0
```

通过单击 NETTXQUEUE 的句柄或在命令行中输入 **！ ndiskd**命令，你可以查看此队列的详细信息，包括其伴生 WDF 对象的句柄、其环形缓冲区的句柄和其已注册回调的函数指针。

```console
0: kd> !ndiskd.netqueue ffffd1022f512700

    NETTXQUEUE         00002efdd0aed9a8
    Ring buffer        ffffd1022d000000

    Switch to EC thread

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtQueueAdvance                        fffff80034152af8   RtEthSample+2af8
    EvtQueueArmNotification                fffff80034159a94   RtEthSample+9a94
    EvtQueueCancel                         fffff800341598d8   RtEthSample+98d8
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

[网络适配器 WDF 类扩展（Cx）](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[对象摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[ **！ ndiskd. get-netadapter**](-ndiskd-netadapter.md)

[ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

 

 






