---
title: 在 WDF 中调试电源参考漏孔
description: 当 Windows 驱动程序框架（WDF）驱动程序调用 WdfDeviceStopIdle 时，框架会递增设备的电源引用计数。
ms.assetid: 25F4EEBB-4733-498C-8704-8E015F81FE06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e2d1cda1ba2cdd6f4e21283b7063cf16f8d5bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844673"
---
# <a name="debugging-power-reference-leaks-in-wdf"></a>在 WDF 中调试电源参考漏孔


当 Windows 驱动程序框架（WDF）驱动程序调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)时，框架会递增设备的电源引用计数。 对**WdfDeviceStopIdle**的每次成功调用都必须通过调用[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)进行匹配，以减小电源引用计数。

从内核模式驱动程序框架（KMDF）1.15 和用户模式驱动程序框架（UMDF）2.15 开始，你可以通过使用[ **！ wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)和[**wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)调试器扩展来监视 power reference 的使用情况。 由于性能原因，此功能默认处于禁用状态，因此，你需要使用您尚未 wdfverifier 应用程序或手动编辑驱动程序的服务密钥来启用此功能。

## <a name="wdfverifier"></a>您尚未 wdfverifier


打开驱动程序的 "设置" 列表，然后右键单击 " **TrackPower** " 设置。 选择适用于你的方案的选项。

**提示**  避免在性能关键代码路径中捕获堆栈跟踪。

 

![在您尚未 wdfverifier 中设置跟踪 power 引用](images/wdfverifier--track-power-references-on.png)

## <a name="editing-the-registry"></a>编辑注册表


还可以通过编辑驱动程序的服务密钥来打开验证程序支持和电源引用跟踪。

对于 KMDF 驱动程序：

**HKLM\\SYSTEM\\ControlSet001\\服务\\&lt;驱动程序服务名称&gt;\\参数\\Wdf**

对于 UMDF 驱动程序：

**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;驱动程序服务名称&gt;\\参数\\Wdf**

```cpp
(REG_DWORD) VerifierOn = 0x1
(REG_DWORD) TrackPower = 0x0 (disabled)
                       = 0x1 (capture tick count, file name, line number)
                       = 0x2 (capture tick count, file name, line number, and stack traces)
```

## <a name="driver-code"></a>驱动程序代码


驱动程序调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)和[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)来管理设备的工作电源状态，如下所示：

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


若要显示设备上的电源引用以及显示引用历史记录的标记跟踪器，请使用带有详细标志的[ **！ wdfkd。 wdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice) ：

```cpp
kd> !wdfkd.wdfdevice 0x6d939790 ff
Power references: 0 !wdftagtracker 0x9ea030a8
```

调用[ **！ wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)会显示设备的电源参考历史记录：

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


还可以指定标记名称，以便识别特定的 power 引用。 为此，请使用[**WdfDeviceStopIdleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevicestopidlewithtag)和[**WdfDeviceResumeIdleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdeviceresumeidlewithtag)：

```cpp
status = WdfDeviceStopIdleWithTag(device, FALSE, (PVOID)'oyeH');
if (NT_SUCCESS(status)) {
    WdfDeviceResumeIdleWithTag(device, (PVOID)'oyeH');
}
```

对应[ **！ wdftagtracker**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)示例输出：

```cpp
(--) 0 ref: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

 

 





