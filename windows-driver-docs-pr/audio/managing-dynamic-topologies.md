---
title: 管理动态拓扑
description: 管理动态拓扑
keywords:
- 动态拓扑音频
- 插座状态检测 WDK 音频
- 注册 subdevices
- 动态 subdevices WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edbbea4ae10bf9283428db418c40bc85967064be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801035"
---
# <a name="managing-dynamic-topologies"></a>管理动态拓扑


音频适配器包含一定数量的 subdevices，用于维护外部音频设备（如扬声器和麦克风），用户将其插入适配器的前面板或后面板音频插孔。 每个 subdevice 都是特定音频插孔或插孔组的服务。

音频驱动程序通过提供一种实质上是内部连接和 subdevice 中的处理元素映射的拓扑，来描述每个 subdevice。 系统提供的 Windows API 模块和供应商提供的控制面板应用程序使用拓扑信息来确定 subdevice 的功能，并确定其内部控制点。 有关详细信息，请参阅 [公开筛选器拓扑](exposing-filter-topology.md)。

在 [IUnregisterSubdevice](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice) 和 [IUnregisterPhysicalConnection](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection) 接口可用之前开发的 WDM 音频驱动程序通常是静态拓扑。 对于这些驱动程序，在适配器驱动程序创建一个用于管理 subdevice 的微型端口驱动程序对象之后，该对象及其关联的 subdevice 在适配器驱动程序对象的生存期内保持不变。

但是，在可动态配置的音频适配器中，适配器驱动程序可以在运行时创建和删除 subdevices，以反映硬件配置中的更改，因为用户将外部设备插入音频插孔并将其删除。 此行为允许 subdevices 作为逻辑上独立的硬件功能运行。 换句话说，每个 subdevice 都可以进行开机、配置，并独立于其他 subdevices 进行关闭。

每个 subdevice 都有一个内部拓扑，其中包含以下内容：

-   通过 subdevice 的数据路径。

-   拓扑节点 (例如，用于处理沿数据路径传递的数据流的音量控制) 。

-   Subdevice 与同一适配器中其他 subdevices 的物理连接。

当适配器驱动程序动态删除 subdevice 时，它会释放绑定到 subdevice 的内部拓扑的硬件资源。 然后，适配器驱动程序可以使用这些资源来创建具有可能不同拓扑的新 subdevice。

配置新的音频 subdevice 时，适配器驱动程序会将 subdevice 的驱动程序接口注册为一个或多个 [设备接口类](../install/overview-of-device-interface-classes.md)的实例，并且 i/o 管理器会添加一个或多个注册表项，其中包含关联接口类和接口实例的符号链接。 若要访问 subdevice，用户模式客户端将从注册表中检索符号链接，并将其作为调用参数传递给 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 函数。 通常情况下，客户端是 Windows API 模块，如 Dsound.dll 或 winspool.drv，或者供应商提供的控制面板或音频实用程序。 有关 **CreateFile** 的详细信息，请参阅 Microsoft Windows SDK 文档。

当微型端口驱动程序调用 [**IUnregisterSubdevice：： UnregisterSubdevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice) 方法来删除 subdevice 时，PortCls 系统驱动程序 ( # A0) 通知 i/o 管理器从注册表中删除关联设备接口的符号链接。 注册为设备接口删除事件的组件会在删除接口时收到通知。

音频适配器可以包含插孔状态电路，以便在插入到音频插孔或从音频插孔中删除插头时通知微型端口驱动程序。 当用户将某个插头插入音频插孔时，适配器驱动程序会将相关 subdevice 的设备接口添加到注册表中。 当用户从音频插孔中删除插头时，适配器驱动程序将从注册表中删除相应的设备接口。

支持动态拓扑的音频适配器具有以下优势：

-   用户友好

    除非桌面扬声器、耳机和其他外部音频设备实际插入音频适配器前端或后面板上的音频插孔，否则系统不会将这些设备提供给音频应用程序以供使用。

-   节能

    当用户从音频插孔中删除插头时，驱动程序可以切断服务该插孔的适配器电路的部分。

-   可配置

    删除 subdevice 后，驱动程序可以使用绑定到 subdevice 的内部拓扑的硬件资源来创建具有可能不同拓扑的新 subdevice。

 

