---
title: Bug 检查 0x9F DRIVER_POWER_STATE_FAILURE
description: 此 bug 检查具有 0x0000009F 值。 此 bug 检查指示驱动程序处于不一致或无效的电源状态。
ms.assetid: f767fe80-0ec0-45e4-9949-467f50ac601c
keywords:
- （开发人员内容）Bug 检查 0x9F DRIVER_POWER_STATE_FAILURE
- DRIVER_POWER_STATE_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_POWER_STATE_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f31ab4dc1d224cd9fee54cb0e25f766a92b7f75c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519077"
---
# <a name="developer-content-bug-check-0x9f-driverpowerstatefailure"></a>（开发人员内容）Bug 检查 0x9F:驱动程序\_电源\_状态\_失败


该驱动程序\_电源\_状态\_故障错误检查的值为 0x0000009F。 此 bug 检查指示驱动程序处于不一致或无效的电源状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。

## <a name="driverpowerstatefailure-parameters"></a>驱动程序\_电源\_状态\_失败参数

参数 1 指示冲突的类型。

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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>正在释放的设备对象仍然具有未完成 power 请求尚未完成的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>目标设备的设备对象，如果可用</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>驱动程序对象，如果可用</p></td>
<td align="left"><p>设备对象为系统电源状态请求，完成 I/O 请求数据包 (IRP)，但它未调用<strong>PoStartNextPowerIrp</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>堆栈的物理设备对象 (PDO)</p></td>
<td align="left"><p>堆栈功能的设备对象 (FDO)。 在 Windows 7 及更高版本，nt ！TRIAGE_9F_POWER。</p></td>
<td align="left"><p>被阻止的 IRP</p></td>
<td align="left"><p>设备对象已被阻止了 IRP 太长时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>超时值，以秒为单位。</p></td>
<td align="left"><p>当前持有到-和-插即用 (PnP) 锁的线程。</p></td>
<td align="left"><p>在 Windows 7 及更高版本，nt ！TRIAGE_9F_POWER。</p></td>
<td align="left"><p>电源状态转换操作已超时等待与即插即用的子系统进行同步。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x500</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>目标设备的设备对象，如果可用</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>设备对象完成系统电源状态请求，IRP，但它未调用<strong>PoStartNextPowerIrp</strong>。</p></td>
</tr>
</tbody>
</table>

## <a name="cause"></a>原因
-----

可能的原因的说明，请参阅每个代码的 Parameters 节中的说明。

## <a name="resolution"></a>分辨率
----------

**调试 bug 检查当参数 1 等于 0x3 0x9F**

- 在内核调试程序，使用[ **！ 分析-v** ](-analyze.md)命令来执行初始 bug 检查分析。 详细的分析显示的地址**nt ！会审\_9F\_电源**结构，它是 Arg3 中。

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

Nt ！会审\_9F\_电源结构提供了其他错误检查信息，可帮助你确定此 bug 检查的原因。 结构可以实现一组所有未完成 power Irp，所有 power IRP 工作线程和指向延迟的系统工作队列的列表。

- 使用[ **dt （显示类型）** ](dt--display-type-.md)命令并指定 nt ！会审\_9F\_电源结构使用 Arg3 中的地址。

```dbgcmd
    0: kd> dt nt!TRIAGE_9F_POWER fffff8000386c3d8
       +0x000 Signature        : 0x8000
       +0x002 Revision         : 1
       +0x008 IrpList          : 0xfffff800`01c78bd0 _LIST_ENTRY [ 0xfffffa80`09f43620 - 0xfffffa80`0ad00170 ]
       +0x010 ThreadList       : 0xfffff800`01c78520 _LIST_ENTRY [ 0xfffff880`009cdb98 - 0xfffff880`181f2b98 ]
       +0x018 DelayedWorkQueue : 0xfffff800`01c6d2d8 _TRIAGE_EX_WORK_QUEUE
```

[ **Dt （显示类型）** ](dt--display-type-.md)命令显示的结构。 可以使用各种调试器命令遵循列表\_输入字段来检查未完成的 Irp 和 power IRP 工作线程的列表。

- 使用[ **！ irp** ](-irp.md)命令来检查已被阻止的 IRP。 在了 Arg4 是此 IRP 的地址。

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

- 使用[ **！ devstack** ](-devstack.md) Arg2，以显示与该错误的驱动程序相关联的信息中的 PDO 地址命令。

```dbgcmd
    0: kd> !devstack fffffa8007b13440
      !DevObj           !DrvObj            !DevExt           ObjectName
      fffffa800783f060  \Driver\HidUsb     fffffa800783f1b0  InfoMask field not found for _OBJECT_HEADER at fffffa800783f030

    > fffffa8007b13440  \Driver\usbhub     fffffa8007b13590  Cannot read info offset from nt!ObpInfoMaskToOffset

    !DevNode fffffa8007ac8a00 :
      DeviceInst is "USB\VID_04D8&PID_0033\5&46fa7b7&0&1"
      ServiceName is "HidUsb"
