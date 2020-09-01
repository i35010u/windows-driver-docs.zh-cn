---
title: ndiskd.nbllog
description: Ndiskd. nbllog 扩展显示系统上所有 NBL (NET_BUFFER_LIST) 活动的日志。
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
ms.openlocfilehash: b9d984024176fa5fc634d4d7f4bfd9797bb07acf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216762"
---
# <a name="ndiskdnbllog"></a>!ndiskd.nbllog


**！ Ndiskd nbllog**扩展显示系统上所有 NBL ([**NET \_ BUFFER \_ LIST**](../network/net-buffer-list-structure.md)) 活动的日志。

```console
!ndiskd.nbllog [-stacks] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-stacks______"></span><span id="_______-STACKS______"></span>*-堆栈*   
包括调用堆栈。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

**重要提示**   
 **！ ndiskd。 nbllog**需要在调试对象目标计算机上启用 NBL 跟踪。 默认情况下，不会在 Windows 的所有配置中启用 NBL 跟踪。 如果未启用 NBL 跟踪，！ ndiskd 将为你提供有关如何启用它的说明，如以下代码片段所示。

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

 

NBL 日志显示系统上的网络流量。 [**！ ndiskd netreport**](-ndiskd-netreport.md) 分析 NBL 跟踪日志以直观地显示此网络流量。 因此，如果未启用 NBL 跟踪， **！ ndiskd** 会显示此信息。

<a name="examples"></a>示例
--------

在目标调试对象计算机上启用 NBL 跟踪后，输入 **！ ndiskd nbllog** 命令，查看系统上所有 NBL 流量的日志。 如以下示例中所示，运行不带参数的 **！ ndiskd** 会将输出限制为200个事件，通过使用 *-force* 选项重新运行命令，可以绕过这些事件。 为了简洁起见，此示例中的输出的中间 excised。

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

有关如何解释 **！ ndiskd. nbllog**的结果的更详细说明，请参阅 "NDIS 博客上的[！ ndiskd。](/archive/blogs/ndis/ndiskd-nbl-log)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0) **](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**网络 \_ 缓冲区 \_ 列表**](../network/net-buffer-list-structure.md)

[！ ndiskd nbl-log](/archive/blogs/ndis/ndiskd-nbl-log)

 

