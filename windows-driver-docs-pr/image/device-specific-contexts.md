---
title: 特定于设备的上下文
description: 特定于设备的上下文
ms.assetid: 29e0d451-57fb-4943-9508-022adffa4650
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00727bc8cfc6a4e9fc3a484c548fd18738e7a425
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189603"
---
# <a name="device-specific-contexts"></a>特定于设备的上下文





微型驱动程序可以选择性地利用专用上下文来存储特定于设备的信息。 此设备特定的上下文可以减少微型驱动程序必须调用设备以获取设备信息的次数。 特定微型驱动程序的每个驱动程序项只能有一个设备特定的上下文。 当不再需要驱动程序项时，WIA 服务将调用微型驱动程序的 [**IWiaMiniDrv：:D rvfreedrvitemcontext**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext) 方法，以释放附加到设备特定上下文的所有资源。

例如，当照相机驱动程序从设备检索缩略图数据时，它通常会将数据缓存在与相应的驱动程序项相关联的驱动程序上下文中。 请注意，WIA 服务释放上下文。 驱动程序的责任只是释放其上下文所持有的所有资源。 如果上一个示例的缩略图数据存储在特定于设备的上下文中的内存中，则保存该缓存数据的内存应在此处释放，而不是在上下文本身中。

 

