---
title: WLAN 通用 Windows 驱动程序模型
description: WDI （WLAN 设备驱动程序接口） 是适用于 Windows 10 的新通用 Windows 驱动程序模型。
ms.assetid: 6EF92E34-7BC9-465E-B05D-2BCB29165A18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2c8b90af05caab82984ea70c062f5d3e682ab3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378960"
---
# <a name="wlan-universal-windows-driver-model"></a>WLAN 通用 Windows 驱动程序模型


WDI （WLAN 设备驱动程序接口） 是适用于 Windows 10 的新通用 Windows 驱动程序模型。 WLAN 设备制造商可以编写在所有设备平台上运行的单个 WDI 微型端口驱动程序，并且需要比以前的本机 WLAN 驱动程序模型更少的代码。 Windows 10 中引入的所有新 WLAN 功能均需要基于 WDI 的驱动程序。

供应商提供的本机 WLAN 驱动程序继续在 Windows 10 中运行，但功能仅限于开发它们时所针对的 Windows 版本。

WDI 标头文件，wditypes.hpp 和 dot11wdi.h，包含在 WDK 中。

## <a name="how-to-write-a-universal-wlan-driver"></a>如何编写通用 WLAN 驱动程序


若要编写通用 WLAN 驱动程序，请参阅[通用 Windows 驱动程序入门](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)，并按照一节中的步骤*构建通用 Windows 驱动程序*通用驱动程序使用进行生成内核模式驱动程序 (KMDF) 模板中。

然后，请参阅实现指南 WDI 设计和引用部分。

-   [WDI 微型端口驱动程序设计指南](wdi-miniport-driver-design-guide.md)
-   [WDI 微型端口驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/dn926075)

## <a name="related-topics"></a>相关主题


[通用 Windows 驱动程序入门](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)

 

 






