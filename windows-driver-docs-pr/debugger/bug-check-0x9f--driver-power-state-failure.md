---
title: Bug 检查 0x9F DRIVER_POWER_STATE_FAILURE
description: 此 bug 检查的值为0x0000009F。 此 bug 检查表明驱动程序处于不一致或处于无效状态。
ms.assetid: f767fe80-0ec0-45e4-9949-467f50ac601c
keywords:
- Bug 检查 0x9F DRIVER_POWER_STATE_FAILURE
- DRIVER_POWER_STATE_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_POWER_STATE_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: df50ead9a8bd9398c3df5b3b97cec400bc1b13ce
ms.sourcegitcommit: a54b96c52b0c7009dfa05bcc68d210b13711f2ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77601715"
---
# <a name="bug-check-0x9f-driver_power_state_failure"></a>Bug 检查0x9F：驱动程序\_电源\_状态\_故障

驱动程序\_POWER\_状态\_故障 bug 检查的值为0x0000009F。 此 bug 检查表明驱动程序处于不一致或处于无效状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="driver_power_state_failure-parameters"></a>驱动程序\_电源\_状态\_故障参数

参数1指示违规类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Device 对象</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>正在释放的设备对象的电源请求仍未完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>目标设备的设备对象（如果可用）</p></td>
<td align="left"><p>Device 对象</p></td>
<td align="left"><p>驱动程序对象（如果可用）</p></td>
<td align="left"><p>设备对象已完成系统电源状态请求的 i/o 请求数据包（IRP），但未调用<strong>PoStartNextPowerIrp</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>堆栈的物理设备对象（PDO）</p></td>
<td align="left"><p>nt!TRIAGE_9F_POWER。</p></td>
<td align="left"><p>阻止的 IRP</p></td>
<td align="left"><p>设备对象已阻止 IRP 太长时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>超时值（以秒为单位）。</p></td>
<td align="left"><p>当前持有即插即用（PnP）锁的线程。</p></td>
<td align="left"><p>nt!TRIAGE_9F_POWER。</p></td>
<td align="left"><p>等待与 PnP 子系统同步时，电源状态转换超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>堆栈的物理设备对象</p></td>
<td align="left"><p></p>POP_FX_DEVICE 对象</td>
<td align="left"><p>保留-0</p></td>
<td align="left"><p>设备在所需的时间段内未能完成定向的电源转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>POP_FX_DEVICE 对象</p></td>
<td align="left"><p>指示此电源关闭（1）还是通电（0）完成。</p></td>
<td align="left"><p>保留-0</p></td>
<td align="left"><p></p>设备未成功完成其定向的电源转换回拨。</td>
</tr>
<tr class="odd">
<td align="left"><p>0x500</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>目标设备的设备对象（如果可用）</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>设备对象已完成系统电源状态请求的 IRP，但未调用<strong>PoStartNextPowerIrp</strong>。</p></td>
</tr>
</tbody>
</table>

## <a name="cause"></a>原因

有关可能的原因的说明，请参阅 Parameters 部分中每个代码的说明。

## <a name="resolution"></a>分辨率

**当参数1等于0x3 时，调试 bug 检查0x9F**

- 在内核调试器中，使用[ **！分析-v**](-analyze.md)命令执行初始 bug 检查分析。 详细分析显示 nt 的地址 **！会审\_9F\_POWER** structure，它位于 Arg3 中。

```dbgcmd
kd>!analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

    DRIVER_POWER_STATE_FAILURE (9f)
    A driver has failed to complete a power IRP within a specific time.
    Arguments:
    Arg1: 0000000000000003, A device object has been blocking an Irp for too long a time
    Arg2: fffffa8007b13440, Physical Device Object of the stack
    Arg3: fffff8000386c3d8, nt!TRIAGE_9F_POWER on Win7 and higher, otherwise the Functional Device Object of the stack
    Arg4: fffffa800ab61bd0, The blocked IRP
```

Nt！会审\_9F\_POWER structure 提供其他 bug 检查信息，这些信息可能会帮助您确定此错误检查的原因。 此结构可以提供所有未完成的电源 Irp 的列表、所有电源 IRP 工作线程的列表以及指向延迟的系统工作线程队列的指针。

- 使用[**dt （显示类型）** ](dt--display-type-.md)命令，并指定 nt！使用 Arg3 中的地址\_9F\_POWER structure 进行会审。

