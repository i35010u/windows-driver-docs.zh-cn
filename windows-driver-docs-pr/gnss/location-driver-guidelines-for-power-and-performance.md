---
title: 位置驱动程序功率和性能指南
description: 以下各节介绍了一些准则，以确保你的位置驱动程序节省电源并有效地提供数据。
ms.assetid: 81B9A3A1-D273-48C8-A808-CDB1533A1B6A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7df6a2de8280f37b16ae6b8be9786e2d728aadb8
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980688"
---
# <a name="location-driver-guidelines-for-power-and-performance"></a>位置驱动程序功率和性能指南

以下各节介绍了一些准则，以确保你的位置驱动程序节省电源并有效地提供数据。

## <a name="tracking-the-number-of-connected-clients-and-radio-state"></a>跟踪连接的客户端和无线电状态的数目

位置传感器必须跟踪已连接的应用程序的数目，并且必须跟踪传感器\_属性\_位置的值\_所需的\_准确性和传感器\_属性\_当前\_报表\_每个已订阅应用程序的间隔属性。

如果连接的客户端数为零，则位置传感器应输入可能的最低电源状态，即 D3。 当某个事件指示客户端已连接时，传感器应退出低功耗状态并获取数据。

此外，如果位置设备包含收音机，如 GPS 位置传感器，则还必须使用 "[无线电管理](https://docs.microsoft.com/previous-versions/windows/hardware/radio/hh406615(v=vs.85))" 跟踪该无线电状态。 驱动程序编写器必须创建与驱动程序通信的收音机管理实现以设置无线电状态。 无线管理实现和如何与驱动程序通信的示例位于[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)中。

当跟踪已连接的客户端和无线电状态时，位置传感器应输入最小可能的电源状态，即 D3，无论何时，当无线电处于开启状态时，都没有连接的客户端。 下图演示了连接的客户端、无线电状态和建议的相应设备状态的状态机。

![状态机](images/state-diagram-with-radio.png)

下表提供了各种输入组合和生成的输出（包括电源状态）的另一个视图。

|               |             |                  |                   |            |               |             |
|---------------|-------------|------------------|-------------------|------------|---------------|-------------|
| 输入        |             |                  |                   | 输出    |               |             |
| 客户端存在 | 无线电收发器状态 | CRI              | 报告的位置 | ASIC 状态 | 传感器状态  | 电源状态 |
| 无            | 任意         | 任意              | 任意               | Off        | N/A           | D3          |
| “是”           | On          | &lt;= 120 秒 | 无                | On         | 初始化  | D0          |
| “是”           | On          | &lt;= 120 秒 | “是”               | On         | Ready         | D0          |
| “是”           | Off         | 任意              | 任意               | Off        | 未推出 | D3          |
| “是”           | On          | &gt;120 秒  | 任意               | Off        | Ready         | D3          |
| “是”           | On          | &gt;120 秒  | 任意               | On         | Ready         | D0          |

WDK 中的[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)提供了一个驱动程序示例，该驱动程序跟踪连接的客户端数和无线电状态。

## <a name="tracking-report-intervals"></a>跟踪报表间隔

通过订阅事件来使用位置数据的应用程序通过将传感器\_属性设置\_当前\_报表\_INTERVAL 属性，来请求数据更新事件的最大频率。 为了节省电源，您的驱动程序应发送的数据报告不会比请求的请求报告时间间隔更少。

有关如何跟踪每个应用程序的值的详细信息，请参阅[筛选数据](https://docs.microsoft.com/windows-hardware/drivers/sensors/filtering-data)。 你还可以在 WDK 的[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)中找到跟踪报表间隔的示例。

## <a name="tracking-desired-accuracy"></a>跟踪所需准确性

正如每个客户端跟踪报表间隔一样，必须跟踪每个客户端请求的准确性级别。

WDK 中的[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)提供一个驱动程序示例，用于跟踪客户端请求的所需准确性。

位置传感器驱动程序必须支持传感器\_属性\_位置\_所需的\_准确性作为可设置属性。 驱动程序应监视已连接客户端的所需准确性属性，并根据所需的最高所需准确性，将传感器\_属性\_位置设置为\_所需\_准确性。

如果需要应用所需的最高准确性\_准确度\_默认情况下，位置传感器应优化电源和其他成本注意事项。 如果位置数据可从系统中的其他提供程序使用，且数据准确性500m 或更佳，则 Location API 不会使用 GPS 传感器。

如果任何应用请求\_准确性\_高，则传感器应提供可能的最高准确性报告。 Location API 始终连接到所有位置传感器（包括 GPS），以便尽可能获得最准确的位置。

## <a name="detecting-idle-states"></a>检测空闲状态

你的驱动程序应检测到空闲状态并进入低功耗状态。 例如，如果 GPS 设备的位置未更改、没有挂起的 i/o 请求或者数据不可用，则可能会发生空闲状态。 如果 GPS 或全局导航卫星系统（GNSS）设备通过 USB 实现，则它必须支持选择性挂起。 有关详细信息，请参阅[在基于 UMDF 的驱动程序中支持空闲电源关闭](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-idle-power-down-in-umdf-drivers)。

## <a name="position-injection-for-gps-and-global-navigation-satellite-system-gnss"></a>GPS 和全局导航卫星系统（GNSS）的位置注入

GPS 或全局导航卫星系统（GNSS）传感器可以使用系统中的三角化传感器数据来缩短首次修复的时间。 这称为*位置注入*。

仅在采集阶段支持传感器到传感器通信的使用。 全局导航卫星系统（GNSS）驱动程序可以通过传感器 API 与任何三角传感器（包括 Windows 位置提供程序）建立连接。 如果位置数据可用，则驱动程序可以获得一个粗糙位置。 在获取位置之后，驱动程序应立即关闭连接。

如果全局导航卫星系统（GNSS）驱动程序在15秒内没有从传感器 API 获得位置，则应该超时并关闭与传感器 API 的连接。 请勿继续订阅事件。

> [!IMPORTANT]
> 与 Windows 位置提供程序（或通过传感器 API 的任何其他传感器）的持久连接不应保持打开状态。

> [!IMPORTANT]
> 不要实例化[**ILocation**](https://docs.microsoft.com/windows/desktop/api/locationapi/nn-locationapi-ilocation)以从其他位置传感器获取数据。 请改用传感器 API （[**ISensorManager**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nn-sensorsapi-isensormanager)）。

> [!NOTE]
> 传感器不应从同一类型的位置传感器获取数据。 例如，三角化传感器不应使用其他三角传感器的数据。

若要访问三角化传感器，请将[**ISensorManager：： GetSensorByType**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensormanager-getsensorsbytype)与类型为传感器\_类型\_位置\_三角化。 这将返回所有三角化传感器，包括 Windows 8 中内置的 Windows 位置提供程序。 你的 GPS 驱动程序需要能够处理从零传感器返回到多个传感器的任何位置。 有关使用**GetSensorsByType**的详细信息，请参阅[检索传感器对象](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-a-sensor)。

> [!NOTE]
> Windows 位置提供程序不提供准确性或可用性的任何保证。

不支持使用传感器 API 来实现传感器到传感器通信，以启用位置合成（例如，使用加速感应器或 gyro 磁力仪数据来估计物理位置）。

## <a name="related-topics"></a>相关主题

[写入位置传感器驱动程序](writing-a-location-sensor-driver.md)  

[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  
