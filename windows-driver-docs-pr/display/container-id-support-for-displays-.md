---
title: 显示设备的容器 ID 支持
description: 介绍容器 ID 支持，显示嵌入到显示或监视设备内的设备的可视表示形式。
ms.assetid: 3149C156-34F4-4C55-AE77-1CC40C2B35BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 532a5f82f73183cecc9dad4634d99b92a5ba03a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839808"
---
# <a name="container-id-support-for-displays"></a>显示设备的容器 ID 支持


本主题介绍容器 ID 支持，其中显示了在显示或监视设备中嵌入的设备的可视表示形式。

|                                                                                   |                                          |
|-----------------------------------------------------------------------------------|------------------------------------------|
| 最小 Windows 显示器驱动程序模型（WDDM）版本                               | 1.2                                      |
| 最大 Windows 版本                                                           | 8                                        |
| 驱动程序实现-完整图形和仅显示                              | Mandatory                                |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 |  [监视器容器 ID 功能测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4) |

 

## <a name="span-idcontainer_id_device_driver_interface__ddi_spanspan-idcontainer_id_device_driver_interface__ddi_spanspan-idcontainer_id_device_driver_interface__ddi_spancontainer-id-device-driver-interface-ddi"></a><span id="Container_ID_device_driver_interface__DDI_"></span><span id="container_id_device_driver_interface__ddi_"></span><span id="CONTAINER_ID_DEVICE_DRIVER_INTERFACE__DDI_"></span>容器 ID 设备驱动程序接口（DDI）


在显示微型端口驱动程序中实现此函数和结构：

-   [*DxgkDdiGetChildContainerId*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_get_child_container_id)
-   [**DXGK\_子\_容器\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_container_id)

## <a name="span-idcontainer_id_descriptionspanspan-idcontainer_id_descriptionspanspan-idcontainer_id_descriptionspancontainer-id-description"></a><span id="Container_ID_description"></span><span id="container_id_description"></span><span id="CONTAINER_ID_DESCRIPTION"></span>容器 ID 描述


监视设备中的新功能可以提供更好的用户体验。 特别是，通用串行总线（USB）中心是监视器上用于连接鼠标和键盘的常用连接器。 此外，连接器（如 HDMI）支持音频，因此音频扬声器也嵌入到监视器中。 许多新的显示设备支持触摸功能。 这可以减少用户桌面的网络混乱，从而提供出色的用户体验。

以直观的方式向用户呈现这些设备的连接和状态很重要。 Windows 7 中引入了 "**设备和打印机**" 页面。 如下所示，"**设备和打印机**" 文件夹向用户显示连接到 PC 的已安装设备，并提供一种简单的方法来检查打印机、音乐播放机、照相机、鼠标或数字图片框（只需命名几个）。 同时，此页对包含在同一硬件中的设备进行分组，使用户能够更轻松地发现其所有驱动程序。

!["设备和打印机" 文件夹的可视化表示形式](images/visualdevicesprintersfolder.jpg)

在 Windows 7 中，Microsoft 引入了设备的*容器 ID*的概念： "系统提供的设备标识字符串，用于唯一地将与安装在计算机 "。 （请参阅[容器 id](https://go.microsoft.com/fwlink/p/?linkid=327784)。）如果设备包含相同的容器 ID，则对其进行分组。

为了使容器 ID 概念成功，Windows 中的所有设备类必须支持它，并且整个生态系统都需要在硬件中实现它。 在 Windows 7 中，如果插入了多个支持音频的监视器，用户将无法轻松确定哪些显示映射到哪些音频终结点。 触控数字化器存在相同的难度。 在 Windows 8 中，显示设备类添加了对容器 ID 的支持。 这使得显示设备的所有功能都可以报告相同的容器 ID 并在 Windows 用户界面和 Api 中以可视方式配对。

## <a name="span-idcontainer_id_user_scenariosspanspan-idcontainer_id_user_scenariosspanspan-idcontainer_id_user_scenariosspancontainer-id-user-scenarios"></a><span id="Container_ID_user_scenarios"></span><span id="container_id_user_scenarios"></span><span id="CONTAINER_ID_USER_SCENARIOS"></span>容器 ID 用户方案


请考虑具有嵌入音频扬声器的监视器的以下工作流：

1.  用户使用 HDMI 电缆连接监视器。
2.  WDDM 驱动程序报告显示设备是否存在于 Windows 图形堆栈中。
3.  Windows 图形堆栈使用 Windows 8 中引入的设备驱动程序接口（DDIs）来查询容器 ID 的 WDDM 驱动程序。
4.  显示驱动程序将查询监视器以获取容器 ID 并将其传递回 Windows。
5.  同时，音频驱动程序必须将完全相同的容器 ID 传递到 Windows 音频堆栈。
6.  如果在 "**设备和打印机**" 控制面板中查看，则显示和扬声器组合在一起。

在某些情况下，显示设备可能不包含容器 ID。 在这种情况下，Windows 将使用从扩展显示标识数据（EDID）获得的制造商 ID、产品 ID 和序列号来自动生成唯一容器 ID。 由于这些值是唯一的，因此容器 ID 也是唯一的。 Windows 8 提供了一个向 WDDM 驱动程序传递相同信息的 DDI，以便可以将其传递给音频驱动程序以生成相同的容器 ID。

在少数情况下，驱动显示的所有权在 Windows、WDDM 显示驱动程序和固件之间转换。 这些转换与硬件或正在重置或重新配置的软件相关联，并可能导致屏幕闪烁和闪烁。 在[WDDM 1.2 和更高版本中提供无缝状态转换](seamless-state-transitions-in-wddm-1-2-and-later.md)中讨论了可能的转换方案及其行为。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)，[了解监视容器 ID 的功能测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4)。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)，了解 Windows 8 中添加的功能。

 

 





