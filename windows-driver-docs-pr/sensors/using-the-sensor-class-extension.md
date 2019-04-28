---
title: 使用传感器类扩展
description: 传感器类扩展支持传感器驱动程序和传感器 API 之间的链接。
ms.assetid: F9632F86-10E8-4006-8FB7-97FA5EED492D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10b4818e8e7da6513df09adffb1fe2a1abf8db0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345059"
---
# <a name="using-the-sensor-class-extension"></a>使用传感器类扩展


传感器类扩展支持传感器驱动程序和传感器 API 之间的链接。

传感器应用程序会通过注册以接收事件通知从驱动程序检索 ADXL345 数据字段。 一旦应用程序注册为数据更新事件，该驱动程序将引发这些事件每次从传感器接收数据。 这些事件通知的频率与当前报告间隔属性相对应。

当驱动程序调用**ISensorClassExtension::PostEvent**中的方法**CSensorDdi::PostDataEvent**方法，则类扩展会将通知转发到传感器 API。 示例驱动程序支持事件处理线程。 与此线程关联的代码从传感器接收数据的更新，并确保该驱动程序将数据发布在指定的报表时间间隔。 此代码会调用**CSensorDdi::ReportIntervalExpired**方法，反过来，调用该方法**PostDataEvent**方法。

## <a name="related-topics"></a>相关主题
[SpbAccelerometer 驱动程序示例](spbaccelerometer-driver-sample.md)  
[驱动程序 I/O 模型](the-driver-i-o-model.md)  



