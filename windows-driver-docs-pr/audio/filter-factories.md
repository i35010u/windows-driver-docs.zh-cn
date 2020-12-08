---
title: 筛选器工厂
description: 筛选器工厂
keywords:
- 音频筛选 WDK 音频，筛选器工厂
- 筛选器工厂 WDK 音频
- 筛选 WDK 音频、工厂
- KS 筛选 WDK 音频，筛选器工厂
- 音频插孔
- 扬声器 WDK 音频，筛选器工厂
- 实例化对 WDK 音频的筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b17c9c9045a950f5f734ff892bc53b4f3d22d96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784805"
---
# <a name="filter-factories"></a>筛选器工厂


## <span id="filter_factories"></span><span id="FILTER_FACTORIES"></span>


音频适配器驱动程序提供筛选器工厂以管理筛选器的实例化。 每个筛选器工厂可以实例化特定类型的一个或多个 KS 筛选器。 如果筛选器类型封装了特定的硬件函数，则工厂可以实例化的该类型的筛选器数目将受到底层硬件资源的限制。

由于筛选器工厂管理很大程度上自治的硬件功能块，因此每个筛选器工厂都可以视为设备驱动程序。 事实上，上一段中使用的 "适配器驱动程序" 一词是指一组相关的驱动程序--筛选器工厂，它们打包在一起以管理适配器卡上的各种硬件功能。

与任何其他 Microsoft Windows 驱动模型 (WDM) 驱动程序一样，筛选器工厂处理电源管理和安装功能。 在安装过程中，驱动程序的 INF 文件将注册一个或多个筛选器设备名称 (参阅) 的 [设备标识字符串](../install/device-identification-strings.md) 。 此过程将名称加载到系统注册表中，并将每个筛选器工厂与一个或多个 KS 筛选器类别关联，如 [安装音频适配器的设备接口](installing-device-interfaces-for-an-audio-adapter.md)中所述。 所有音频设备都在 KSCATEGORY 音频下进行分类 \_ ，但音频设备还可能会分类为音频渲染设备的 KSCATEGORY 渲染 (，如音频 \_ 渲染) 设备的渲染 \_ () 。 驱动程序通过在其下注册该设备的筛选器的各种类别来公布设备的常规功能。 例如，当 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)需要特定类型的音频设备时，它会在注册表中查找属于相应类别的设备。

操作系统使用安装 API （如 [设备安装组件](../install/system-provided-device-installation-components.md)中所述）来发现和枚举注册表中的所有 KSCATEGORY \_ 音频筛选器工厂。 每个工厂的注册表项都指定筛选器工厂的友好名称和其设备名称，这是客户端传递给实例化筛选器的创建文件调用的长字符串。 此调用可能会从内核模式 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile) 或从用户模式 **CreateFile** 。 筛选器是一个内核模式对象，由内核句柄标识。 创建文件调用返回客户端可以用来引用筛选器的实例句柄。 音频图形中的用户模式客户端或上游筛选器可以使用此句柄来发送或转发对筛选器的 IOCTL 请求。 有关 **CreateFile** 的详细信息，请参阅 Microsoft Windows SDK 文档。

例如，典型的 WDM 音频适配器卡可能驻留在 PCI 总线上，并且包含用于呈现或捕获波数据的多个 i/o 连接器。 该卡上的单个音频设备可能包含模拟音频输出插孔，用于驱动一套扬声器和一 lineout 线，并使用模拟音频输入插孔接收来自麦克风和 linein 电缆的信号。 WDM 音频系统将设备表示为一个筛选器，并将音频插孔表示为该筛选器上的 pin。

音频设备的筛选器实现为单独的端口，并将小型端口驱动程序绑定在一起以协同操作：

-   微型端口驱动程序包含硬件特定的代码。

-   端口驱动程序包含特定类型的所有筛选器通用的通用代码。

供应商写入微型端口驱动程序，其中包含筛选器管理音频硬件所需的所有专有代码。 操作系统提供端口驱动程序，该驱动程序可以通过 PortCls 系统驱动程序进行访问， ( # A0;请参阅 [端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)) 。 将筛选器实现划分为端口和微型端口驱动程序可简化为专有设备编写驱动程序的任务。

当筛选器工厂实例化某个筛选器时，它将首先为该筛选器创建微型端口驱动程序对象。 然后，筛选器工厂创建适当端口对象的实例，并将微型端口驱动程序对象绑定到该实例，以形成完全正常运行的筛选器。 [Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。 端口和微型端口驱动程序通过定义完善的软件接口相互通信。 有关这些接口的详细信息，请参阅 [微型端口接口](miniport-interfaces.md) 和 [支持设备](supporting-a-device.md)。

音频筛选器将基础音频设备的结构公开为 pin 工厂、节点和内部连接的集合。 微型端口驱动程序将此信息合并到筛选器描述符中，后者是 [**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)类型的结构。 相反，此结构包含筛选器的固定工厂、节点和内部连接的各个描述符。 这些描述符是以下类型的结构：

[**PCPIN \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)

[**PCNODE \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor)

[**PCCONNECTION \_ 描述符**](/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))

若要从微型端口驱动程序获取筛选器描述符，端口驱动程序将调用 [**IMiniport：： GetDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription) 方法。

有关驱动程序如何设置其 PCFILTER 描述符结构的示例 \_ ，请参阅 Windows 驱动程序工具包中的 sb16 示例音频驱动程序中的头文件表 .h (WDK) 。

 

