---
title: 管理动态拓扑
description: 管理动态拓扑
ms.assetid: 324c372b-c8d6-4eed-b4ea-071b3d5412b1
keywords:
- 动态拓扑 WDK 音频
- jack 存在检测 WDK 音频
- 注册子设备
- 动态子设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb7778874e402487f6c3990fc40c138385c45fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358678"
---
# <a name="managing-dynamic-topologies"></a>管理动态拓扑


音频适配器包含一定数量的子设备维护服务外部的音频设备，如扬声器和麦克风的用户插入到适配器前或后面板音频插孔。 每个子服务的特定音频插孔或组的插孔。

音频驱动程序通过显示是实质上是内部连接的映射的拓扑和处理中的子元素描述每个子。 系统提供的 Windows API 模块和供应商提供的控制面板应用程序使用的拓扑信息来确定子功能并确定其内部控件的点。 有关详细信息，请参阅[公开筛选器拓扑](exposing-filter-topology.md)。

之前已开发的 WDM 音频驱动程序[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)并[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)接口可供使用了具有主要是静态的拓扑。 对于这些驱动程序，适配器驱动程序创建一个用于管理子的微型端口驱动程序对象后该对象和其关联的子保持不变的适配器驱动程序对象的生存期。

但是，在可动态配置的音频适配器中，适配器驱动程序可以创建和删除子设备在运行时以反映在硬件配置中的更改与用户插入音频插孔的外部设备，并将其删除。 此行为允许子设备作为逻辑上独立于硬件函数来操作。 换而言之，可以启动、 配置和独立于其他子设备关闭每个子。

每个子具有以下内容组成的内部拓扑：

-   通过子数据路径。

-   处理流沿数据路径的数据流拓扑节点 （例如，音量控制）。

-   与其他子设备相同的适配器中的子的物理连接。

当适配器驱动程序动态将删除子时，它使绑定到子的内部拓扑的硬件资源。 适配器驱动程序然后可以使用这些资源来创建新的子使用可能是不同的拓扑。

在配置新的音频子，适配器驱动程序会将子的驱动程序接口注册为一个或多个实例[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)，并添加包含符号的一个或多个注册表项，I/O 管理器将接口的类和接口实例相关联的链接。 若要访问子，用户模式下客户端将从注册表检索的符号链接并将其传递到调用参数为[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。 通常情况下，客户端是 Windows API 模块，例如 Dsound.dll Wdmaud.drv 或供应商提供的控件面板或音频实用程序。 有关详细信息**CreateFile**，请参阅 Microsoft Windows SDK 文档。

当微型端口驱动程序调用[ **IUnregisterSubdevice::UnregisterSubdevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)方法来删除子 PortCls 系统驱动程序 (Portcls.sys) 告知 I/O 管理器中删除符号链接注册表中的关联的设备接口的链接。 注册的设备接口删除事件的组件接口删除时收到通知。

音频的适配器可以包含插孔存在电路时插入或删除从的音频插孔即插即用通知微型端口驱动程序。 当用户将即插即用到的音频插孔时，适配器驱动程序将关联子设备接口添加到注册表。 当用户从的音频插孔中删除插件时，适配器驱动程序从注册表中删除相应的设备接口。

支持动态拓扑的音频适配器具有以下优势：

-   用户友好

    桌面扬声器、 耳机和其他外部的音频设备实际插入到音频适配器的前面或背面面板上的音频插孔中，除非系统不会显示为可用的音频应用程序使用这些设备。

-   电源效率

    当用户从的音频插孔中删除插件时，可以关闭服务该插孔适配器电路的部分电源驱动程序。

-   可配置

    删除子之后, 该驱动程序可以使用已绑定到子的内部拓扑使用可能是不同的拓扑中创建新的子的硬件资源。

 

 




