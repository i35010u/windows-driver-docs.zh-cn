---
title: 位置驱动程序功率和性能指南
description: 以下各节介绍准则以确保您位置的驱动程序，以节约能源并有效地提供数据。
ms.assetid: 81B9A3A1-D273-48C8-A808-CDB1533A1B6A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c315186a98d2aab5f70a73c1fa30584811ceed4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363655"
---
# <a name="location-driver-guidelines-for-power-and-performance"></a>位置驱动程序功率和性能指南


以下各节介绍准则以确保您位置的驱动程序，以节约能源并有效地提供数据。

### <a name="tracking-the-number-of-connected-clients-and-radio-state"></a>跟踪连接的客户端和单选状态的数

位置传感器必须跟踪连接的应用程序的数目和必须跟踪这两个传感器值\_属性\_位置\_所需\_准确性和传感器\_属性\_当前\_报表\_间隔属性为每个订阅应用程序。

当连接的客户端数为零时，位置传感器应输入最低可能的电源状态，最好是 D3。 当一个事件指示客户端连接时，传感器应退出低功耗状态，并获取数据。

此外，如果位置设备包含单选，例如 GPS 位置传感器，然后单选状态必须也使用跟踪[无线电管理](https://docs.microsoft.com/previous-versions/windows/hardware/radio/hh406615(v=vs.85))。 驱动程序编写器必须创建用于设置单选的状态的驱动程序进行通信的单选管理实现。 单选管理实现以及如何与驱动程序进行通信的一个示例是在[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)。

跟踪时连接的客户端和广播状态，位置传感器应输入最低可能的电源状态，最好是 D3，在没有连接的客户端上单选时任何时间。 下图展示了连接的客户端、 单选状态，并建议相应的设备状态的状态机。

![状态机](images/state-diagram-with-radio.png)

下表提供了另一个视图的不同输入组合，以及生成输出 （包括电源状态）。

|               |             |                  |                   |            |               |             |
|---------------|-------------|------------------|-------------------|------------|---------------|-------------|
| 输入        |             |                  |                   | outputs    |               |             |
| 客户端存在 | 无线电收发器状态 | CRI              | 位置报告 | ASIC 状态 | 传感器状态  | 电源状态 |
| 否            | Any         | Any              | Any               | 关闭        | 不可用           | D3          |
| 是           | 开          | &lt;= 120 秒 | 否                | 开         | 初始化  | D0          |
| 是           | 开          | &lt;= 120 秒 | 是               | 开         | 就绪         | D0          |
| 是           | 关闭         | Any              | Any               | 关闭        | 未推出 | D3          |
| 是           | 开          | &gt;120 秒  | Any               | 关闭        | 就绪         | D3          |
| 是           | 开          | &gt;120 秒  | Any               | 开         | 就绪         | D0          |

 

[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)WDK 中提供的跟踪的连接的客户端和单选状态数量的驱动程序示例。

### <a name="tracking-report-intervals"></a>跟踪报表时间间隔

通过订阅事件，使用位置数据的应用程序通过设置传感器请求数据更新事件的最大频率\_属性\_当前\_报表\_间隔属性。 为节省电源，您的驱动程序应不频率高于最低请求的报告间隔发送数据报告。

有关如何跟踪每个应用程序的值的详细信息，请参阅[筛选数据](https://docs.microsoft.com/windows-hardware/drivers/sensors/filtering-data)。 此外可以找到示例的跟踪中的报告间隔[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)WDK 中。

### <a name="tracking-desired-accuracy"></a>跟踪所需的准确性

就像报表时间间隔会跟踪每个客户端，必须跟踪每个客户端请求的准确性级别。

[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)WDK 中提供的跟踪所需的客户端请求的准确性的驱动程序示例。

位置传感器驱动程序必须支持传感器\_属性\_位置\_所需\_作为可设置属性的准确性。 该驱动程序应监视连接的客户端的所需的准确性属性并设置传感器\_属性\_位置\_所需\_准确性基于最高请求所需的精度。

如果所需的应用程序请求的最高准确性\_准确性\_默认情况下，位置传感器应优化电源和其他成本考虑事项。 位置 API 将使用 GPS 传感器，如果位置数据来自其他提供程序在系统上可用且数据的准确性是 500 分钟或更好的。

如果任何应用程序请求所需\_准确性\_传感器高，应提供可能的最高准确性报表。 位置 API 将始终连接到所有位置传感器 （包括 GPS） 以获取可能的最准确位置。

### <a name="detecting-idle-states"></a>检测空闲状态

您的驱动程序应检测空闲状态，并进入低功耗状态。 例如，GPS 设备的位置不会更改，没有任何挂起的 I/O 请求，或数据不可用时，可能会出现空闲状态。 如果你的 GPS 或 GNSS 设备通过 USB 中实现时，它必须支持选择性挂起。 请参阅[支持空闲电源关闭基于 UMDF 驱动程序中](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-idle-power-down-in-umdf-drivers)的详细信息。

### <a name="position-injection-for-gps-and-gnss"></a>GPS 和 GNSS 位置注入

GPS 或 GNSS 传感器可用于三角测量传感器数据在系统上加快了第一个修补程序。 这称为*定位注入*。

仅在采集阶段支持传感器与传感器之间通信的这种用法。 GNSS 驱动程序可能会打开与任何三角测量传感器，包括 Windows 位置提供程序，通过传感器 API 的连接。 该驱动程序然后可以获取一个粗略的位置，位置数据是否可用。 该驱动程序应关闭连接后立即获取位置。

如果 GNSS 驱动程序不会得到一个位置传感器 API 15 秒内，它应超时并关闭与传感器 API 的连接。 请不要继续订阅事件。

**重要**  Windows 位置提供程序 （或通过传感器 API 的任何其他传感器） 的持续性连接应不会保持打开。

 

**重要**  不实例化[ **ILocation** ](https://docs.microsoft.com/windows/desktop/api/locationapi/nn-locationapi-ilocation)从其他位置传感器获取数据。 请改用传感器 API ([**ISensorManager**](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nn-sensorsapi-isensormanager))。

 

**请注意**  传感器应从同一类型的位置传感器获取数据。 例如，三角测量传感器不应使用其他三角测量传感器数据。

 

若要访问三角测量传感器，请调用[ **ISensorManager::GetSensorByType** ](https://docs.microsoft.com/windows/desktop/api/sensorsapi/nf-sensorsapi-isensormanager-getsensorsbytype)类型传感器\_类型\_位置\_三角测量。 这将返回所有三角测量传感器，其中包括内置于 Windows 8 Windows 位置提供程序。 GPS 驱动程序必须能够处理任何位置从零到多个传感器返回的传感器。 请参阅[检索的传感器对象](https://docs.microsoft.com/windows/desktop/SensorsAPI/retrieving-a-sensor)有关详细信息的使用**GetSensorsByType**。

**请注意**  的 Windows 位置提供程序不提供任何保证的准确性或可用性。

 

不支持要启用位置合成 （例如，使用加速感应器或回转仪磁力仪数据来估计物理位置） 传感器与传感器之间通信的传感器 api 使用。

## <a name="related-topics"></a>相关主题
[编写位置传感器驱动程序](writing-a-location-sensor-driver.md)  
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



