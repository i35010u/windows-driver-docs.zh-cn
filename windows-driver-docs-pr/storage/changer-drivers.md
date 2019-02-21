---
title: 更换器驱动程序
description: 更换器驱动程序
ms.assetid: 47310de7-e69d-4f06-9995-3d95783d607a
keywords:
- 更换器驱动程序 WDK 存储
- 存储更换器驱动程序 WDK
- 存储驱动程序 WDK，更换器驱动程序
- 更换器驱动程序 WDK 存储有关更换器驱动程序
- 存储更换器驱动程序 WDK，有关更换器驱动程序
- 自动加载器 WDK 存储
- 自动转换器 WDK 存储
- 自动唱片点唱机 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6448d7eec54d0611dbc81f8efa2f27b45332008c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545495"
---
# <a name="changer-drivers"></a>更换器驱动程序


## <span id="ddk_changer_drivers_kg"></span><span id="DDK_CHANGER_DRIVERS_KG"></span>


本部分包含以下信息：

[系统提供更换器驱动程序](system-supplied-changer-drivers.md)

[供应商提供更换器驱动程序](vendor-supplied-changer-drivers.md)

[将特定于设备的信息存储在换带机的设备扩展](storing-device-specific-information-in-the-changer-s-device-extension.md)

[处理换带机设备控制请求](processing-changer-device-control-requests.md)

更换器驱动程序控制的媒体库中，元素或*转换器*(有时称为*自动换带机*，*换带机*，或*自动唱片点唱机*). 在基于 NT 的操作系统，用于更换器的驱动程序包含以下：

-   为一个库，提供的系统提供的转换器类驱动程序*mcd.lib*，提供了通用的转换器的所有驱动程序的功能

-   特定于设备的 miniclass 驱动程序，以静态方式链接到*mcd.lib*，提供由转换器类驱动程序以支持特定类型转换器的调用的例程

本部分包含用于写入新的转换器 miniclass 驱动程序的指导原则。

 

 




