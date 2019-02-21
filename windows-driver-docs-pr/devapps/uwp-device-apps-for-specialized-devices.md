---
title: UWP 应用的内部设备的设备应用程序
description: 本主题介绍了 UWP 的设备应用程序可以访问内部设备方法。
ms.assetid: 864EDABF-C734-425D-A532-A01E545E4E51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7722bee32ecdcee22804d0bb9a1aa8ebc709826
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521003"
---
# <a name="uwp-device-apps-for-internal-devices"></a>UWP 应用的内部设备的设备应用程序


本主题介绍了 UWP 的设备应用程序可以访问内部设备方法。 *内部设备*是驻留在或集成在一起的 PC 机箱的设备。

**请注意**  本主题中提到的某些 Api 可用于访问外部设备过。 本主题专门重点介绍访问内部设备。 有关每个 API 的详细信息，请参阅[Windows API 参考](https://go.microsoft.com/fwlink/p/?LinkId=250938)。

 

## <a name="span-idaccessinginternaldevicesspanspan-idaccessinginternaldevicesspanspan-idaccessinginternaldevicesspanaccessing-internal-devices"></a><span id="Accessing_internal_devices"></span><span id="accessing_internal_devices"></span><span id="ACCESSING_INTERNAL_DEVICES"></span>访问内部设备


有三种方法，UWP 应用可以访问内部设备：

| 建议？ | API                                                  | 开发人员      | 是所需的设备元数据？    |
|--------------|------------------------------------------------------|----------------|---------------------------------|
| 是          | 设备方案 Api （映像捕获，扫描，等等。） | 所有开发人员 | 否                              |
| 是          | 设备协议 Api （如 USB、 HID 等）。                | OEM            | 是 （对于仅限内部设备） |
| 否           | 自定义驱动程序访问                                 | OEM            | 是                             |

 

## <a name="span-iddevicescenarioapisspanspan-iddevicescenarioapisspanspan-iddevicescenarioapisspandevice-scenario-apis"></a><span id="Device_scenario_APIs"></span><span id="device_scenario_apis"></span><span id="DEVICE_SCENARIO_APIS"></span>设备方案 Api


Windows 运行时提供了几个 Api 用于访问是内置的或附加到 PC，例如为映像捕获，扫描、 打印以及使用运动传感器 Api 的常见设备。 这些 Api 的设计中考虑到一个特定方案，因为它们被称为*设备方案 Api*。 设备方案 Api 可由所有开发人员，并使用其所需的任何设备元数据。 有关方案的 Api 的详细信息，请参阅[集成设备]( https://go.microsoft.com/fwlink/p/?LinkId=306557)。

Api 提供了哪些设备方案以外的任何访问限制为 Oem （或组件供应商整合，处理与 Oem 结合使用），并需要将系统容器的设备元数据。

## <a name="span-iddeviceprotocolapisspanspan-iddeviceprotocolapisspanspan-iddeviceprotocolapisspandevice-protocol-apis"></a><span id="Device_protocol_APIs"></span><span id="device_protocol_apis"></span><span id="DEVICE_PROTOCOL_APIS"></span>设备协议 Api


当 OEM/组件供应商需要访问 Api 的方案不能满足一种方法在内部设备时，它们可以使用*设备协议 Api*。 设备协议 Api 是 UWP 应用可用于访问 USB 和人机接口设备 (HID) 的 Windows 运行时 Api。 每个 API 而异的访问类型。

| 设备协议 API | 命名空间                                                                               | 访问类型                      |
|---------------------|-----------------------------------------------------------------------------------------|----------------------------------|
| USB                 | [Windows.Devices.Usb](https://go.microsoft.com/fwlink/p/?LinkId=306694)                  | 独占读取和排他写入 |
| HID                 | [Windows.Devices.HumanInterfaceDevice](https://go.microsoft.com/fwlink/p/?LinkId=306697) | 共享的读取和排他写入    |

 

若要访问使用唯一 Microsoft 类驱动程序的设备协议 Api 的最常见用途-的外围设备的设备元数据不需要。 但是，若要访问这些 Api 与内部设备，不需要元数据。 当访问内部设备，必须为特权的系统容器的应用中设备元数据指定应用。 此要求将内部设备的访问限制为 Oem。

有关详细信息，请参阅：

-   [为 USB 设备编写应用程序](https://go.microsoft.com/fwlink/p/?LinkId=324880)
-   [支持人机接口设备 (HID)](https://go.microsoft.com/fwlink/p/?LinkId=324881)
-   [支持蓝牙设备](https://go.microsoft.com/fwlink/p/?LinkId=324882)
-   [设备驱动程序要求](step-1--create-a-uwp-device-app.md)（步骤 1 中的分步指南）
-   [创建设备元数据](step-2--create-device-metadata.md)（步骤 2 的分步指南）

## <a name="span-idcustomdriveraccessspanspan-idcustomdriveraccessspanspan-idcustomdriveraccessspancustom-driver-access"></a><span id="Custom_driver_access"></span><span id="custom_driver_access"></span><span id="CUSTOM_DRIVER_ACCESS"></span>自定义驱动程序访问


Oem 或 Ihv 无法使用设备协议 Api 来访问其 （内部或外围设备） 设备时，应首先联系 Microsoft 以讨论 Windows 生态系统团队使用其方案。 在某些情况下-Microsoft 批准的后 UWP 设备应用程序可以直接访问自定义驱动程序。

自定义驱动程序的访问要求设备元数据。 若要访问自定义驱动程序，该应用程序必须指定设备元数据中作为用于外围设备或系统容器的特权应用程序。 有关自定义驱动程序访问的详细信息，请参阅[UWP 设备应用程序设计指南适用于 PC 的内部专用设备](https://go.microsoft.com/fwlink/p/?LinkId=306693)。

## <a name="span-idcomponentsuppliersspanspan-idcomponentsuppliersspanspan-idcomponentsuppliersspancomponent-suppliers"></a><span id="Component_suppliers"></span><span id="component_suppliers"></span><span id="COMPONENT_SUPPLIERS"></span>组件供应商


组件供应商可以使用 Oem 开发 UWP 应用为其内部的设备的设备应用程序。 这可以通过多种方法中：

-   **组件供应商开发并分发应用**:在这种情况下，组件供应商拥有，开发，并分配应用和访问内部的设备的驱动程序。 OEM 拥有的设备元数据。

-   **OEM 开发并分发应用**:在这种情况下，OEM 开发并分发的应用程序访问一个或多个内部设备中不同组件供应商。 OEM 最终拥有应用程序开发、 应用分发和维护设备元数据。 组件供应商拥有该驱动程序。

有关这些工作流的详细信息，请参阅[UWP 设备应用程序设计指南适用于 PC 的内部专用设备](https://go.microsoft.com/fwlink/p/?LinkId=306693)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[确定内部相机 （UWP 设备应用） 的位置](identifying-the-location-of-internal-cameras.md)

 

 






