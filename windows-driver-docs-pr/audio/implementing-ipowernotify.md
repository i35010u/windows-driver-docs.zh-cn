---
title: 实现 IPowerNotify
description: 实现 IPowerNotify
ms.assetid: 8bd8b4c8-1961-41ea-ba98-41e3a732ed37
keywords:
- IPowerNotify 接口
- 通知 WDK 音频
- 电源状态更改通知 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 626f1a98db318057d51c6ca800b4cb34815d06da
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209469"
---
# <a name="implementing-ipowernotify"></a>实现 IPowerNotify


## <span id="implementing_ipowernotify"></span><span id="IMPLEMENTING_IPOWERNOTIFY"></span>


如果驱动程序的微型端口对象 (参阅[音频微型端口对象接口](./audio-miniport-object-interfaces.md)) 或流对象 (参阅[音频流对象接口](./audio-stream-object-interfaces.md)) 需要了解电源状态更改，它们可支持其**QueryInterface**方法中的[IPowerNotify](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)接口，并可在每次发生电源更改时接收来自 PortCls 系统驱动程序的通知。

当电源状态更改时，PortCls 会调用 [**IPowerNotify：:P owerchangenotify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-ipowernotify-powerchangenotify) 方法，分别通知每个支持 **IPowerNotify** 接口的微型端口和流对象。 在 **PowerChangeNotify** 调用过程中，微型端口对象应缓存新设备电源状态。 例如，在 **CAdapterCommon：： Init** 调用期间 (，请参阅 Microsoft Windows 驱动程序工具包 WDK) 中的 Msvad 示例适配器中的实现 \[ \] ，微型端口驱动程序应将其缓存的电源状态设置为初始值 PowerDeviceD0。

在调用 **PowerChangeState** 以关闭电源之前，PortCls 会调用 **IPowerNotify：:P owerchangenotify** ，使微型端口驱动程序有机会保存任何必需的设备上下文。 例如，此上下文可能包含体现当前筛选器拓扑和混音器设置的硬件注册值。 在调用 **PowerChangeState** 启动后，PortCls 会调用 **PowerChangeNotify** ，以便微型端口驱动程序可以还原已保存的上下文。

关机时，PortCls 会在调用 **PowerChangeNotify**之前暂停任何活动的音频数据流。 当启动时，PortCls 将调用 **PowerChangeNotify** ，然后重新启动任何暂停的音频数据流。

微型端口驱动程序的微型端口和流对象类可以继承自 **IPowerNotify** 接口，并支持其 **NonDelegatingQueryInterface** 方法中的此接口。 可以使用 \_ 标头文件 Portcls 中的 IMP IPowerNotify 定义将 **PowerChangeNotify** 方法的函数声明添加到驱动程序的微型端口和流对象的类定义。

 

