---
title: 闪光灯支持
description: 本主题提供有关设备如何支持 WinRT 灯具 API 的指南
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6ae80820792c6dbd8f4cfb6ccc3f53ae964876e0
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681681"
---
# <a name="flashlight-support"></a>闪光灯支持

从 Windows 阈值开始，我们将公开一个新的 WinRT*灯泡*API，该 API 允许一个程序的*照相机闪烁*，无需创建[MediaCapture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture)实例。 通过这种方式，开发人员可以通过绘制最小数量的资源（包括电源）来编写一个*闪光灯*应用程序（仅适用于照明目的），以便能够针对电池寿命和性能优化计算设备。

为实现此目的，IHV/OEM 应实现支持以下功能的 WDM 驱动程序：

- 允许系统枚举所有闪存设备。

- 基于每个设备开启/关闭闪光灯。

- 如果适用，请在每个设备基础上调整光源强度（类似于 PowerPercent）。

- 如果适用，则为每个设备指定亮色。

就功能而言，上面的列表与 MediaCapture 的列表（例如， [FlashControl](https://docs.microsoft.com/uwp/api/Windows.Media.Devices.FlashControl)和[TorchControl](https://docs.microsoft.com/uwp/api/Windows.Media.Devices.TorchControl)）明显重叠。 此外，同一闪存硬件同时用于*灯具*和*在捕获期间闪烁*。 因此，我们建议使用单个 WDM 驱动程序来支持这两种类型的操作，以独占方式控制闪存。 下图说明了这一概念：

![专用 flash 控件概念关系图](images/exclusive-flash-control.png)

在上面的示例中，只有一个闪存硬件实例（显示为），它由单个*KMDF 闪存驱动程序*管理。 闪存驱动程序公开两个设备接口，每个接口都针对特定类型的客户端（或 WinRT API）。 例如，假设上图：

- WinRT*媒体**捕获*API 和 AVSTREAM 微型驱动程序始终通过 GUID \_ DEVINTERFACE 相机 flash 接口与闪存驱动程序通信 \_ \_ ，而

- WinRT*灯泡*API 始终通过 GUID \_ DEVINTERFACE 灯接口与闪存驱动程序通信 \_ 。

由于 GUID \_ DEVINTERFACE \_ 照相机 \_ 闪存接口由特定于供应商的 AVStream 微型驱动程序使用，因此 IHV/OEM 可随意定义其功能，而不会对 Windows 施加任何限制。

不过，Microsoft 会将接口 GUID \_ DEVINTERFACE 灯标准化 \_ ，因为它应由 WINRT*灯光 API*使用。 有关 GUID DEVINTERFACE 灯的详细信息 \_ \_ ，请参阅[设备接口类 GUID](#device-interface-class-guid)

## <a name="concurrency-use-cases"></a>并发用例

### <a name="sharing-flash-between-camera-and-flashlight-applications"></a>共享照相机和闪光灯应用程序之间的闪烁

照相机闪光灯通常被视为捕获设备的*从属*设备。 当捕获正在运行时，不应与非照相机方案共享。 为了进一步增加，底盘上的闪存设备数非常有限，因此，在实际情况下，不会有专用闪存专用于闪烁用途。

从软件的角度来看，上述一项挑战就是相机应用程序和闪存应用程序可以同时共存和访问闪存的挑战。 例如，在理论上，用户可以在照相机取景器运行时通过闪烁应用程序切换 LED 状态。

由于照相机需要通过闪存的精确控制来支持焦点和捕获，因此驱动程序在确保图像质量的同时，可能很难解决感兴趣的闪烁请求。 若要解决此问题，请在系统级别将以下策略强制为协定：

- **如果首先启动捕获会话**，闪烁应用程序将无法操作 flash，直到捕获停止。

  - 闪光灯应用程序仍可获取闪存驱动程序的句柄，但任何修改闪存状态的操作都会产生即时错误。

  - 当捕获停止以便 AVStream 微型驱动程序释放闪存时，需要使用闪存驱动程序发布 PnP 通知（请参阅 \_ \_ \_ [异步通知](#asynchronous-notifications)中可用的 GUID 灯泡资源），指出底层硬件现在变为可用。 收到此类通知后，将允许闪烁应用程序相应地进行刷新。

- **如果闪光应用程序首先启动**，捕获会话可随意劫持闪存硬件，而无需明确同意。

  - "劫持" 是指 IHV/OEM 可以实现任意协议（可能通过 GUID \_ DEVINTERFACE \_ 相机 \_ FLASH 接口），以便允许 AVStream 微型驱动程序获取闪存，就好像硬件根本不使用一样。

  - 当发生劫持时，需要使用闪存驱动程序发布另一个 PnP 通知（请参阅 GUID \_ 灯泡 \_ 资源 \_ 在[异步通知](#asynchronous-notifications)中丢失），以指示闪存已 involuntarily 重新分配，以便闪光灯应用程序可以相应地进行操作（例如，通过更新 UI）

### <a name="sharing-flash-between-multiple-flashlight-applications"></a>在多个闪光应用程序之间共享 Flash

如果不涉及相机并且两个闪光灯应用程序连续运行，则驱动程序应继续为第一个客户端提供服务，该客户端已经获取了 GUID \_ DEVINTERFACE \_ 灯接口并拒绝所有其他客户端，直到第一个客户端最终释放该接口。

换句话说，GUID \_ DEVINTERFACE \_ 灯接口每次只允许使用一台闪光灯客户端，而第一个获取接口的客户端会阻止其他设备运行（相机/AVStream 排除）。

## <a name="device-interface-class-guid"></a>设备接口类 GUID

支持独立于 MediaCapture 的的 IHV/OEM 闪存驱动程序必须向[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)Guid、 **guid \_ DEVINTERFACE \_ 灯具**注册自身。

| Attribute  | 设置                                |
| ---------- | -------------------------------------- |
| 标识符 | GUID \_ DEVINTERFACE \_ 灯               |
| 类 GUID | {6C11E9E3-8232-4F0A-AD19-AAEC26CA5E98} |

GUID DEVINTERFACE 照相机闪存的设备接口类 GUID \_ \_ \_ 可以是由 ihv/oem 定义的自定义。 但是，GUID DEVINTERFACE 灯具的设备接口类 \_ guid \_ 由 Windows 定义。

按照约定，提供设备接口 GUID DEVINTERFACE 灯具的驱动 \_ 程序 \_ 需要支持以下功能（有关详细信息，请参阅后面的部分）：

- **IOCTL \_灯泡 \_ 获取 \_ 功能 \_ {白色 |COLOR}** –获取底层硬件支持的所有模式（例如，仅限白与彩色）

- **IOCTL \_灯 \_ {GET |设置} \_ 模式**–获取或设置当前模式

- **IOCTL \_灯 \_ {GET |设置} \_ 强度 \_ {白色 |COLOR}** –获取或设置光源强度

- **IOCTL \_灯 \_ {GET |设置} \_ 发出 \_ 光源**–获取或设置闪光灯状态（例如，开/关）

如果设备有多个不同类型的闪存硬件（例如，*白色 LED*和*Xenon 闪存*），并且这些硬件由不同的闪存驱动程序控制，则每个驱动程序应 \_ 使用唯一的实例 ID 公开同一 GUID DEVINTERFACE \_ 灯具接口。

## <a name="device-interface-property"></a>设备接口属性

由于一台计算设备可以在不同的面板上有零个或多个闪存设备，因此，WinRT*灯光 API*需要一个机制来枚举所有闪存硬件，使应用程序可以对特定实例进行编程。

为了支持设备枚举，与相机驱动程序类似，需要使用闪存驱动程序将 ACPI \_ PLD v2 结构与每个 GUID \_ DEVINTERFACE 灯泡接口相关联， \_ 作为接口属性数据。

## <a name="ioctl_lamp_get_capabilities_white"></a>IOCTL_LAMP_GET_CAPABILITIES_WHITE

IOCTL \_ 灯光 \_ 获取功能 \_ ： \_ 当设备配置为发出白屏时，白色 i/o 请求会查询闪存的功能。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_BASE FILE_DEVICE_UNKNOWN
#define IOCTL_LAMP_GET_CAPABILITIES_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0000, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向类型为 "灯光" 的 \_ 缓冲区 \_ 。 有关详细信息，请参阅**备注**。

IO \_ 堆栈 \_ 位置。DeviceIoControl. OutputBufferLength 是 Irp \>AssociatedIrp.SystemBuffer 字段中传递的缓冲区的长度（以字节为单位）。

### <a name="output-parameters"></a>输出参数

Irp- \>AssociatedIrp.SystemBuffer 填充了闪存硬件支持的所有功能。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。 它会将 IoStatus 设置 \> 为保留缓冲区所需的字节数。

### <a name="remarks"></a>注解

根据要求，驱动程序支持 GUID \_ DEVINTERFACE \_ 灯接口，以支持发出白屏。 此 IOCTL 的有效负载定义如下：

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_WHITE.
typedef struct LAMP_CAPABILITIES_WHITE
{
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_WHITE;
```

IsLightIntensityAdjustable 字段指示是否可以对亮度级别进行编程。 如果此字段的计算结果为 false，则表示基础设备仅支持 on/off 开关，并且无法调整光线强度。

## <a name="ioctl_lamp_get_capabilities_color"></a>IOCTL_LAMP_GET_CAPABILITIES_COLOR

IOCTL \_ 灯光 \_ 获取 \_ 功能 \_ 当设备配置为发出颜色亮度时，i/o 请求会查询闪存的功能。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_CAPABILITIES_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0001, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向类型为灯光功能的缓冲区 \_ \_ 。 有关详细信息，请参阅**备注**。

IO \_ 堆栈 \_ 位置。DeviceIoControl. OutputBufferLength 是 Irp \>AssociatedIrp.SystemBuffer 字段中传递的缓冲区的长度（以字节为单位）。

### <a name="output-parameters"></a>输出参数

Irp- \>AssociatedIrp.SystemBuffer 填充了闪存硬件支持的所有功能。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。 它会将 IoStatus 设置 \> 为保留缓冲区所需的字节数。

### <a name="remarks"></a>注解

此 IOCTL 的有效负载定义如下：

```cpp
// The output parameter type of IOCTL_LAMP_GET_CAPABILITIES_COLOR.
typedef struct LAMP_CAPABILITIES_COLOR
{
    BOOLEAN IsSupported;
    BOOLEAN IsLightIntensityAdjustable;
} LAMP_CAPABILITIES_COLOR;
```

第一个字段 "IsSupported" 指示闪光灯是否可以发出颜色浅。 如果硬件不支持颜色指示灯，则驱动程序应将此字段设置为 false。

第二个字段 "IsLightIntensityAdjustable" 指示是否可以对亮度级别进行编程。 如果 flash 不支持颜色浅（例如，IsSupported 计算为 false），则客户端应丢弃 IsLightIntensityAdjustable 的值。

## <a name="ioctl_lamp_get_mode"></a>IOCTL_LAMP_GET_MODE

IOCTL \_ 灯光 \_ 获取 \_ 模式 i/o 请求查询当前配置闪存时所用的模式。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0002, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向类型为 \_ "灯模式" 的缓冲区，其定义如下：

```cpp
typedef enum LAMP_MODE
{
    LAMP_MODE_WHITE = 0,
    LAMP_MODE_COLOR
} LAMP_MODE;
```

IO \_ 堆栈 \_ 位置。DeviceIoControl. OutputBufferLength 是 Irp \>AssociatedIrp.SystemBuffer 字段中传递的缓冲区的长度（以字节为单位）。

### <a name="output-parameters"></a>输出参数

Irp- \>AssociatedIrp.SystemBuffer 使用灯具 \_ 模式值进行填充。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。 它会将 IoStatus 设置 \> 为保存 DWORD 值所需的字节数。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

## <a name="ioctl_lamp_set_mode"></a>IOCTL_LAMP_SET_MODE

IOCTL \_ 灯光 \_ 集 \_ 模式 i/o 请求设置 flash 操作的模式。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_MODE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0003, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向类型为灯光模式的缓冲区 \_ 。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

## <a name="ioctl_lamp_get_intensity_white"></a>IOCTL_LAMP_GET_INTENSITY_WHITE

IOCTL \_ 灯 \_ 获取 \_ 强度 \_ 当 flash 配置为发出白色光时，i/o 请求会查询光线强度。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0004, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向灯泡强度的 \_ \_ 白色结构。 有关详细信息，请参阅**备注**。

IO \_ 堆栈 \_ 位置。DeviceIoControl. OutputBufferLength 是 Irp \>AssociatedIrp.SystemBuffer 字段中传递的缓冲区的长度（以字节为单位）。

### <a name="output-parameters"></a>输出参数

Irp- \>AssociatedIrp.SystemBuffer 填充光强度信息。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

### <a name="remarks"></a>注解

此 IOCTL 的负载类型定义如下：

```cpp
// The I/O parameter type of IOCTL_LAMP_{GET|SET}_INTENSITY_WHITE.
typedef struct LAMP_INTENSITY_WHITE
{
    BYTE Value;
} LAMP_INTENSITY_WHITE;
```

值字段是介于0到100之间（含0和）的白色光源亮度。

## <a name="ioctl_lamp_set_intensity_white"></a>IOCTL_LAMP_SET_INTENSITY_WHITE

IOCTL \_ 灯 \_ 设置 \_ 强度 \_ 白色 i/o 请求将闪存设置为指定的光线强度。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_INTENSITY_WHITE \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0005, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向灯泡强度的 \_ \_ 白色结构（有关详细信息，请参阅[IOCTL_LAMP_GET_INTENSITY_WHITE](#ioctl_lamp_get_intensity_white) ）。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

## <a name="ioctl_lamp_get_intensity_color"></a>IOCTL_LAMP_GET_INTENSITY_COLOR

IOCTL \_ 灯 \_ 获取 \_ 强度 \_ 色 i/o 请求会在将闪存配置为发出颜色亮度时查询光线强度。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0006, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向灯光 \_ 强度 \_ 色结构。 有关详细信息，请参阅**备注**。

IO \_ 堆栈 \_ 位置。DeviceIoControl. OutputBufferLength 是 Irp \>AssociatedIrp.SystemBuffer 字段中传递的缓冲区的长度（以字节为单位）。

### <a name="output-parameters"></a>输出参数

Irp- \>AssociatedIrp.SystemBuffer 填充光强度信息。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

### <a name="remarks"></a>注解

此 IOCTL 的负载类型定义如下：

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

IOCTL \_ 灯 \_ 设置 \_ 强度 \_ 颜色 i/o 请求将闪光灯设置为指定的光线强度。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_INTENSITY_COLOR \
    CTL_CODE(IOCTL_LAMP_BASE, 0x0007, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向灯泡 \_ 强度 \_ 色结构（有关详细信息，请参阅[IOCTL_LAMP_GET_INTENSITY_COLOR](#ioctl_lamp_get_intensity_color) ）。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

## <a name="ioctl_lamp_get_emitting_light"></a>IOCTL_LAMP_GET_EMITTING_LIGHT

\_ \_ \_ \_ 如果已打开（闪光灯）指示灯，则 IOCTL 灯将发出轻型 i/o 请求查询。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_GET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0008, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向布尔类型的缓冲区。

IO \_ 堆栈 \_ 位置。DeviceIoControl. OutputBufferLength 是 Irp \>AssociatedIrp.SystemBuffer 字段中传递的缓冲区的长度（以字节为单位）。

### <a name="output-parameters"></a>输出参数

Irp- \>AssociatedIrp.SystemBuffer 填充了 flash 状态，这意味着闪存处于开启状态（例如，发射灯光）;否则为 FALSE。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。 它会将 IoStatus 设置 \> 为保存 DWORD 值所需的字节数。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

## <a name="ioctl_lamp_set_emitting_light"></a>IOCTL_LAMP_SET_EMITTING_LIGHT

IOCTL \_ 灯 \_ 设置 \_ 发出 \_ 的 i/o 请求开启/关闭（闪光灯）光。

### <a name="definition"></a>定义

```cpp
#define IOCTL_LAMP_SET_EMITTING_LIGHT
    CTL_CODE(IOCTL_LAMP_BASE, 0x0009, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

### <a name="input-parameters"></a>输入参数

Irp- \>AssociatedIrp.SystemBuffer 指向布尔类型的缓冲区，其值为 TRUE，表示 ON;否则为 FALSE。

### <a name="output-parameters"></a>输出参数

无。

### <a name="io-status-block"></a>I/o 状态块

驱动程序将 Irp- \> IoStatus 设置为 " \_ 成功" 或相应的 "错误" 状态。

如果在发出此请求时 MediaCapture 会话正在传输数据，则驱动程序应 \_ \_ 通过 Irp-IoStatus 返回错误（正在使用的状态资源 \_ ） \> 。

## <a name="asynchronous-notifications"></a>异步通知

如[*并发用例*](#concurrency-use-cases)中所述，需要使用闪存驱动程序将 PnP 通知发送到报表资源可用性。 这可以通过使用以下 Guid 调用 IoReportTargetDeviceChange （或 IoReportTargetDeviceChangeAsynchronous）来实现，具体取决于方案：

- 闪存资源已被逐出，因为捕获会话（或另一个闪烁应用程序）启动：

  | Attribute  | 设置                                |
  | ---------- | -------------------------------------- |
  | 标识符 | GUID \_ 灯泡 \_ 资源 \_ 丢失            |
  | 类 GUID | {F770E98C-4403-48C9-B1D2-4EEC3302E41F} |

- Flash 资源现在变为可用：

  | Attribute  | 设置                                |
  | ---------- | -------------------------------------- |
  | 标识符 | GUID \_ 灯泡 \_ 资源 \_ 可用       |
  | 类 GUID | {185FE7CE-2616-481B-9094-20BB893ACD81} |
