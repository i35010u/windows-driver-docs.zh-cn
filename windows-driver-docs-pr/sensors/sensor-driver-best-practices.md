---
title: 传感器驱动程序最佳做法
description: 传感器驱动程序最佳做法
ms.assetid: adb20558-aa94-41a9-9d26-9d757bdb0999
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: bb14f60f709f5f9b29a9d58953271ec7f160c29c
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010129"
---
# <a name="sensor-driver-best-practices"></a>传感器驱动程序最佳做法


本部分介绍了传感器驱动程序的最佳做法。

## <a name="windows-hardware-certification-program-requirements"></a>Windows 硬件认证计划要求

Windows 硬件认证计划允许硬件制造商接收其设备符合使用 Windows 所需标准的认证。 该计划提供所有传感器的要求，以及针对位置传感器和环境轻型传感器的特定要求。 应使传感器驱动程序符合所有 Windows 硬件认证计划的要求。

通常，此 WDK 文档中的建议与计划要求相匹配。 但是，在创建要提交用于认证的传感器驱动程序时，必须查看官方 Windows 硬件认证计划文档。 有关 Windows 硬件认证计划的详细信息，请参阅 [Windows 硬件开发人员中心](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 网站。

## <a name="performance"></a>性能

使用位置 API 和传感器 API 时，请按照以下建议优化传感器性能：

-   使用对 [**ISensorDriver：： OnClientSubscribeToEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents) 和 [**ISensorDriver：： OnClientUnsubscribeFromEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents) 的调用来跟踪是否有任何程序监视事件。 当没有客户端订阅时停止引发事件。

-   使用为传感器属性 "当前报表间隔" 提供的值 \_ \_ \_ \_ 作为提示来了解事件的引发频率。 仅在建议的时间间隔内或之后引发事件，以防止对驱动程序提供的数据进行筛选。

-   有关设置当前报表间隔的信息，请参阅 [筛选数据](filtering-data.md) 主题。

-   如果可以这样做，则引发的事件不会比请求的最短报表间隔更频繁。

-   请求时提供数据。 尽管我们建议程序避免轮询数据，但 Api 不会限制这些同步请求。 如果适合，可以提供缓存数据。

## <a name="properties-and-data-fields"></a>属性和数据字段

以下要求适用于属性和数据字段。

-   设置或返回 [属性](sensor-properties.md)时，驱动程序必须使用正确的类型。

-   返回 [数据字段](sensor-categories--types--and-data-fields.md)时，驱动程序必须使用正确的类型。

## <a name="events"></a>事件

以下建议适用于传感器事件：

-   仅当当前报表间隔已过并且超出了更改敏感度时才引发数据更新事件。 这很大程度上是设备固件的一个功能。 但是，驱动程序必须在多个客户端之间进行仲裁。 有关详细信息，请参阅 [关于传感器驱动程序事件](about-sensor-driver-events.md)。

## <a name="related-topics"></a>相关主题
[写入位置传感器驱动程序](../gnss/writing-a-location-sensor-driver.md) 
[支持环境光线传感器](supporting-ambient-light-sensors.md) 
[传感器地理位置驱动程序示例](../gnss/sensors-geolocation-driver-sample.md)