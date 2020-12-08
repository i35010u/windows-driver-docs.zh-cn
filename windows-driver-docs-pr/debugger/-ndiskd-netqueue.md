---
title: ndiskd.netqueue
description: Ndiskd. netqueue 扩展显示有关 NETTXQUEUE 或 NETRXQUEUE 对象的信息。
keywords:
- ndiskd netqueue Windows 调试
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.netqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27ee6335977759101fdf4daf42d02b22a1708c8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833905"
---
# <a name="ndiskdnetqueue"></a>!ndiskd.netqueue

**！ Ndiskd netqueue** 扩展显示有关 NETTXQUEUE 或 NETRXQUEUE 对象的信息。

有关网络适配器 WDF 类扩展的详细信息 (NetAdapterCx) ，请参阅 [网络适配器 Wdf Class extension (Cx) ](../netcx/index.md)。

```console
!ndiskd.netqueue -handle <x> [-basic]
```

## <a name="parameters"></a>参数

*-handle*   
必需。 NETTXQUEUE 或 NETRXQUEUE 的句柄。

*-基本*   
显示基本信息。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

**注意**  若要查看说明 NETTXQUEUE 和 NETRXQUEUE 对象与 NetAdapterCx 中其他对象的关系的关系图，请参阅 [对象的摘要](../netcx/summary-of-netadaptercx-objects.md) 。

若要获取 NETTXQUEUE 或 NETRXQUEUE 的句柄，请执行以下步骤：

1. 运行 [**！ ndiskd. get-netadapter**](-ndiskd-netadapter.md) 扩展。
2. 单击安装了 NetAdapterCx 驱动程序的 Get-netadapter 的句柄。
3. 单击 Get-netadapter 的 GET-NETADAPTER 对象右侧的 "详细信息" 链接，以运行 [**！ ndiskd. cxadapter**](-ndiskd-cxadapter.md) 扩展。
4. 输入包含 *-数据路径* 参数的 **！ cxadapter** 命令，以查看 get-netadapter 的数据路径队列。

有关此过程的详细信息，请参阅 **！ ndiskd. cxadapter** 主题中的示例。
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

通过单击 NETTXQUEUE 的句柄或在命令行中输入 **！ ndiskd** 命令，你可以查看此队列的详细信息，包括其伴生 WDF 对象的句柄、其环形缓冲区的句柄和其已注册回调的函数指针。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx) ](../netcx/index.md)

[对象摘要](../netcx/summary-of-netadaptercx-objects.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)