```

- 使用 ！ poaction 命令以显示处理电源操作和任何线程分配 power Irp。

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

- 如果您正在使用 KMDF 驱动程序，使用[Windows 驱动程序框架扩展](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)(！ wdfkd) 若要收集的其他信息。

  使用[ **！ wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md) &lt;驱动程序名称&gt;，以查看是否 KMDF 正在等待您来确认任何挂起的请求。

  使用[ **！ wdfkd.wdfdevicequeues** ](-wdfkd-wdfdevicequeues.md) &lt;你 WDFDEVICE&gt;检查所有未完成的请求和它们处于何种状态。

- 使用[ **！ 堆栈**](-stacks.md)扩展，用于检查每个线程的状态和查找可能会妨碍电源状态转换的线程。

- 若要帮助您确定错误的原因，请考虑以下问题：

  - 物理设备对象 (PDO) 驱动程序 (Arg2) 的特征是什么？
  - 您可以找到阻塞的线程？ 当检查的线程[ **！ 线程**](-thread.md)调试器命令，什么 does 线程组成？
  - 是否有与阻塞的线程关联的 IO？ 符号是什么在堆栈上？
  - 当您检查阻止的 power IRP 时，是否注意到？
  - 什么是 power IRP 的即插即用次要函数代码？

**调试 bug 检查当参数 1 等于 0x4 0x9F**

- 在内核调试程序，使用[ **！ 分析-v** ](-analyze.md)命令来执行初始 bug 检查分析。 详细的分析显示的地址**nt ！会审\_9F\_PNP**结构，它是在参数 4 (了 arg4)。

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

Nt ！会审\_9F\_即插即用结构提供了其他错误检查信息，可帮助你确定错误的原因。 Nt ！会审\_9F\_即插即用结构提供了指向一个结构，其中包含调度 （但未完成） PnP Irp 的列表，并提供指向延迟的系统工作队列的指针的指针。

- 使用[ **dt （显示类型）** ](dt--display-type-.md)命令并指定**nt ！会审\_9F\_PNP**结构和在了 Arg4 中找到的地址。

```dbgcmd
    kd> dt nt!TRIAGE_9F_PNP 82931b24
       +0x000 Signature        : 0x8001
       +0x002 Revision         : 1
       +0x004 CompletionQueue  : 0x82970e20 _TRIAGE_PNP_DEVICE_COMPLETION_QUEUE
       +0x008 DelayedWorkQueue : 0x829455bc _TRIAGE_EX_WORK_QUEUE

```

[ **Dt （显示类型）** ](dt--display-type-.md)命令显示的结构。 可以使用调试器命令遵循列表\_输入字段来检查未完成的 PnP Irp 的列表。

若要帮助您确定错误的原因，请考虑以下问题：

- 是否有与线程关联 IRP？
- CompletionQueue 中是否有任何 IO？
- 符号是什么在堆栈上？

- 请参阅上文所述参数 0x3 下的其他技术。

**时间的差旅跟踪**

如果可以按要求重现 bug 检查，调查花些时间旅行跟踪使用 WinDbg 预览的可能性。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

## <a name="remarks"></a>备注
----------

如果您未配备调试此问题，使用上面所述的技术，可以使用一些基本的故障排除方法。

- 如果最近，添加新设备驱动程序或系统服务尝试删除或更新它们。 尝试确定导致新的错误检查代码才会显示在系统中更改的内容。

- 查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

- 检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

- 若要尝试并找出原因，暂时禁用节能使用控制面板中，电源选项。 某些驱动程序问题与系统休眠和挂起和恢复的能力的各种状态相关。

- 如果你最近添加到系统中，请尝试删除或替换它的硬件。 或者，请与制造商联系，以了解是否有任何修补程序。

- 您可以尝试运行硬件诊断程序提供的系统制造商。

- 请与制造商联系，以查看更新的系统 BIOS ACPI/或其他固件是否可用。
