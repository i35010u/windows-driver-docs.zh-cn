---
title: 显示设备的容器 ID 支持
description: 描述对显示的容器 ID 支持嵌入在显示器或监视器的设备中的设备的可视表示形式。
ms.assetid: 3149C156-34F4-4C55-AE77-1CC40C2B35BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e8e69a9d4f4b144ee561c4f080643e3d1f8d780
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356384"
---
# <a name="container-id-support-for-displays"></a>显示设备的容器 ID 支持


本主题介绍对显示的容器 ID 支持 — 嵌入在显示器或监视器的设备中的设备的可视表示形式。

|                                                                                   |                                          |
|-----------------------------------------------------------------------------------|------------------------------------------|
| Windows 显示器驱动程序模型 (WDDM) 的最低版本                               | 1.2                                      |
| 最大 Windows 版本                                                           | 8                                        |
| 驱动程序实现 — 仅完全图形和显示                              | 强制                                |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 |  [监视器容器 ID 功能测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4) |

 

## <a name="span-idcontaineriddevicedriverinterfaceddispanspan-idcontaineriddevicedriverinterfaceddispanspan-idcontaineriddevicedriverinterfaceddispancontainer-id-device-driver-interface-ddi"></a><span id="Container_ID_device_driver_interface__DDI_"></span><span id="container_id_device_driver_interface__ddi_"></span><span id="CONTAINER_ID_DEVICE_DRIVER_INTERFACE__DDI_"></span>容器 ID 设备驱动程序接口 (DDI)


在显示的微型端口驱动程序中实现此函数和结构：

-   [*DxgkDdiGetChildContainerId*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_get_child_container_id)
-   [**DXGK\_子\_容器\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_container_id)

## <a name="span-idcontaineriddescriptionspanspan-idcontaineriddescriptionspanspan-idcontaineriddescriptionspancontainer-id-description"></a><span id="Container_ID_description"></span><span id="container_id_description"></span><span id="CONTAINER_ID_DESCRIPTION"></span>容器 ID 说明


监视设备中的新功能可以提供更好的用户体验。 具体而言，通用串行总线 (USB) 集线器是监视器上的常用连接器用于连接的鼠标和键盘。 此外，等 HDMI 连接器支持音频，并且音频扬声器嵌入在监视器也因此。 许多新的显示设备支持触摸功能。 这通过减少网络干扰用户桌面上提供出色的用户体验。

请务必以可视方式表示的连接和这些设备的状态向用户直观的方式。 **设备和打印机**页中引入了 Windows 7。 如下所示，**设备和打印机**文件夹向用户显示已安装的设备连接到 PC，提供简单的方法来检查打印机、 音乐播放器、 照相机、 鼠标或数字图片画面 （以命名几个）。 同时，此页包含相同的硬件即可使用户更轻松地发现其驱动程序在这些设备进行分组。

![设备和打印机文件夹的可视表示形式](images/visualdevicesprintersfolder.jpg)

与 Windows 7 Microsoft 引入了的概念*容器 ID*的设备:"系统提供的设备标识字符串的唯一组功能的单函数或多功能与关联的设备设备在计算机中安装的。" (请参阅[容器 Id](https://go.microsoft.com/fwlink/p/?linkid=327784)。)设备进行分组，如果它们包含相同的容器 id。

为容器 ID 概念才能成功，在 Windows 中的所有设备类必须都支持它，并且整个生态系统需要在硬件中实现它。 在 Windows 7 中，如果插入支持音频的多个监视器，它并不便于用户来确定哪些显示映射到的音频的终结点。 触控数字化器存在相同的问题。 在 Windows 8 中，显示设备类添加支持的容器 id。 这样，可以为显示设备报告相同的容器 ID 并以可视方式获取配对中的 Windows 用户界面和 Api 的所有函数。

## <a name="span-idcontaineriduserscenariosspanspan-idcontaineriduserscenariosspanspan-idcontaineriduserscenariosspancontainer-id-user-scenarios"></a><span id="Container_ID_user_scenarios"></span><span id="container_id_user_scenarios"></span><span id="CONTAINER_ID_USER_SCENARIOS"></span>容器 ID 用户方案


具有嵌入音频扬声器的监视器，请考虑以下工作流：

1.  在用户连接监视器使用 HDMI 电缆。
2.  WDDM 驱动程序报告给 Windows 图形堆栈的显示设备存在。
3.  Windows 图形堆栈查询 WDDM 驱动程序使用 Windows 8 中引入的设备驱动程序接口 (DDIs) 的容器 ID。
4.  显示驱动程序查询的容器 ID 的监视器，并将其传递回 Windows。
5.  同时，音频驱动程序必须将完全相同的容器 ID 传递给 Windows 音频堆栈。
6.  如果在中查看**设备和打印机**控制面板、 显示和扬声器组合在一起。

在某些情况下，显示设备可能不包含容器 id。 在这种情况下，Windows 使用自动生成唯一的容器 ID 制造商 ID、 产品 ID 和序列号获取从扩展显示标识数据 (EDID)。 这些值是唯一的因为容器 ID 也是唯一的。 Windows 8 提供了将相同的信息传递给 WDDM 驱动程序，以便它可以传递给音频驱动程序生成相同的容器 id。 DDI

在少数情况下，Windows 之间转换的推动显示所有权、 WDDM 显示驱动程序和固件。 这些过渡是与硬件或软件，正在重置或重新配置可能会导致屏幕闪烁，闪烁相关联。 中讨论了可能的解决方案的方案和它们的行为[提供无缝的状态转换 WDDM 1.2 及更高版本](seamless-state-transitions-in-wddm-1-2-and-later.md)。

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上[容器 id 为显示器的功能测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/2f657caa-368c-4531-8cec-8faf475125f4)。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





