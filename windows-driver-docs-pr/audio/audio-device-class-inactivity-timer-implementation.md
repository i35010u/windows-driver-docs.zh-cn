---
title: 音频设备类不活动计时器实现
description: 音频设备类不活动计时器实现
keywords:
- 不活动计时器音频
- 计时器音频
- power idle 检测 WDK 音频
- 空闲电源状态 WDK 音频
- 空闲超时音响音频
- 超时间隔 WDK 音频
- 节能模式 WDK 音频
- 节省电源模式 WDK 音频
- 性能电源模式 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 744913b927108a3e119dccd63ef974ec68cb7304
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789431"
---
# <a name="audio-device-class-inactivity-timer-implementation"></a>音频设备类不活动计时器实现


## <span id="audio_device_class_inactivity_timer_implementation"></span><span id="AUDIO_DEVICE_CLASS_INACTIVITY_TIMER_IMPLEMENTATION"></span>


在 Windows Server 2003 SP1、Windows XP SP2 及更高版本中，PortCls 系统驱动程序利用系统的电源空闲检测功能来为其音频客户端实现不活动的计时器。 PortCls 程序在初始化时将两个超时值和所需的空闲电源状态写入计时器。 PortCls 监视 (例如，i/o 和属性访问) 设备的任何访问权限，并有效地重置每个访问的计时器计数。 如果计时器超时，则系统请求 power IRP 将设备置于所需的空闲状态。 设备处于空闲状态后，PortCls 会在新的访问活动发生时对设备进行备份。

PortCls 包含空闲超时和空闲电源状态的硬编码默认值。 硬件供应商可以选择通过将其自己的值写入系统注册表中特定于驱动程序的密钥来替代默认值。 通过这种方式，供应商可以选择最适合其设备的电源空闲参数值。

供应商可以重写以下电源空闲参数的默认值：

-   *ConservationIdleTime*

    此参数指定在系统以节能模式运行时的空闲超时间隔。 这是在系统使用电池电源运行时通常使用的模式。 此参数的默认值为0，这将在节能模式下禁用电源空闲计时器。 硬件供应商可以通过将 DWORD 值写入下列特定于驱动程序的注册表项来替代默认值：

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\ConservationIdleTime
    ```

    请注意， *xxxx* 表示 MEDIA 类 GUID (参阅 [系统提供的设备安装程序类](/windows-hardware/drivers/install/system-defined-device-setup-classes-reserved-for-system-use)) ， *yyyy* 表示 media 类 GUID 下驱动程序子项的名称。 键的值指定超时间隔（秒）。

-   *PerformanceIdleTime*

    此参数指定系统在性能模式下运行时的空闲超时间隔。 这是在系统以交流电源运行时通常使用的模式。 此参数的默认值为0，这将在性能模式下禁用电源空闲计时器。 硬件供应商可以通过将 DWORD 值写入下列特定于驱动程序的注册表项来替代默认值：

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\PerformanceIdleTime
    ```

    同样， *xxxx* 表示 MEDIA 类 GUID， *yyyy* 表示驱动程序子项的名称。 键的值指定超时间隔（秒）。

-   *IdlePowerState*

    此参数指定空闲超时期限到期后设备将置于的电源状态。 此参数的默认值为0，对应于设备电源状态 D0 (完全电源) 。 硬件供应商可以通过将 DWORD 值写入下列特定于驱动程序的注册表项来替代默认值：

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\IdlePowerState
    ```

    同样， *xxxx* 表示 MEDIA 类 GUID， *yyyy* 表示驱动程序子项的名称。 放置在键中的值应为0、1、2或3，分别对应于设备电源状态 D0、D1、D2 或 D3。

只有设备安装 INF 文件创建了这三个空闲的注册表项。 在配置电源空闲计时器之前，PortCls 会尝试从注册表中检索驱动程序特定的 power idle 参数。 PortCls 使用默认值来代替在注册表中找不到的任何电源空闲参数。 如前所述，默认的 power idle 参数值禁用空闲计时器。

有关指定 *ConservationIdleTime*、 *PerformanceIdleTime* 和 *IdlePowerState* 参数的详细信息，请参阅 [**PoRegisterDeviceForIdleDetection**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)中最后三个调用参数的定义。

### <a name="span-idexamplespanspan-idexamplespan-example"></a><span id="example"></span><span id="EXAMPLE"></span> 示例

例如，硬件供应商可能想要为音频设备指定以下电源空闲参数： *ConservationIdleTime* = 0x0000001e (30 秒) ， *PerformanceIdleTime* = 0x0000012c (300 秒) ， *IdlePowerState* = 0x00000003 (设备电源状态 D3) 。 若要启用这些设置，设备安装文件可以包含包含以下指令的 [**INF AddReg 部分**](../install/inf-addreg-directive.md) ：

```inf
[MyAudioDevice.AddReg]
HKR,PowerSettings,ConservationIdleTime,1,1e,00,00,00
HKR,PowerSettings,PerformanceIdleTime,1,2c,01,00,00
HKR,PowerSettings,IdlePowerState,1,03,00,00,00
```

HKR 表示注册表中驱动程序的根密钥：

```inf
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy
```

同样， *xxxx* 表示 MEDIA 类 GUID， *yyyy* 表示驱动程序子项的名称。 相对于根密钥的路径名称指定 **PowerSettings** 子项。

 

