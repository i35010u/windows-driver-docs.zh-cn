---
title: 适用于内部设备的 UWP 设备应用
description: 此主题介绍 UWP 设备应用访问内部设备的方式。
ms.assetid: 864EDABF-C734-425D-A532-A01E545E4E51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c0e4a8af47a024d6c181a8153bce8b6e5de0ee2
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733356"
---
# <a name="uwp-device-apps-for-internal-devices"></a>适用于内部设备的 UWP 设备应用


此主题介绍 UWP 设备应用访问内部设备的方式。 *内部设备* 是位于或与 PC 机箱集成的设备。

**注意**   本主题中提到的某些 Api 也可用于访问外部设备。 本主题重点介绍如何访问内部设备。 有关每个 API 的详细信息，请参阅 [WINDOWS api 参考](/uwp/api/)。

 

## <a name="span-idaccessing_internal_devicesspanspan-idaccessing_internal_devicesspanspan-idaccessing_internal_devicesspanaccessing-internal-devices"></a><span id="Accessing_internal_devices"></span><span id="accessing_internal_devices"></span><span id="ACCESSING_INTERNAL_DEVICES"></span>访问内部设备


UWP 应用可以使用三种方法访问内部设备：

| 您? | API                                                  | 开发人员      | 是否需要设备元数据？    |
|--------------|------------------------------------------------------|----------------|---------------------------------|
| 是          | 设备方案 Api (映像捕获、扫描等 )  | 所有开发人员 | 否                              |
| 是          | 设备协议 Api (USB、HID 等 )                 | OEM            | 是 (仅适用于内部设备)  |
| 否           | 自定义驱动程序访问                                 | OEM            | 是                             |

 

## <a name="span-iddevice_scenario_apisspanspan-iddevice_scenario_apisspanspan-iddevice_scenario_apisspandevice-scenario-apis"></a><span id="Device_scenario_APIs"></span><span id="device_scenario_apis"></span><span id="DEVICE_SCENARIO_APIS"></span>设备方案 Api


Windows 运行时提供了多个 Api，用于访问内置或附加到电脑的常见设备，如用于映像捕获、扫描、打印和使用运动传感器的 Api。 由于这些 Api 是使用特定的方案设计的，因此它们被称为 *设备方案 api*。 设备方案 Api 可由所有开发人员使用，无需设备元数据即可使用。 有关方案 Api 的详细信息，请参阅 [集成设备]( https://go.microsoft.com/fwlink/p/?LinkId=306557)。

超出设备方案 Api 所提供的任何访问权限仅限于 Oem (或组件供应商，与 Oem) 配合工作，并且需要系统容器的设备元数据。

## <a name="span-iddevice_protocol_apisspanspan-iddevice_protocol_apisspanspan-iddevice_protocol_apisspandevice-protocol-apis"></a><span id="Device_protocol_APIs"></span><span id="device_protocol_apis"></span><span id="DEVICE_PROTOCOL_APIS"></span>设备协议 Api


如果 OEM/组件供应商需要以方案 Api 不满足的方式访问内部设备，则可以使用 *设备协议 api*。 设备协议 Api 是 Windows 运行时的 Api，UWP 应用可以使用这些 Api (HID) 访问 USB 和人体学接口设备。 每个 API 的访问类型各不相同。

| 设备协议 API | 命名空间                                                                               | 访问类型                      |
|---------------------|-----------------------------------------------------------------------------------------|----------------------------------|
| USB                 | [Windows.Devices.Usb](/uwp/api/Windows.Devices.Usb)                  | 独占读取 & 独占写入 |
| HID                 | [Windows.Devices.HumanInterfaceDevice](/uwp/api/Windows.Devices.HumanInterfaceDevice) | 共享读取 & 独占写入    |

 

若要访问仅使用 Microsoft 类驱动程序的外围设备-设备协议 Api 的最常见用途-设备元数据不是必需的。 但是，若要使用这些 Api 访问内部设备，需要元数据。 访问内部设备时，必须在设备元数据中将应用指定为系统容器的特权应用。 此要求限制内部设备对 Oem 的访问。

有关详细信息，请参阅：

-   [为 USB 设备编写应用](/previous-versions/windows/apps/dn263144(v=win.10))
-   [ (HID) 支持人体学接口设备 ](/previous-versions/windows/apps/dn263140(v=win.10))
-   [支持蓝牙设备](/previous-versions/windows/apps/dn264587(v=win.10))
-   从循序渐进指南的第1步 ([设备驱动程序要求](step-1--create-a-uwp-device-app.md)) 
-   [创建设备元数据](step-2--create-device-metadata.md) (循序渐进指南的步骤 2) 

## <a name="span-idcustom_driver_accessspanspan-idcustom_driver_accessspanspan-idcustom_driver_accessspancustom-driver-access"></a><span id="Custom_driver_access"></span><span id="custom_driver_access"></span><span id="CUSTOM_DRIVER_ACCESS"></span>自定义驱动程序访问


如果 Oem 或 Ihv 无法使用设备协议 Api 来访问其 (内部或外围) 设备，则他们应该首先联系 Microsoft 以与 Windows 生态系统团队讨论他们的方案。 在某些情况-根据 Microsoft 审批-UWP 设备应用可以直接访问自定义驱动程序。

自定义驱动程序访问需要设备元数据。 若要访问自定义驱动程序，必须在设备元数据中将应用指定为外围设备或系统容器的特权应用。 有关自定义驱动程序访问的详细信息，请参阅 [适用于 PC 内部专用设备的 UWP 设备应用设计指南](https://go.microsoft.com/fwlink/p/?LinkId=306693)。

## <a name="span-idcomponent_suppliersspanspan-idcomponent_suppliersspanspan-idcomponent_suppliersspancomponent-suppliers"></a><span id="Component_suppliers"></span><span id="component_suppliers"></span><span id="COMPONENT_SUPPLIERS"></span>组件供应商


组件供应商可以与 Oem 合作，为其内部设备开发 UWP 设备应用。 这种情况可能发生在以下几种情况：

-   **组件供应商开发和分发应用程序**：在这种情况下，组件供应商拥有、开发和分发访问内部设备的应用程序和驱动程序。 OEM 拥有设备元数据。

-   **Oem 开发和分发应用程序**：在这种情况下，oem 开发并分发访问不同组件供应商的一个或多个内部设备的应用程序。 OEM 最终拥有应用开发、应用分发和设备元数据维护。 组件供应商拥有该驱动程序。

有关这些工作流的详细信息，请参阅 [适用于 PC 内部专用设备的 UWP 设备应用设计指南](https://go.microsoft.com/fwlink/p/?LinkId=306693)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[确定 (UWP 设备应用的内部照相机位置) ](identifying-the-location-of-internal-cameras.md)

 

