---
title: 音频设备类不活动计时器实现
description: 音频设备类不活动计时器实现
ms.assetid: e7e431ec-626d-4fdb-8705-fc5420c43f17
keywords:
- 非活动计时器 WDK 音频
- 计时器 WDK 音频
- power 空闲检测 WDK 音频
- 空闲处理能力状态 WDK 音频
- 空闲超时 WDK 音频
- 超时间隔 WDK 音频
- 节约电源模式 WDK 音频
- 节省电源模式 WDK 音频
- 性能电源模式 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26ba356afcf9e9f9c6f2d5cb5e92985c2a1c150a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331557"
---
# <a name="audio-device-class-inactivity-timer-implementation"></a>音频设备类不活动计时器实现


## <span id="audio_device_class_inactivity_timer_implementation"></span><span id="AUDIO_DEVICE_CLASS_INACTIVITY_TIMER_IMPLEMENTATION"></span>


在 Windows Server 2003 SP1，Windows XP SP2 和更高版本，PortCls 系统驱动程序利用系统的电源空闲检测功能来实现其音频的客户端的非活动计时器。 PortCls 程序两个超时值和所需进行初始化时空闲到计时器电源状态。 PortCls 监视设备的任何访问 （例如 I/O 和属性访问），并有效地将在每次访问计时器计数重置。 如果计时器超时时，系统将请求 power IRP 将设备置于所需的空闲状态。 设备已置于空闲状态后，PortCls power 设备备份出现新的访问活动。

PortCls 包含硬编码默认值为空闲超时和空闲处理能力状态。 硬件供应商可以通过其自身的值写入系统注册表中的特定于驱动程序的键选择替代默认值。 在这种方式，供应商可以选择最适合他们的设备的 power 空闲参数值。

供应商可以重写以下 power 空闲参数的默认值：

-   *ConservationIdleTime*

    此参数指定空闲超时间隔以节约电源模式运行系统时。 这是系统运行电池电源时，通常使用的模式。 此参数的默认值为 0，这将禁用在保留模式下的 power 空闲计时器。 硬件供应商可以通过写入以下特定于驱动程序的注册表项 DWORD 值来覆盖默认值：

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\ConservationIdleTime
    ```

    请注意， *xxxx*表示媒体类 GUID (请参阅[System-Supplied 设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)) 和*yyyy*表示下媒体类的驱动程序的子项的名称GUID。 键的值指定的超时间隔 （秒）。

-   *PerformanceIdleTime*

    系统在性能模式下运行时，此参数指定空闲超时间隔。 这是系统运行交流电源时，通常使用的模式。 此参数的默认值为 0，这将禁用在性能模式下的 power 空闲计时器。 硬件供应商可以通过写入以下特定于驱动程序的注册表项 DWORD 值来覆盖默认值：

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\PerformanceIdleTime
    ```

    同样， *xxxx*表示 GUID 的媒体类和*yyyy*表示驱动程序的子项的名称。 键的值指定的超时间隔 （秒）。

-   *IdlePowerState*

    此参数指定将被放入该设备，如果空闲超时期限过期的电源状态。 默认值为此参数为 0，对应于设备电源状态 D0 （完整电源）。 硬件供应商可以通过写入以下特定于驱动程序的注册表项 DWORD 值来覆盖默认值：

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\IdlePowerState
    ```

    同样， *xxxx*表示 GUID 的媒体类和*yyyy*表示驱动程序的子项的名称。 放在项中的值应为 0、 1、 2 或 3，分别对应于设备的电源状态更改 D0、 D1、 D2 或 D3。

三个电源空闲注册表项存在仅当设备安装 INF 文件将创建它们。 配置 power 空闲计时器之前, PortCls 尝试从注册表检索特定于驱动程序的电源空闲参数。 PortCls 使用代替它不会在注册表中未找到任何 power 空闲的参数的默认值。 正如上文 power 空闲的默认参数值将禁用空闲计时器。

有关指定详细信息*ConservationIdleTime*， *PerformanceIdleTime*，并*IdlePowerState*参数，请参阅的最后三个定义调用中的参数[ **PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721)。

### <a name="span-idexamplespanspan-idexamplespan-example"></a><span id="example"></span><span id="EXAMPLE"></span> 示例

例如，硬件供应商可能想要指定用于将音频设备的以下 power 空闲参数：*ConservationIdleTime* = 0x0000001e （30 秒）， *PerformanceIdleTime* = 0x0000012c （300 秒） 和*IdlePowerState* = 0x00000003 （设备电源状态 D3）。 若要启用这些设置，设备安装文件可以包含[ **INF AddReg 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含以下指令：

```inf
[MyAudioDevice.AddReg]
HKR,PowerSettings,ConservationIdleTime,1,1e,00,00,00
HKR,PowerSettings,PerformanceIdleTime,1,2c,01,00,00
HKR,PowerSettings,IdlePowerState,1,03,00,00,00
```

HKR 表示注册表中的驱动程序的根项：

```inf
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy
```

同样， *xxxx*表示 GUID 的媒体类和*yyyy*表示驱动程序的子项的名称。 **PowerSettings**子项指定相对于根项的路径名称。

 

 




