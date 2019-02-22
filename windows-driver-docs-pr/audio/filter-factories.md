---
title: 筛选器工厂
description: 筛选器工厂
ms.assetid: e836f941-274f-4e27-8069-753ef9ef2a06
keywords:
- 音频筛选器 WDK 音频，筛选器工厂
- 筛选器工厂 WDK 音频
- 筛选 WDK 音频工厂
- KS 筛选器 WDK 音频，筛选器工厂
- 音频插孔 WDK
- 扬声器 WDK 音频，筛选器工厂
- 实例化筛选器 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a86100076af0dc7329a1c005cc6043ed4dc9c787
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555969"
---
# <a name="filter-factories"></a>筛选器工厂


## <span id="filter_factories"></span><span id="FILTER_FACTORIES"></span>


音频适配器驱动程序提供了筛选器工厂来管理的筛选器实例化。 每个筛选器工厂可以实例化特定类型的一个或多个 KS 筛选器。 如果筛选器类型封装特定硬件函数，该工厂可以实例化该类型的筛选器数受底层硬件资源。

由于筛选器工厂管理硬件功能的很大程度上自治块，每个筛选器工厂可以被视为是自己权限内的设备驱动程序。 事实上，适配器驱动程序用作在上一段表示的相关驱动程序-一个集合术语的筛选器工厂-它们打包在一起以管理各种硬件函数上的适配器卡。

与任何其他 Microsoft Windows 驱动程序模型 (WDM) 驱动程序，筛选器工厂负责处理电源管理和安装功能。 在安装期间，驱动程序的 INF 文件会注册一个或多个筛选器设备名称 (请参阅[设备标识字符串](https://msdn.microsoft.com/library/windows/hardware/ff541224))。 此过程将名称加载到系统注册表，并将每个筛选器工厂与一个或多个 KS 筛选器类别关联，如中所述[音频适配器安装设备接口](installing-device-interfaces-for-an-audio-adapter.md)。 所有音频设备下 KSCATEGORY 进行分类\_音频，但将音频设备也可能属于在其他类别，如 KSCATEGORY\_（对于音频呈现设备） 的呈现器或 KSCATEGORY\_（用于捕获音频捕获设备）。 驱动程序会在设备的常规功能通告通过不同的类别在其下注册该设备的筛选器。 当[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)，例如，需要将音频设备注册表中的相应类别的设备特定类型的查找。

操作系统使用安装程序 API，如中所述[设备安装组件](https://msdn.microsoft.com/library/windows/hardware/ff728855)，以发现和枚举所有 KSCATEGORY\_音频筛选器工厂注册表中的。 每个工厂的注册表项指定筛选器工厂的友好名称和其设备名称，这是一个长字符串，客户端将传递给创建文件调用实例化筛选器。 可能会向发起此呼叫[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)从内核模式或设置为**CreateFile**从用户模式。 筛选器是一个内核模式对象，由内核句柄。 创建文件调用将返回客户端可以使用筛选器是指一个实例句柄。 用户模式下客户端或音频图形中的上游筛选器可以使用此句柄发送或 IOCTL 将请求转发到筛选器。 有关详细信息**CreateFile**，请参阅 Microsoft Windows SDK 文档。

典型的 WDM 音频适配器卡可能驻留在 PCI 总线，例如，并且包含用于呈现或捕获批数据的多个 I/O 连接器。 此卡上的单个音频设备可能包含用于驱动的发言人和线路输出电缆，一组模拟音频输出插孔和从麦克风和线路输入电缆接收信号的模拟音频插孔。 WDM 音频系统表示该设备是一个筛选器，该筛选器上的图钉形式表示的音频插孔。

音频设备的筛选器作为单独端口和微型端口驱动程序绑定在一起以统一行动：

-   微型端口驱动程序包含特定于硬件的代码。

-   端口驱动程序包含普遍适用于特定类型的所有筛选器的通用代码。

供应商将写入微型端口驱动程序，其中包含筛选器进行管理的音频硬件所需的所有专用代码。 操作系统提供的端口驱动程序，可通过 PortCls 系统驱动程序进行访问 (Portcls.sys，请参见[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver))。 将划分到端口和微型端口驱动程序的筛选器实现简化了编写专用设备的驱动程序的任务。

当筛选器工厂实例化筛选器时，它首先创建筛选器的微型端口驱动程序对象。 然后，筛选器工厂创建适当的端口对象的实例，并形成完全正常运行的筛选器将微型端口驱动程序对象绑定到该实例。 中的代码示例[子创建](subdevice-creation.md)说明了此过程。 通过定义完善的软件的接口彼此通信的端口和微型端口驱动程序。 有关这些接口的详细信息，请参阅[微型端口接口](miniport-interfaces.md)并[支持设备](supporting-a-device.md)。

音频筛选器作为 pin 工厂、 节点和内部连接的集合公开基础的音频设备的结构。 微型端口驱动程序将筛选器描述符，这是类型的结构到这些信息合并[ **PCFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537694)。 此结构，又包含各个描述符的筛选器的 pin 工厂、 节点和内部连接。 这些描述符是以下类型的结构：

[**PCPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537721)

[**PCNODE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537720)

[**PCCONNECTION\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537688)

若要从微型端口驱动程序获取筛选器描述符，端口驱动程序调用[ **IMiniport::GetDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff536765)方法。

为举例说明如何将驱动程序设置了其 PCFILTER\_描述符结构，请参阅 sb16 示例音频驱动程序在 Windows Driver Kit (WDK) 中的标头文件 Table.h。

 

 




