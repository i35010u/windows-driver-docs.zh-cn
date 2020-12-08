---
title: 在 WDF 中调试电源参考漏孔
description: 当 Windows 驱动程序框架 (WDF) 驱动程序调用 WdfDeviceStopIdle 时，框架会递增设备的电源引用计数。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b5a5dfff88b059773984dcf82c76299ed118ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828987"
---
# <a name="debugging-power-reference-leaks-in-wdf"></a>在 WDF 中调试电源参考漏孔


当 Windows 驱动程序框架 (WDF) 驱动程序调用 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)时，框架会递增设备的电源引用计数。 对 **WdfDeviceStopIdle** 的每次成功调用都必须通过调用 [**WdfDeviceResumeIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle) 进行匹配，以减小电源引用计数。

从 Kernel-Mode Driver Framework (KMDF) 1.15 和 User-Mode Driver Framework (UMDF) 2.15 开始，你可以通过使用 [**！ wdfkd**](../debugger/-wdfkd-wdfdevice.md) 和 [**wdfkd**](../debugger/-wdfkd-wdftagtracker.md) 调试器扩展来监视 power reference 的使用情况。 由于性能原因，此功能默认处于禁用状态，因此，你需要使用您尚未 wdfverifier 应用程序或手动编辑驱动程序的服务密钥来启用此功能。

## <a name="wdfverifier"></a>您尚未 wdfverifier


打开驱动程序的 "设置" 列表，然后右键单击 " **TrackPower** " 设置。 选择适用于你的方案的选项。

**提示**  避免在性能关键代码路径中捕获堆栈跟踪。

 

![在您尚未 wdfverifier 中设置跟踪 power 引用](images/wdfverifier--track-power-references-on.png)

## <a name="editing-the-registry"></a>编辑注册表


还可以通过编辑驱动程序的服务密钥来打开验证程序支持和电源引用跟踪。

对于 KMDF 驱动程序：

**HKLM \\ SYSTEM \\ ControlSet001 \\ Services \\ &lt; 驱动程序服务名称 &gt; \\ 参数 \\ Wdf**

对于 UMDF 驱动程序：

**HKLM\ \\ SOFTWARE \\ MICROSOFT \\ Windows NT \\ CurrentVersion \\ WUDF \\ Services \\ &lt; 驱动程序服务名称 &gt; \\ 参数 \\ Wdf**

```cpp
(REG_DWORD) VerifierOn = 0x1
(REG_DWORD) TrackPower = 0x0 (disabled)
                       = 0x1 (capture tick count, file name, line number)
                       = 0x2 (capture tick count, file name, line number, and stack traces)
```

## <a name="driver-code"></a>驱动程序代码


驱动程序调用 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 和 [**WdfDeviceResumeIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle) 来管理设备的工作电源状态，如下所示：

```cpp
//
// Take power reference
//
status = WdfDeviceStopIdle(device, FALSE);
if (NT_SUCCESS(status)) {
    //
    // Release power reference
    //
    WdfDeviceResumeIdle(device);
}
```

## <a name="debugging-with-wdfkd"></a>用 WdfKd 进行调试


若要显示设备上的电源引用以及显示引用历史记录的标记跟踪器，请使用带有详细标志的 [**！ wdfkd。 wdfdevice**](../debugger/-wdfkd-wdfdevice.md) ：

```cpp
kd> !wdfkd.wdfdevice 0x6d939790 ff
Power references: 0 !wdftagtracker 0x9ea030a8
```

调用 [**！ wdfkd**](../debugger/-wdfkd-wdftagtracker.md) 会显示设备的电源参考历史记录：

```cpp
kd> !wdftagtracker 0x9ea030a8
Reference and Release History:
# (showing most recent first; refcount is approximate in multi-threaded scenarios)

## 3 entries, history depth is 25

(--) 0 ref: Tag '....' at Time 0x1331e ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag '....' at Time 0x1331e ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

## <a name="specifying-a-tag"></a>指定标记


还可以指定标记名称，以便识别特定的 power 引用。 为此，请使用 [**WdfDeviceStopIdleWithTag**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidlewithtag) 和 [**WdfDeviceResumeIdleWithTag**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidlewithtag)：

```cpp
status = WdfDeviceStopIdleWithTag(device, FALSE, (PVOID)'oyeH');
if (NT_SUCCESS(status)) {
    WdfDeviceResumeIdleWithTag(device, (PVOID)'oyeH');
}
```

对应 [**！ wdftagtracker**](../debugger/-wdfkd-wdftagtracker.md) 示例输出：

```cpp
(--) 0 ref: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

 