```dbgcmd
    0: kd> dt nt!TRIAGE_9F_POWER fffff8000386c3d8
       +0x000 Signature        : 0x8000
       +0x002 Revision         : 1
       +0x008 IrpList          : 0xfffff800`01c78bd0 _LIST_ENTRY [ 0xfffffa80`09f43620 - 0xfffffa80`0ad00170 ]
       +0x010 ThreadList       : 0xfffff800`01c78520 _LIST_ENTRY [ 0xfffff880`009cdb98 - 0xfffff880`181f2b98 ]
       +0x018 DelayedWorkQueue : 0xfffff800`01c6d2d8 _TRIAGE_EX_WORK_QUEUE
```

[**Dt （显示类型）** ](dt--display-type-.md)命令显示结构。 你可以使用各种调试器命令\_输入字段列表来检查未完成的 Irp 和 power IRP 工作线程的列表。

- 使用[ **！ irp**](-irp.md)命令检查已阻止的 irp。 此 IRP 的地址位于 Arg4 中。

```dbgcmd
    0: kd> !irp fffffa800ab61bd0
    Irp is active with 7 stacks 6 is current (= 0xfffffa800ab61e08)
     No Mdl: No System Buffer: Thread 00000000:  Irp stack trace.  
         cmd  flg cl Device   File     Completion-Context
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
    >[IRP_MJ_POWER(16), IRP_MN_SET_POWER(2)]
                0 e1 fffffa800783f060 00000000 00000000-00000000    pending
               \Driver\HidUsb
                Args: 00016600 00000001 00000004 00000006
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-fffffa800ad00170    

                Args: 00000000 00000000 00000000 00000000
```

- 使用带有 Arg2 地址的[ **！ devstack**](-devstack.md)命令来显示与错误驱动程序关联的信息。

```dbgcmd
    0: kd> !devstack fffffa8007b13440
      !DevObj           !DrvObj            !DevExt           ObjectName
      fffffa800783f060  \Driver\HidUsb     fffffa800783f1b0  InfoMask field not found for _OBJECT_HEADER at fffffa800783f030

    > fffffa8007b13440  \Driver\usbhub     fffffa8007b13590  Cannot read info offset from nt!ObpInfoMaskToOffset

    !DevNode fffffa8007ac8a00 :
      DeviceInst is "USB\VID_04D8&PID_0033\5&46fa7b7&0&1"
      ServiceName is "HidUsb"
```

- 使用！ poaction 命令显示处理电源操作和任何分配的电源 Irp 的线程。

```dbgcmd
    3: kd> !poaction
    PopAction: fffff801332f3fe0
      State..........: 0 - Idle
      Updates........: 0 
      Action.........: None
      Lightest State.: Unspecified
      Flags..........: 10000003 QueryApps|UIAllowed
      Irp minor......: ??
      System State...: Unspecified
      Hiber Context..: 0000000000000000

    Allocated power irps (PopIrpList - fffff801332f44f0)
      IRP: ffffe0001d53d8f0 (wait-wake/S0), PDO: ffffe00013cae060
      IRP: ffffe0001049a5d0 (wait-wake/S0), PDO: ffffe00012d42050
      IRP: ffffe00013d07420 (set/D3,), PDO: ffffe00012daf840, CURRENT: ffffe00012dd5040
      IRP: ffffe0001e5ac5d0 (wait-wake/S0), PDO: ffffe00013d33060
      IRP: ffffe0001ed3e420 (wait-wake/S0), PDO: ffffe00013c96060
      IRP: ffffe000195fe010 (wait-wake/S0), PDO: ffffe00012d32050

    Irp worker threads (PopIrpThreadList - fffff801332f3100)
      THREAD: ffffe0000ef5d040 (static)
      THREAD: ffffe0000ef5e040 (static), IRP: ffffe00013d07420, DEVICE: ffffe00012dd5040

    PopAction: fffff801332f3fe0
      State..........: 0 - Idle
      Updates........: 0 
      Action.........: None
      Lightest State.: Unspecified
      Flags..........: 10000003 QueryApps|UIAllowed
      Irp minor......: ??
      System State...: Unspecified
      Hiber Context..: 0000000000000000

    Allocated power irps (PopIrpList - fffff801332f44f0)
      IRP: ffffe0001d53d8f0 (wait-wake/S0), PDO: ffffe00013cae060
      IRP: ffffe0001049a5d0 (wait-wake/S0), PDO: ffffe00012d42050
      IRP: ffffe00013d07420 (set/D3,), PDO: ffffe00012daf840, CURRENT: ffffe00012dd5040
      IRP: ffffe0001e5ac5d0 (wait-wake/S0), PDO: ffffe00013d33060
      IRP: ffffe0001ed3e420 (wait-wake/S0), PDO: ffffe00013c96060
      IRP: ffffe000195fe010 (wait-wake/S0), PDO: ffffe00012d32050

    Irp worker threads (PopIrpThreadList - fffff801332f3100)
      THREAD: ffffe0000ef5d040 (static)
      THREAD: ffffe0000ef5e040 (static), IRP: ffffe00013d07420, DEVICE: ffffe00012dd5040
