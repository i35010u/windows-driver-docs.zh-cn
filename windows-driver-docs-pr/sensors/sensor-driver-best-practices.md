---
title: 传感器驱动程序的最佳做法
description: 传感器驱动程序的最佳做法
ms.assetid: adb20558-aa94-41a9-9d26-9d757bdb0999
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08bbeaf79f0cb6e91fc0ee847df4b1211c8644bc
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136110"
---
# <a name="sensor-driver-best-practices"></a>传感器驱动程序的最佳做法


本部分介绍传感器驱动程序的最佳做法。

## <a name="windows-hardware-certification-program-requirements"></a>Windows 硬件认证计划要求

Windows 硬件认证计划使硬件制造商以接收其设备满足所需的标准 Windows 所使用的证书。 该计划提供的要求的所有传感器和位置传感器和环境光线传感器的特定要求。 应使传感器驱动程序符合所有 Windows 硬件认证计划要求。

通常情况下，此 WDK 文档中的建议匹配程序的要求。 但是，你必须创建想要提交供认证的传感器驱动程序时查看官方 Windows 硬件认证计划文档。 有关 Windows 硬件认证计划的详细信息，请参阅[Windows 硬件开发人员中心](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))网站。

## <a name="performance"></a>性能

请遵循以下建议来优化性能的传感器，当您使用位置 API 和传感器 API:

-   使用为调用[ **ISensorDriver::OnClientSubscribeToEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)并[ **ISensorDriver::OnClientUnsubscribeFromEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents)到跟踪的任何程序正在监视的事件是否。 停止任何客户端所不订阅时引发事件。

-   使用传感器提供的值\_属性\_当前\_报表\_作为如何通常引发事件的提示的间隔。 仅期间或之后要防止筛选的数据，您的驱动程序提供的建议间隔引发事件。

-   有关设置当前报告间隔的信息，请参阅[筛选数据](filtering-data.md)主题。

-   如果可以执行此操作不比更频繁地请求，最短报表时间间隔内引发的事件。

-   提供数据请求时。 尽管我们建议程序避免在轮询数据，但 Api 不会限制这些同步请求。 适合时，您可以提供缓存的数据。

## <a name="properties-and-data-fields"></a>属性和数据字段

以下要求适用于属性和数据字段。

-   您的驱动程序必须使用正确的类型时设置，或返回时，[属性](sensor-properties.md)。

-   返回时，您的驱动程序必须使用正确的类型[数据字段](sensor-categories--types--and-data-fields.md)。

## <a name="events"></a>事件

以下建议适用于传感器事件：

-   已超过引发数据更新事件仅在当前报告间隔过后和变化敏感度。 这是很大程度上设备固件的函数。 但是，该驱动程序必须在多个客户端之间进行仲裁。 有关详细信息，请参阅[有关传感器驱动程序事件](about-sensor-driver-events.md)。

## <a name="related-topics"></a>相关主题
[编写位置传感器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gnss/writing-a-location-sensor-driver)
[支持环境光线传感器](supporting-ambient-light-sensors.md)
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



