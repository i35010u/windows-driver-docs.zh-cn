---
title: 支持某个设备
description: 支持某个设备
ms.assetid: 5f60d3aa-6061-40f7-8108-d752534b88ed
keywords:
- 音频的微型端口驱动程序 WDK、 设备支持
- 微型端口驱动程序 WDK 音频设备支持
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频设备支持
- 端口驱动程序 WDK 音频，微型端口驱动程序
- 端口驱动程序 WDK 音频，端口类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc78c0b0edf81c7983bbf37d02f78ecb87e9b1b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576929"
---
# <a name="supporting-a-device"></a>支持某个设备


## <span id="supporting_a_device"></span><span id="SUPPORTING_A_DEVICE"></span>


PortCls 系统驱动程序 (*Portcls.sys*) 提供了几个内置端口驱动程序以支持的呈现和捕获批和 MIDI 流音频设备。

所有端口驱动程序将派生自基接口的接口都公开[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)。 **IPort**方法继承自基接口**IUnknown**。 **IPort**提供了以下其他方法：

[**IPort::GetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff536941)

从注册表检索的音频适配器插属性。
[**IPort::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536943)

初始化端口对象。
[**IPort::NewRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff536945)

创建新的注册表项或打开现有的密钥。
PortCls 实现以下端口驱动程序：

[WaveCyclic 端口驱动程序](wavecyclic-port-driver.md)

[WavePci 端口驱动程序](wavepci-port-driver.md)

[WaveRT 端口驱动程序](wavert-port-driver.md)

[拓扑端口驱动程序](topology-port-driver.md)

[MIDI 端口驱动程序](midi-port-driver.md)

[Dmu 端口驱动程序](dmus-port-driver.md)

 

 