```

- 如果使用的是 KMDF 驱动程序，请使用[Windows 驱动程序框架扩展](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)（！ wdfkd）来收集其他信息。

  使用[ **！ wdfkd**](-wdfkd-wdflogdump.md)将驱动程序名称&gt;&lt;，以查看 KMDF 是否正在等待确认任何挂起的请求。

  使用[ **！ wdfdevicequeues**](-wdfkd-wdfdevicequeues.md) &lt;你的 WDFDEVICE&gt;，以检查所有未完成的请求及其所处状态。

- 使用[ **！** ](-stacks.md) stack 扩展来检查每个线程的状态，并查找可能会保持电源状态转换的线程。

- 为了帮助你确定错误的原因，请考虑以下问题：

  - 物理设备对象（PDO）驱动程序（Arg2）有哪些特征？
  - 是否可以找到被阻止的线程？ 当你检查带有[ **！ thread**](-thread.md)调试器命令的线程时，该线程包含哪些内容？
  - 是否存在与阻止它的线程关联的 IO？ 堆栈上有哪些符号？
  - 检查已阻止的电源 IRP 后，你会注意到什么？
  - Power IRP 的 PnP 次要功能代码是什么？

**当参数1等于0x4 时调试 bug 检查0x9F**

- 在内核调试器中，使用[ **！分析-v**](-analyze.md)命令执行初始 bug 检查分析。 详细分析显示 nt 的地址 **！会审\_9F\_PNP**结构，该结构位于参数4（arg4）中。

```dbgcmd
    kd> !analyze -v
    *******************************************************************************
    *                                                                             *
    *                        Bugcheck Analysis                                    *
    *                                                                             *
    *******************************************************************************

    DRIVER_POWER_STATE_FAILURE (9f)
    A driver has failed to complete a power IRP within a specific time (usually 10 minutes).
    Arguments:
    Arg1: 00000004, The power transition timed out waiting to synchronize with the Pnp
            subsystem.
    Arg2: 00000258, Timeout in seconds.
    Arg3: 84e01a70, The thread currently holding on to the Pnp lock.
    Arg4: 82931b24, nt!TRIAGE_9F_PNP on Win7

```

Nt！会审\_9F\_PNP 结构提供可帮助您确定错误原因的其他 bug 检查信息。 Nt！会审\_9F\_PNP 结构提供一个指向结构的指针，该结构包含已调度（但未完成） PnP Irp 的列表，并提供指向延迟的系统工作队列的指针。

- 使用[**dt （显示类型）** ](dt--display-type-.md)命令，并指定**nt！会审\_9F\_PNP**结构和在 Arg4 中找到的地址。

```dbgcmd
    kd> dt nt!TRIAGE_9F_PNP 82931b24
       +0x000 Signature        : 0x8001
       +0x002 Revision         : 1
       +0x004 CompletionQueue  : 0x82970e20 _TRIAGE_PNP_DEVICE_COMPLETION_QUEUE
       +0x008 DelayedWorkQueue : 0x829455bc _TRIAGE_EX_WORK_QUEUE

```

[**Dt （显示类型）** ](dt--display-type-.md)命令显示结构。 您可以使用调试器命令\_输入字段列表来检查未完成的 PnP Irp 的列表。

为了帮助你确定错误的原因，请考虑以下问题：

- 是否存在与该线程关联的 IRP？
- CompletionQueue 中是否有任何 IO？
- 堆栈上有哪些符号？

- 请参阅上述参数0x3 下介绍的其他技术。

## <a name="remarks"></a>备注
----------

如果你不能使用上述方法来调试此问题，则可以使用一些基本的故障排除方法。

- 如果最近添加了新的设备驱动程序或系统服务，请尝试删除或更新它们。 尝试确定系统中发生了导致新 bug 检查代码的更改。

- 查看**设备管理器**，查看是否有任何设备标记为惊叹号（！）。 查看在驱动程序属性中显示的任何错误驱动程序的事件日志。 请尝试更新相关驱动程序。

- 检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 有关详细信息，请参阅[Open 事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在与蓝色屏幕相同的时间范围内查找系统日志中的严重错误。

- 若要尝试并找出原因，暂时将使用 "控制面板" 的 "电源选项" 禁用省电。 某些驱动程序问题与系统休眠的各种状态、挂起和恢复电源相关。

- 如果最近向系统中添加了硬件，请尝试删除或替换它。 或与制造商联系，查看是否有可用的修补程序。

- 你可以尝试运行系统制造商提供的硬件诊断。

- 请与制造商联系，以了解是否有更新的系统 ACPI/BIOS 或其他固件可用。
