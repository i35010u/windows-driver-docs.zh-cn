---
title: 特定于设备的上下文
description: 特定于设备的上下文
ms.assetid: 29e0d451-57fb-4943-9508-022adffa4650
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 997a393dadee38d8f955e3f4b81a60dd3cc975ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562118"
---
# <a name="device-specific-contexts"></a>特定于设备的上下文





微型驱动程序可以根据需要进行使用的专用上下文来存储特定于设备的信息。 此设备特定的上下文可以减少的微型驱动程序必须调用设备以获取设备信息的次数。 可以为特定的微型驱动程序的每个驱动程序项只有一个特定于设备的上下文。 当不再需要的驱动程序项时，WIA 服务调用微型驱动程序的[ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543972)方法来释放的所有附加到特定于设备的资源上下文。

例如，当照相机驱动程序从设备检索缩略图的数据，它通常会缓存与相应的驱动程序项关联的驱动程序上下文中的数据。 请注意，WIA 服务会释放上下文。 驱动程序的职责是只需释放由其上下文占用任何资源。 如果前一示例的缩略图的数据存储在内存中分配的设备特定的上下文中，应在这里，将缓存的数据的内存存放释放但上下文本身。

 

 




