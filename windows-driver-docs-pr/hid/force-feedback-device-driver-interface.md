---
title: 强制反馈设备驱动程序接口
description: 强制反馈设备驱动程序接口
ms.assetid: 59668521-84b9-4a1a-980b-6de57422a2c5
keywords:
- 强制反馈驱动程序 WDK HID
- 虚拟游戏杆驱动程序 WDK HID，强制反馈
- VJoyD WDK HID，强制反馈
- 操纵杆 WDK HID，强制反馈
- 效果驱动程序 WDK 强制反馈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07d0bd13e619817bf6c7609f4cb8a8f4e87a758f
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355945"
---
# <a name="force-feedback-device-driver-interface"></a>强制反馈设备驱动程序接口

本部分介绍 DirectInput 与设备特定的强制反馈驱动程序之间的接口。

## <a name="oemforcefeedback-registry-settings"></a>OEMForceFeedback 注册表设置

新的操纵杆注册表项位于特定于 OEM 的密钥下，该密钥是使用注册表路径 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Control \\ windows.media.mediaproperties \\ PrivateProperties \\ 游戏杆 \\ OEM**为密钥下的每个操纵杆设备类型安装的。 在第一次安装设备时，将初始化存储在此 OEM 特定密钥下的数据，并将其仅用于参考目的。 除了为现有操纵杆设备定义的值外，还定义了两个新的可选一般值和一组特定于强制反馈的值。

