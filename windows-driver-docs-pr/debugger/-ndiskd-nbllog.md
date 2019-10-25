---
title: ndiskd.nbllog
description: Ndiskd. nbllog 扩展显示系统上所有 NBL （NET_BUFFER_LIST）活动的日志。
ms.assetid: 59CB6B60-E0B3-435E-A6F6-82A715E87C69
keywords:
- ndiskd nbllog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbllog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0898a87ef75f767eecdb38df4bd3c0f99c04f2ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826620"
---
# <a name="ndiskdnbllog"></a>!ndiskd.nbllog


**！ Ndiskd nbllog**扩展显示系统上所有 NBL （[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)）活动的日志。

```console
!ndiskd.nbllog [-stacks] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-堆栈*   
包括调用堆栈。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="remarks"></a>备注
-------

**重要**  
 **！ nbllog**需要在调试对象目标计算机上启用 NBL 跟踪。 默认情况下，不会在 Windows 的所有配置中启用 NBL 跟踪。 如果未启用 NBL 跟踪，！ ndiskd 将为你提供有关如何启用它的说明，如以下代码片段所示。

```console
0: kd> !ndiskd.nbllog
    This command requires NBL tracking to be enabled on the debugee target
    machine.  (By default, client operating systems have level 1, and servers
    have level 0).  To enable, set this REG_DWORD value to a nonzero value on
    the target machine and reboot the target machine:
    
    HKLM\SYSTEM\CurrentControlSet\Services\NDIS\Parameters ! TrackNblOwner
    Possible Values (features are cumulative)
    * 0:  Disable all tracking.
    * 1:  Track the most recent owner of each NBL (enables !ndiskd.pendingnbls)
    * 2:  Scan for leaks at runtime (use with StuckNblReaction)
    * 3:  Keep a full history of all activity (enables !ndiskd.nbl -log)
    * 4:  Take stack capture snapshots (enables !ndiskd.nbl -log -stacks)
    This command requires level 3 or higher.
```

 

NBL 日志显示系统上的网络流量。 [ **！ ndiskd netreport**](-ndiskd-netreport.md)分析 NBL 跟踪日志以直观地显示此网络流量。 因此，如果未启用 NBL 跟踪， **！ ndiskd**会显示此信息。

<a name="examples"></a>示例
--------

在目标调试对象计算机上启用 NBL 跟踪后，输入 **！ ndiskd nbllog**命令，查看系统上所有 NBL 流量的日志。 如以下示例中所示，运行不带参数的 **！ ndiskd**会将输出限制为200个事件，通过使用 *-force*选项重新运行命令，可以绕过这些事件。 为了简洁起见，此示例中的输出的中间 excised。

```console
0: kd> !ndiskd.nbllog
    NBLs               Processor           Event              Detail            
                                                                     
    ffffe00bc71453f0   CPU  0              Freed
    ffffe00bc7163b40   CPU  2              Allocated
    ffffe00bc7163b40   CPU  2              ProtocolSent       ffffe00bc5ac4880 - QoS Packet Scheduler-0000
    ffffe00bc7163b40   CPU  2              FilterSent         ffffe00bc5ac5c70 - WFP Native MAC Layer LightWeight Filter-0000
    ffffe00bc7163b40   CPU  2, IRQL=DPC    FilterSent         ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc7163b40   CPU  2, IRQL=DPC    SentToMiniport     ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc7163b40   CPU  0, IRQL=DPC    MiniportSendCompleted ffffe00bc5ac5c70 - WFP Native MAC Layer LightWeight Filter-0000
    ffffe00bc7163b40   CPU  0, IRQL=DPC    FilterSendCompleted ffffe00bc5ac4880 - QoS Packet Scheduler-0000
    ffffe00bc7163b40   CPU  0, IRQL=DPC    FilterSendCompleted send complete in NDIS, sorting to Opens
    ffffe00bc7163b40   CPU  0, IRQL=DPC    SendCompleted      ffffe00bc5ab7c10 - TCPIP6

...

    ffffe00bc6b469b0   CPU  2              Allocated
    ffffe00bc6b469b0   CPU  2              Freed
    ffffe00bc64a3690   CPU  2              Allocated
    ffffe00bc64a3690   CPU  2              ProtocolSent       ffffe00bc5ac4880 - QoS Packet Scheduler-0000
    ffffe00bc64a3690   CPU  2              FilterSent         ffffe00bc5ac5c70 - WFP Native MAC Layer LightWeight Filter-0000
    ffffe00bc64a3690   CPU  2, IRQL=DPC    FilterSent         ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc64a3690   CPU  2, IRQL=DPC    SentToMiniport     ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter
    ffffe00bc3cf2d10   CPU  1              Allocated
    ffffe00bc7bc6030   CPU  1              Allocated
    ffffe00bc3cf2d10   CPU  1              ProtocolSent       ffffe00bc5ac4880 - QoS Packet Scheduler-0000

    Maximum of 200 events printed; quitting early.
    Rerun with the '-force' option to bypass this limit.
```

有关如何解释 **！ ndiskd. nbllog**的结果的更详细说明，请参阅 "NDIS 博客上的[！ ndiskd。](https://go.microsoft.com/fwlink/p/?linkid=846176)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[！ ndiskd nbl-log](https://go.microsoft.com/fwlink/p/?linkid=846176)

 

 






