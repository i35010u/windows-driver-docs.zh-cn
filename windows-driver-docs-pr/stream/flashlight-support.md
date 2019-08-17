---
title: 闪光灯支持
description: 本主题提供有关设备如何支持 WinRT 灯具 API 的指南
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0d4f857edc85bd4549a9180b3cd6953af4f1c671
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565925"
---
# <a name="flashlight-support"></a>闪光灯支持

## <a name="overview"></a>概述

从 Windows 阈值开始, 我们将公开一个新的 WinRT*灯泡*API, 该 API 允许一个程序的*照相机闪烁*, 无需创建[MediaCapture](http://msdn.microsoft.com/en-us/library/windows/apps/windows.media.capture.mediacapture.aspx)实例。 通过这种方式, 开发人员可以通过绘制最小数量的资源 (包括电源) 来编写一个*闪光灯*应用程序 (仅适用于照明目的), 以便能够针对电池寿命和性能优化计算设备。

为实现此目的, IHV/OEM 应实现支持以下功能的 WDM 驱动程序:

- 允许系统枚举所有闪存设备。
- 基于每个设备开启/关闭闪光灯。
- 如果适用, 请在每个设备基础上调整光源强度 (类似于 PowerPercent)。
- 如果适用, 则为每个设备指定亮色。

就功能而言, 上面的列表与 MediaCapture 的列表 (例如[FlashControl](http://msdn.microsoft.com/en-us/library/windows/apps/windows.media.devices.flashcontrol.aspx)和[TorchControl](http://msdn.microsoft.com/en-us/library/windows/apps/windows.media.devices.torchcontrol.aspx)) 明显重叠。
此外, 同一闪存硬件同时用于*灯具*和*在捕获期间闪烁*。 因此, 我们建议使用单个 WDM 驱动程序来支持这两种类型的操作, 以独占方式控制闪存。 下图说明了这一概念:

![专用 flash 控件概念关系图](images/exclusive-flash-control.png)

在上面的示例中, 只有一个闪存硬件实例 (显示为), 它由单个*KMDF 闪存驱动程序*管理。 闪存驱动程序公开两个设备接口, 每个接口都针对特定类型的客户端 (或 WinRT API)。 例如, 假设上图:

- WinRT*媒体* *捕获*API 和 AVStream 微型驱动程序始终通过 GUID\_DEVINTERFACE\_相机\_flash 接口与闪存驱动程序通信, 而
- WinRT*灯泡*API 始终通过 GUID\_DEVINTERFACE\_灯接口与闪存驱动程序通信。

由于 GUID\_DEVINTERFACE\_照相机\_闪存接口由特定于供应商的 AVStream 微型驱动程序使用, 因此 IHV/OEM 可随意定义其功能, 而不会对 Windows 施加任何限制。

不过, Microsoft 会将接口 GUID\_DEVINTERFACE\_灯标准化, 因为它应由 WinRT*灯光 API*使用。
有关 GUID\_DEVINTERFACE\_灯的详细信息, 请参阅[设备接口类 GUID](#device-interface-class-guid)

### <a name="concurrency-use-cases"></a>并发用例

#### <a name="sharing-flash-between-camera-and-flashlight-applications"></a>共享照相机和闪光灯应用程序之间的闪烁

照相机闪光灯通常被视为捕获设备的外设。 当捕获正在运行时, 不应与非照相机方案共享。 为了进一步增加, 机箱上的闪存设备数量极有限制, 因此在实际情况下, 不会将备用闪存专用于闪烁。

从软件的角度来看, 上述一项挑战就是相机应用程序和闪存应用程序可以同时共存和访问闪存的挑战。 例如, 在理论上, 用户可以在照相机取景器运行时通过闪烁应用程序切换 LED 状态。

由于照相机需要通过闪存的精确控制来支持焦点和捕获, 因此驱动程序在确保图像质量的同时, 可能很难解决感兴趣的闪烁请求。 为了解决此问题, 我们将在系统级别将下列策略划分为协定:

- **如果首先启动捕获会话**, 闪烁应用程序将无法操作 flash, 直到捕获停止。
  - 闪光灯应用程序仍可获取闪存驱动程序的句柄, 但任何修改闪存状态的操作都会产生即时错误。
  - 捕获停止后, AVStream 微型驱动程序会释放闪存, 需要闪存驱动程序才能发布 PnP 通知 (请参阅可用于[异步通知](#asynchronous-notifications)的\_GUID\_\_灯泡资源)指示基础硬件现在变为可用。 收到此类通知后, 将允许闪烁应用程序相应地进行刷新。
- **如果闪光应用程序首先启动**, 捕获会话可随意劫持闪存硬件, 而无需明确同意。
  - "劫持" 是指 IHV/OEM 可以实现任意协议 (可能通过 GUID\_DEVINTERFACE\_相机\_FLASH 接口), 以便允许 AVStream 微型驱动程序获取闪存, 就好像硬件不是全部使用。
  - 当发生劫持时, 需要使用闪存驱动程序发布另一个 PnP 通知 (请参阅\_GUID\_灯泡\_资源在[异步通知](#asynchronous-notifications)中丢失), 指示已 involuntarily 重新分配闪存这样, 闪光灯应用程序可以相应地执行操作 (例如, 通过更新 UI)

#### <a name="sharing-flash-between-multiple-flashlight-applications"></a>在多个闪光应用程序之间共享 Flash

如果不涉及相机并且两个闪光灯应用程序连续运行, 则驱动程序应继续为第一个客户端提供服务, 该\_客户\_端已经获取了 GUID DEVINTERFACE 灯接口并拒绝所有其他客户端第一个版本最终会释放接口。

换句话说, GUID\_DEVINTERFACE\_灯接口每次只允许使用一台闪光灯客户端, 而第一个获取接口的客户端会阻止其他设备运行 (相机/AVStream 排除)。

## <a name="device-interface-class-guid"></a>设备接口类 GUID

支持独立于 MediaCapture 的的 IHV/OEM 闪存驱动程序必须向 *[设备接口类](http://msdn.microsoft.com/en-us/library/windows/hardware/ff541339\(v=vs.85\).aspx)guid*、 **guid\_DEVINTERFACE\_灯具**注册自身。

| 特性  | 设置                                |
| ---------- | -------------------------------------- |
| 标识符 | GUID\_DEVINTERFACE\_灯               |
| 类 GUID | {6C11E9E3-8232-4F0A-AD19-AAEC26CA5E98} |

GUID\_DEVINTERFACE\_照相机闪存的设备接口类guid可以是由ihv/oem定义的自定义。\_
但是, guid\_DEVINTERFACE\_灯具的设备接口类 guid 由 Windows 定义。

### <a name="remarks"></a>备注

按照约定, 提供设备接口 GUID\_DEVINTERFACE\_灯具的驱动程序需要支持以下功能 (有关详细信息, 请参阅后面的部分):

- **IOCTL\_灯光获取\_功能{\_白色 |\_COLOR}** –获取底层硬件支持的所有模式 (如仅支持白颜色与颜色)
- **IOCTL\_灯\_{GET |设置}\_模式**–获取或设置当前模式
- **IOCTL\_灯\_{GET |设置}\_强度\_{白色 |COLOR}** –获取或设置光源强度
- **IOCTL\_灯\_{GET |设置}\_发出\_光源**–获取或设置闪光灯状态 (即打开/关闭)

如果设备有多个不同类型的闪存硬件 (例如,*白色 LED*和*Xenon 闪存*), 并且这些硬件由不同的闪存驱动程序控制, 则每个驱动程序应公开同一 GUID\_DEVINTERFACE\_具有唯一[实例 ID](http://msdn.microsoft.com/en-us/library/windows/hardware/ff547656\(v=vs.85\).aspx)的灯泡接口。

## <a name="device-interface-property"></a>设备接口属性

由于一台计算设备可以在不同的面板上有零个或多个闪存设备, 因此, WinRT*灯光 API*需要一个机制来枚举所有闪存硬件, 使应用程序可以对特定实例进行编程。

为了支持设备枚举, 与相机驱动程序类似, 需要使用闪存驱动程序将 ACPI \_PLD v2 结构与每个 GUID\_DEVINTERFACE\_灯泡接口相关联, 作为接口属性数据。

## <a name="ioctl_lamp_get_capabilities_white"></a>IOCTL_LAMP_GET_CAPABILITIES_WHITE

IOCTL\_灯光\_获取\_功能:当设备配置为发出白屏时,白色i/o请求会查询闪存的功能。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_BASE FILE_DEVICE_UNKNOWN
#define IOCTL_LAMP_GET_CAPABILITIES_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0000, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向\_类型\_为的缓冲区。 有关详细信息, 请参阅**备注**。

IO\_堆栈\_位置。OutputBufferLength 是 DeviceIoControl 中\>传递的缓冲区的长度 (以字节为单位)。

### <a name="output-parameters"></a>输出参数

Irp-\>AssociatedIrp. SystemBuffer 是使用闪存硬件支持的所有功能。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。 它会将\>IoStatus 设置为保留缓冲区所需的字节数。

### <a name="remarks"></a>备注

根据要求, 驱动程序支持 GUID\_DEVINTERFACE\_灯接口, 以支持发出白屏。 此 IOCTL 的有效负载定义如下:

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_WHITE.
typedef struct LAMP_CAPABILITIES_WHITE
{
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_WHITE;
```

IsLightIntensityAdjustable 字段指示是否可以对亮度级别进行编程。 如果此字段的计算结果为 false, 则表示基础设备仅支持 on/off 开关, 并且无法调整光线强度。

## <a name="ioctl_lamp_get_capabilities_color"></a>IOCTL_LAMP_GET_CAPABILITIES_COLOR

IOCTL\_灯光\_获取\_功能当设备配置为发出颜色亮度时,i/o请求会查询闪存的功能。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_CAPABILITIES_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0001, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向类型为灯光\_功能\_的缓冲区。 有关详细信息, 请参阅**备注**。

IO\_堆栈\_位置。OutputBufferLength 是 DeviceIoControl 中\>传递的缓冲区的长度 (以字节为单位)。

### <a name="output-parameters"></a>输出参数

Irp-\>AssociatedIrp. SystemBuffer 是使用闪存硬件支持的所有功能。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。 它会将\>IoStatus 设置为保留缓冲区所需的字节数。

### <a name="remarks"></a>备注

此 IOCTL 的有效负载定义如下:

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_COLOR.
typedef struct LAMP_CAPABILITIES_COLOR
{
    BOOLEAN IsSupported;
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_COLOR;
```

第一个字段 "IsSupported" 指示闪光灯是否可以发出颜色浅。 如果硬件不支持颜色指示灯, 则驱动程序应将此字段设置为 false。

第二个字段 "IsLightIntensityAdjustable" 指示是否可以对亮度级别进行编程。 如果 flash 不支持颜色浅 (即 IsSupported 的计算结果为 false), 则客户端应丢弃 IsLightIntensityAdjustable 的值。

## <a name="ioctl_lamp_get_mode"></a>IOCTL_LAMP_GET_MODE

IOCTL\_灯光\_获取模式i/o请求查询当前配置闪存时所用的模式。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0002, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向灯光\_模式类型的缓冲区, 定义如下:

```cpp
typedef enum LAMP_MODE
{
    LAMP_MODE_WHITE = 0,
    LAMP_MODE_COLOR
} LAMP_MODE;
```

IO\_堆栈\_位置。OutputBufferLength 是 DeviceIoControl 中\>传递的缓冲区的长度 (以字节为单位)。

### <a name="output-parameters"></a>输出参数

Irp-\>AssociatedIrp. SystemBuffer 用灯光\_模式值填充。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。 它会将\>IoStatus 设置为保存 DWORD 值所需的字节数。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

## <a name="ioctl_lamp_set_mode"></a>IOCTL_LAMP_SET_MODE

IOCTL\_灯光\_集模式i/o请求设置flash操作的模式。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0003, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向灯光\_模式类型的缓冲区。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

## <a name="ioctl_lamp_get_intensity_white"></a>IOCTL_LAMP_GET_INTENSITY_WHITE

IOCTL\_灯\_获取\_强度当flash配置为发出白色光时,i/o请求会查询光线强度。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0004, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向灯泡\_强度\_的白色结构。 有关详细信息, 请参阅**备注**。

IO\_堆栈\_位置。OutputBufferLength 是 DeviceIoControl 中\>传递的缓冲区的长度 (以字节为单位)。

### <a name="output-parameters"></a>输出参数

Irp-\>AssociatedIrp. SystemBuffer 是用光强度信息填充的。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

### <a name="remarks"></a>备注

此 IOCTL 的负载类型定义如下:

```cpp
// The I/O parameter type of IOCTL_LAMP_{GET|SET}_INTENSITY_WHITE.
typedef struct LAMP_INTENSITY_WHITE
{
    BYTE Value;
} LAMP_INTENSITY_WHITE;
```

值字段是介于0到100之间 (含0和) 的白色光源亮度。 

## <a name="ioctl_lamp_set_intensity_white"></a>IOCTL_LAMP_SET_INTENSITY_WHITE

IOCTL\_灯\_设置\_强度白色i/o请求将闪存设置为指定的光线强度。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0005, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向灯泡\_强度\_(有关详细信息, 请参阅[IOCTL_LAMP_GET_INTENSITY_WHITE](#ioctl_lamp_get_intensity_white) )。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

## <a name="ioctl_lamp_get_intensity_color"></a>IOCTL_LAMP_GET_INTENSITY_COLOR
IOCTL\_灯\_获取亮度\_颜色\_

IOCTL\_灯\_获取\_强度色i/o请求会在将闪存配置为发出颜色亮度时查询光线强度。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0006, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向灯光\_强度\_色结构。 有关详细信息, 请参阅**备注**。

IO\_堆栈\_位置。OutputBufferLength 是 DeviceIoControl 中\>传递的缓冲区的长度 (以字节为单位)。

### <a name="output-parameters"></a>输出参数

Irp-\>AssociatedIrp. SystemBuffer 是用光强度信息填充的。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

### <a name="remarks"></a>备注

此 IOCTL 的负载类型定义如下:

```cpp
// The I/O parameter type of IOCTL_LAMP_{GET|SET}_INTENSITY_COLOR.
typedef struct LAMP_INTENSITY_COLOR
{
    BYTE Red; // Red light intensity in percentage (0-100)
    BYTE Green; // Green light intensity in percentage (0-100)
    BYTE Blue; // Blue light intensity in percentage (0-100)
} LAMP_INTENSITY_COLOR;
```

## <a name="ioctl_lamp_set_intensity_color"></a>IOCTL_LAMP_SET_INTENSITY_COLOR

IOCTL\_灯\_设置\_强度颜色i/o请求将闪光灯设置为指定的光线强度。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0007, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向灯光\_强度\_色结构 (有关详细信息, 请参阅[IOCTL_LAMP_GET_INTENSITY_COLOR](#ioctl_lamp_get_intensity_color) )。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

## <a name="ioctl_lamp_get_emitting_light"></a>IOCTL_LAMP_GET_EMITTING_LIGHT

如果已\_打开 (\_闪光灯\_) 指示灯, 则 IOCTL 灯\_将发出轻型 i/o 请求查询。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0008, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向布尔类型的缓冲区。

IO\_堆栈\_位置。OutputBufferLength 是 DeviceIoControl 中\>传递的缓冲区的长度 (以字节为单位)。

### <a name="output-parameters"></a>输出参数

Irp-\>AssociatedIrp. SystemBuffer 是通过 "flash" 状态填充的, 这意味着闪存处于开启状态 (即发出灯光);否则为 FALSE。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。 它会将\>IoStatus 设置为保存 DWORD 值所需的字节数。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

## <a name="ioctl_lamp_set_emitting_light"></a>IOCTL_LAMP_SET_EMITTING_LIGHT

IOCTL\_灯\_设置\_发出的i/o请求开启/关闭(闪光灯)光。\_

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_EMITTING_LIGHT 
    CTL_CODE(IOCTL_LAMP_BASE, 0x0009, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp-\>AssociatedIrp. SystemBuffer 指向布尔类型的缓冲区, 其值为 TRUE, 表示 ON;否则为 FALSE。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/O 状态块

驱动程序将 Irp-\>IoStatus 设置\_为 "成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据, 则驱动程序应通过\_Irp-\>IoStatus 返回错误 (正在使用的\_\_状态资源)。

## <a name="asynchronous-notifications"></a>异步通知

如[*并发用例*](#concurrency-use-cases)中所述, 需要使用闪存驱动程序将 PnP 通知发送到报表资源可用性。 这可以通过使用以下 Guid 调用 IoReportTargetDeviceChange (或 IoReportTargetDeviceChangeAsynchronous) 来实现, 具体取决于方案:

- 闪存资源已被逐出, 因为捕获会话 (或另一个闪烁应用程序) 启动:
  | 特性  | 设置                                |
  | ---------- | -------------------------------------- |
  | 标识符 | GUID\_灯泡\_资源丢失\_            |
  | 类 GUID | {F770E98C-4403-48C9-B1D2-4EEC3302E41F} |
- Flash 资源现在变为可用:
  | 特性  | 设置                                |
  | ---------- | -------------------------------------- |
  | 标识符 | GUID\_灯泡\_资源可用\_       |
  | 类 GUID | {185FE7CE-2616-481B-9094-20BB893ACD81} |