对于包含**Manufacturer** \_ \_ 制造商名称字符串的 REGSTR ) ，这两个泛型值是包含版本信息和制造商字符串值 (REGSTR VAL 制造商的二进制值。 后者补充了包含设备名称的现有 **OEMName** 值。

定义了一个新的 **OEMForceFeedback** 键，用来保存强制反馈特定的键和值。 此项下的 " **效果** " 子项包含每个效果的两个值。

" **效果** " 子项下是子项列表，每个项的作用都是一项。 每个子项的名称是一个全局唯一标识符 (GUID) 形式，格式为 " {12345678-1234-1234-1234-123456789012} "。 在名为 "{...}" 的项下 为两个值。 默认值为该效果的字符串友好名称。 **属性**值为[**DIEFFECTATTRIBUTES**](https://docs.microsoft.com/windows/desktop/api/dinputd/ns-dinputd-dieffectattributes)结构。

```cpp
"{guid1}"
    Default value = friendly name for effect {guid1} (string)
    "Attributes" = DIEFFECTATTRIBUTES structure (binary)
"{guid2}"
    Default value = friendly name for effect {guid2} (string)
    "Attributes" = DIEFFECTATTRIBUTES structure (binary)
```

**OEMForceFeedback**键还包括一个值，该值包含设备属性和两个可选值中的一个。 在可选值中，如果使用的是 (DLL) 的环形3驱动程序，请使用 **CLSID** ; 如果使用的是 (VxD) ，则使用 **VJoyD** 。

```cpp
"Attributes" = DIFFDEVICEATTRIBUTES structure (binary)
"CLSID" = {GUID} for force feedback effect driver (string)(optional)
"VJoyD" = zero-length binary (optional)
```

可选值的名称指示所使用的接口形式。 如果 **CLSID** 值存在，则它应是一个字符串值，它包含 {12345678-1234-1234-1234-123456789012} 提供驱动程序接口的 COM 对象的 GUID，格式为 ""。 如果存在 **VJoyD** 值，则它应为长度为零的二进制值，该值指示与要使用的设备关联的 VJoyD 微型驱动程序应为驱动程序接口提供额外的回调。 添加一个值，以指示在实现时，人体学接口设备 (HID) 提供驱动程序接口。

如果设备支持不属于任何预定义类别的硬件效果 (DIEFT \_ CONSTANTFORCE、DIEFT \_ RAMPFORCE、DIEFT \_ 周期性、DIEFT \_ 条件或 DIEFT \_ CUSTOMFORCE) ，则该效果的 [**DIEFFECTATTRIBUTES**](https://docs.microsoft.com/windows/desktop/api/dinputd/ns-dinputd-dieffectattributes) 结构应指定 DIEFT \_ 硬件作为效果类型。

设备可以支持属于上一段落中列出 (某个预定义类别的硬件效果) 但还会接收不属于标准类型特定数据结构（ (DICONSTANTFORCE、DIRAMPFORCE、DIPERIODIC、DICONDITION 或 DICUSTOMFORCE) ）的其他参数。 有关这些结构的信息，请参阅 (SDK) 的 DirectX 软件开发工具包的 DirectInput 部分。 在这些情况下，该效果应列出两次，如下所示：

- 列出预定义类别下的效果。 如果应用程序在预定义类别中创建效果，则驱动程序应为指定的参数提供不属于标准类型特定的数据结构的适当默认值。

- 列出 DIEFT 硬件类别下的效果 \_ 。 创建特定类型特定的结构 (例如包含额外参数的 DIPERIODICFORCEWITHDECAY) 。

通过这种方式，为您的硬件设计的应用程序可以使用第二个效果说明符来访问该效果的完整功能，而为一般硬件设计的应用程序可以使用第一个效果说明符来访问该效果的基本功能。

## <a name="driver-interface"></a>驱动程序接口

如果强制反馈驱动程序是基于 COM 的，则 DirectInput 将创建驱动程序的实例。 如果指定的接口为 "VJoyD"，则 VJoyD 将加载 VJoyD 微型驱动程序。 这两个驱动程序路径都支持以下导出的方法：

[*DestroyEffect*](https://docs.microsoft.com/previous-versions/ff538410(v=vs.85))

[*初始化*](https://docs.microsoft.com/previous-versions/ff541025(v=vs.85))

[*DownloadEffect*](https://docs.microsoft.com/previous-versions/ff538601(v=vs.85))

[*GetEffectStatus*](https://docs.microsoft.com/previous-versions/ff538772(v=vs.85))

[*GetForceFeedbackState*](https://docs.microsoft.com/previous-versions/ff538776(v=vs.85))

[*Esc*](https://docs.microsoft.com/previous-versions/ff538680(v=vs.85))

[*SendForceFeedbackCommand*](https://docs.microsoft.com/previous-versions/ff543387(v=vs.85))

[*SetGain*](https://docs.microsoft.com/previous-versions/ff543406(v=vs.85))

[*StartEffect*](https://docs.microsoft.com/previous-versions/ff543458(v=vs.85))

[*StopEffect*](https://docs.microsoft.com/previous-versions/ff543460(v=vs.85))

所有强制反馈设备都支持此功能。

## <a name="user-mode-functions"></a>User-Mode 函数

DirectInput 通过创建由存储在操纵杆类型子项的 **OEMForceFeedback** 注册表子项中的 CLSID 命名的对象，来创建强制反馈效果驱动程序的实例。

由于使用 DirectInput 的应用程序不需要加载 OLE，因此效果驱动程序应注意不依赖于 OLE 特定的行为。 例如，使用 DirectInput 的应用程序不能依赖于调用 **CoFreeUnusedLibraries** 方法。 DirectInput 执行标准 COM 操作来创建效果驱动程序对象的实例。 下面描述了这应该对效果驱动程序实现的唯一可见效果。

DirectInput 释放最后一个效果驱动程序对象后，它会手动执行效果驱动程序 DLL 的 FreeLibrary。 因此，如果效果驱动程序 DLL 创建的其他资源不与效果驱动程序对象相关联，则应手动 LoadLibrary 自己的 DLL 引用计数，从而阻止 DirectInput 中的 FreeLibrary 提前卸载 DLL。

具体而言，如果效果驱动程序 DLL 创建一个工作线程，则只要该工作线程存在，效果驱动程序就必须执行此人工 LoadLibrary 操作。 如果不再需要该工作线程 (例如，当从最后一个影响驱动程序对象的通知) 时，工作线程应调用 FreeLibraryAndExitThread 方法以减小 DLL 引用计数并终止线程。

DirectInput 使用的所有量值和获取值在该范围内都是均匀和线性的。 物理设备中的任何非线性都必须由设备驱动程序进行处理，以使应用程序能够看到线性设备。

[IDirectInputEffectDriver](https://docs.microsoft.com/windows/desktop/api/dinputd/nn-dinputd-idirectinputeffectdriver)接口公开的用户模式强制反馈函数必须由强制反馈效果驱动程序 DLL 实现。 有关这些函数的详细信息，请参阅 IDirectInputEffectDriver。
