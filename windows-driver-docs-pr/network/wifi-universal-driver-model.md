---
title: WLAN 通用 Windows 驱动程序模型
description: WDI （WLAN 设备驱动程序接口）是适用于 Windows 10 的新的通用 Windows 驱动程序模型。
ms.assetid: 6EF92E34-7BC9-465E-B05D-2BCB29165A18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5532b9cdceb43e17b602d2610c46900d89a788b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844396"
---
# <a name="wlan-universal-windows-driver-model"></a>WLAN 通用 Windows 驱动程序模型


WDI （WLAN 设备驱动程序接口）是适用于 Windows 10 的新的通用 Windows 驱动程序模型。 WLAN 设备制造商可以编写在所有设备平台上运行的单个 WDI 微型端口驱动程序，所需要的代码比以前的本机 WLAN 驱动程序模型少。 Windows 10 中引入的所有新 WLAN 功能均需要基于 WDI 的驱动程序。

供应商提供的本机 WLAN 驱动程序继续在 Windows 10 中运行，但功能仅限于开发它们时所针对的 Windows 版本。

WDI 头文件 wditypes. hpp 和 dot11wdi 都包含在 WDK 中。

## <a name="how-to-write-a-universal-wlan-driver"></a>如何编写通用 WLAN 驱动程序


若要编写通用 WLAN 驱动程序，请参阅[使用通用 windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers)，并按照使用内核模式驱动程序（KMDF）模板*构建*通用驱动程序构建通用驱动程序一节中的步骤进行操作。

然后，请参阅 WDI 设计和参考部分，了解实施指南。

-   [WDI 微型端口驱动程序设计指南](wdi-miniport-driver-design-guide.md)
-   [WDI 微型端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

## <a name="related-topics"></a>相关主题


[通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers)

 

 






