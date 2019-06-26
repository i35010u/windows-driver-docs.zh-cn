---
title: ndiskd.netqueue
description: Ndiskd.netqueue 扩展显示有关 NETTXQUEUE 或 NETRXQUEUE 对象的信息。
ms.assetid: 101F29AA-5CEE-41F8-A3EC-AA2E74B8E074
keywords:
- ndiskd.netqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f807be64c22b1589d45d020c21788e3a9140dc69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364246"
---
# <a name="ndiskdnetqueue"></a>!ndiskd.netqueue


**！ Ndiskd.netqueue**扩展显示 NETTXQUEUE 或 NETRXQUEUE 对象有关的信息。

有关网络适配器 WDF 类扩展 (NetAdapterCx) 的详细信息，请参阅[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.netqueue [-handle <x>] [-basic] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 NETTXQUEUE 或 NETRXQUEUE 句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示基本信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

**请注意**  请参阅[对象摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)以查看关系图说明 NetAdapterCx 中的其他对象的 NETTXQUEUE 和 NETRXQUEUE 对象的关系。

 

若要获取 NETTXQUEUE 或 NETRXQUEUE 句柄，请执行以下步骤：

1.  运行[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)扩展。
2.  单击已安装了 NetAdapterCx 驱动程序 NetAdapter 句柄。
3.  单击"更多信息"链接到的 NetAdapter 的 NETADAPTER 对象运行的权限[ **！ ndiskd.cxadapter** ](-ndiskd-cxadapter.md)扩展。
4.  输入 **！ ndiskd.cxadapter**命令*的数据路径*参数，以查看该 NETADAPTER 数据路径队列。

有关此过程的详细信息，请参阅 》 上的示例 **！ ndiskd.cxadapter**主题。
在以下示例中，查找为句柄此 NETADAPTER NETTXQUEUE，ffffd1022f512700。

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

通过单击 NETTXQUEUE 的句柄或输入 **！ ndiskd.netqueue-处理**命令在命令行中，你可以看到此队列，其中包括其随附 WDF 对象，其环形缓冲区，窗口的句柄的句柄的详细信息和已注册的回调的函数指针。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[ **!ndiskd.netadapter**](-ndiskd-netadapter.md)

[ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

 

 






