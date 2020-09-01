---
title: 支持某个设备
description: 支持某个设备
ms.assetid: 5f60d3aa-6061-40f7-8108-d752534b88ed
keywords:
- 音频微型端口驱动程序 WDK，设备支持
- 微型端口驱动程序 WDK 音频，设备支持
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，设备支持
- 端口驱动程序 WDK 音频、微型端口驱动程序
- 端口驱动程序 WDK 音频，端口类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bd0920d662c39d412e21398828fc3b58e667d90
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209929"
---
# <a name="supporting-a-device"></a>支持某个设备


## <span id="supporting_a_device"></span><span id="SUPPORTING_A_DEVICE"></span>


PortCls 系统驱动程序 (*Portcls.sys*) 提供了几个内置的端口驱动程序来支持呈现和捕获 WAVE 和 MIDI 流的音频设备。

所有端口驱动程序都公开从基接口 [IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)派生的接口。 **IPort** 继承基接口 **IUnknown**中的方法。 **IPort** 提供了以下附加方法：

[**IPort::GetDeviceProperty**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-getdeviceproperty)

从注册表检索音频适配器的即插即用属性。
[**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)

初始化 port 对象。
[**IPort::NewRegistryKey**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-newregistrykey)

创建新的注册表项或打开现有的项。
PortCls 实现以下端口驱动程序：

[WaveCyclic 端口驱动程序](wavecyclic-port-driver.md)

[WavePci 端口驱动程序](wavepci-port-driver.md)

[WaveRT 端口驱动程序](wavert-port-driver.md)

[拓扑端口驱动程序](topology-port-driver.md)

[MIDI 端口驱动程序](midi-port-driver.md)

[Dmu 端口驱动程序](dmus-port-driver.md)

 

