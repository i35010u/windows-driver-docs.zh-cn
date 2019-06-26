---
title: 空闲状态和活动电源的 GPU 电源管理
description: 允许 Windows 显示器驱动程序模型 (WDDM) 1.2 和更高版本的驱动程序的 GPU 电源管理基础结构管理个人设备或一组设备的能力。
ms.assetid: F8096F7E-39EA-45CB-8A1C-60A7A298AFEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2316226a9c2ba032831faf9ca1ab7ba79f683990
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379964"
---
# <a name="gpu-power-management-of-idle-states-and-active-power"></a>空闲状态和活动电源的 GPU 电源管理


从 Windows 8 开始，是可选的 GPU 电源管理基础结构可用，可让 Windows 显示器驱动程序模型 (WDDM) 1.2 和更高版本的驱动程序管理的电源可用于单个设备或一组设备。 此基础结构提供了支持 F 状态和 P 状态电源管理中与 Windows 协作的标准化的机制。

|                                                                                   |                                        |
|-----------------------------------------------------------------------------------|----------------------------------------|
| WDDM 的最低版本                                                              | 1.2                                    |
| 最大 Windows 版本                                                           | 8                                      |
| 驱动程序实现                                                             | 可选                               |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **Device.Graphics…RuntimePowerMgmt** |

 

## <a name="span-idgpupowermanagementdevicedriverinterfaceddispanspan-idgpupowermanagementdevicedriverinterfaceddispanspan-idgpupowermanagementdevicedriverinterfaceddispangpu-power-management-device-driver-interface-ddi"></a><span id="GPU_power_management_device_driver_interface__DDI_"></span><span id="gpu_power_management_device_driver_interface__ddi_"></span><span id="GPU_POWER_MANAGEMENT_DEVICE_DRIVER_INTERFACE__DDI_"></span>GPU 电源管理设备驱动程序接口 (DDI)


这些新的和更新函数和结构可从 Windows 8 为显示微型端口驱动程序转换电源组件的状态和交流电源与 Microsoft DirectX 图形内核子系统的事件开始。

-   [*DxgkCbCompleteFStateTransition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_completefstatetransition)
-   [*DxgkCbPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_powerruntimecontrolrequest)
-   [*DxgkCbSetPowerComponentActive*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentactive)
-   [*DxgkCbSetPowerComponentIdle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentidle)
-   [*DxgkCbSetPowerComponentLatency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentlatency)
-   [*DxgkCbSetPowerComponentResidency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentresidency)
-   [*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)
-   [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_POWER\_COMPONENT\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_power_component_flags)
-   [**DXGK\_POWER\_COMPONENT\_MAPPING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_power_component_mapping)
-   [**DXGK\_电源\_组件\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_power_component_type)
-   [**DXGK\_POWER\_RUNTIME\_COMPONENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_power_runtime_component)
-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)
-   [**DXGKARG\_QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)
-   [**DXGK\_QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)

## <a name="span-idgpupowermanagementscenariosspanspan-idgpupowermanagementscenariosspanspan-idgpupowermanagementscenariosspangpu-power-management-scenarios"></a><span id="GPU_power_management_scenarios"></span><span id="gpu_power_management_scenarios"></span><span id="GPU_POWER_MANAGEMENT_SCENARIOS"></span>GPU 电源管理方案


Gpu 和显示屏幕是便携式计算机、 移动设备和桌面 Pc 中的最大电源消耗者的两个。

以下是关键的电源管理方案，以减少能源消耗并延长电池使用时间：

-   移动设备可以进入空闲状态，并保存 power，因为如果未使用关闭各个系统组件。
-   Windows 系统上的芯片 (SoC) – 基于的设备的行为类似消费型电子设备和移动手机，即它们启用立即其在需要时，从而节约能源。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...RuntimePowerMgmt**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





