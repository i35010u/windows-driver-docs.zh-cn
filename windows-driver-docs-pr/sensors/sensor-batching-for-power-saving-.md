---
title: 为了节能而对传感器数据进行批处理
description: 本主题介绍了所需传感器类扩展和传感器驱动程序，用于在 Windows 10 中实现批处理的传感器数据之间的接口。
ms.assetid: E64B9CE0-2C76-430A-ABE0-717BD27BCA8A
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6887e6081d6b29aed699cbf033ded20cc6a10620
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568232"
---
# <a name="sensor-data-batching-for-power-savings"></a>为了节能而对传感器数据进行批处理


本主题介绍了所需传感器类扩展和传感器驱动程序，用于在 Windows 10 中实现批处理的传感器数据之间的接口。

## <a name="introduction"></a>简介


实现数据批处理的传感器驱动程序，使应用程序处理器可以省电，因为处理器接收和频繁地处理传感器数据。 传感器驱动程序在这种情况下，缓冲区将传感器数据中的传感器硬件，然后将它们传输一起在批处理中给传感器类扩展。 若要支持批处理，必须提供实现所需的接口 UMDF 2.0 通用传感器驱动程序。

**批处理的延迟**

批处理延迟被指最大为其传感器可以缓冲数据样本收集，交付给传感器类扩展之前的时间量。 传感器数据批处理"schedule"介入时传感器事件传送由驱动程序，基于批处理的延迟值如以下关系图中所示。

![显示集合和发送的数据示例，使用正常数据传递序列关系图。](images/data-batching1.png)

对于不实现批处理的数据驱动程序，该驱动程序只需收集，并将传感器数据发送变得可用。 因此，例如，若要发送 n 个数据示例，该驱动程序会启动收集和发送的数据示例中，N 次。

![显示集合和发送的数据示例，使用 2 个批处理的批处理的数据传递序列关系图。](images/data-batching2.png)

在实现数据批处理、 数据收集和交付的驱动程序的情况下序列是将在执行批处理，如前面紧邻的关系图中所示。 由传感器类扩展指定批的延迟值。 因此当传感器硬件具有可收集和传输 n 个数据示例，例如，传感器驱动程序无法拆分过程为两个批。 N 个数据示例的第一半将等于批滞后时间的时间间隔后发送。 然后之后另一个批处理的延迟时间间隔，第二个将发送数据样本的一半，两个传输的总 N 传送所需的正常传递方法的比较。

## <a name="sensor-properties"></a>传感器属性


除了所需的通用传感器属性和枚举属性，支持数据批处理的驱动程序还必须报告以下属性：

-   PKEY\_Sensor\_FifoReservedSize\_Samples

-   PKEY\_Sensor\_FifoMaxSize\_Samples

-   PKEY\_Sensor\_WakeCapable

有关详细信息，请参阅[通用传感器属性](common-sensor-properties.md)并[枚举属性](enumeration-properties.md)。

如果支持唤醒的传感器硬件子系统，然后它应确保，它将启动唤醒设置得足够早以避免缓冲区溢出。

## <a name="optional-ddsi-functions-for-data-batching"></a>用于数据批处理的可选 DDSI 函数


设备驱动程序软件接口 (DDSI) 函数是驱动程序和类扩展之间的接口。 若要支持数据批处理，驱动程序必须实现以下 DDSI 函数，，以便传感器类扩展可以设置批处理延迟。

-   [EvtSensorSetBatchLatency](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)这是一个设置指定传感器的批次延迟的回调函数。 该驱动程序应设置为一个值，小于或等于该值的批处理延迟*BatchLatencyMs*参数，具体取决于缓冲区可用性。

该驱动程序还必须实现所有所需的 DDSI 函数。 有关详细信息，请参阅[传感器 DDSI 函数](sensor-ddsi-functions.md)。

它是可选的传感器类扩展，以指定批处理的延迟。 所有传感器的默认批处理延迟为零 (0)，用于指示不将批处理示例。 传感器示例将以提供批处理，仅当类扩展调用**EvtSensorSetBatchLatency**设置批的延迟值。 否则，这些示例将通常传递定期数据间隔速率。

传感器类扩展可以调用**EvtSensorSetBatchLatency**来随时更改批的延迟值。 具体而言，指定的传感器已处于活动状态且正在运行，而不会导致事件丢失，则可以调用此函数。 传感器驱动程序应收集并启动立即 （按最大努力） 交付的最新的批处理的示例。 该驱动程序不应超过指定的类扩展的批处理延迟。

请务必注意，没有对传感器数据传递方法和事件数据批处理暗示任何更改。 批处理滞后时间过期时，该驱动程序调用 SensorsCxSensorDataReady 重复，若要将所有缓冲的数据示例： 一个传递一次。 数据示例都伴随其时间戳 (包含在其关联的主键\_SensorData\_时间戳数据字段)，该值指示每个采样时拍摄。 有关主键的详细信息\_SensorData\_时间戳，请参阅[常见的数据字段](common-data-fields.md)。

## <a name="batch-latency-and-data-rate-relationship"></a>批处理的延迟和数据速率关系


批处理的延迟和数据率相关，如下所示：

![以毫秒为单位的批处理滞后时间值的公式。](images/batch-formula.png)

其中*SensorBatching\_MaxSize\_字节*批处理的传感器数据的缓冲区的最大大小。 如果您的传感器是加速感应器，则我们建议的硬件缓冲区，则大到足以保留 250 或更多示例。 以毫秒为单位，表示数据速率，并且将一个数据样本所需的时间长度。 传感器硬件必须存储在批处理中的样本数是与数据速率成反比。 越小数据速率，存储针对给定的批的延迟值的批处理的示例所需的更大示例的缓冲区。 在上面的公式，由表示批处理延迟*BatchLatencyMs* ，并且由数据速率*DataRateMs*。 如果的组合*BatchLatencyMs*并*DataRateMs*导致缓冲区大小是大于*SensorBatching\_MaxSize\_字节*，然后**EvtSensorSetBatchLatency**并[EvtSensorSetDataInterval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)会将批次延迟设置为前面的公式所显示的值。

如果调用方指定*BatchLatencyMs*值，该值是小于*DataRateMs*，则不进行缓冲传递数据。

## <a name="batching-with-data-thresholds"></a>批处理数据阈值


可以使用传感器驱动程序实现数据批处理[EvtSensorSetDataThresholds](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)若要设置非零数据阈值。 在这种情况下，当数据值中当前读数和最后一个读数，之间的差异超过使用设置的数据阈值**EvtSensorSetDataThresholds**，则数据收集、 批处理和交付过程调用。 因此，使用数据以及数据阈值，批处理允许传感器驱动程序，若要保存更强大的功能。

当非零数据阈值由传感器类扩展，以及数据批处理，设置驱动程序应提供准确的时间戳，批处理的示例，并遵守的数据阈值。 如果传感器硬件本身并不强制执行数据阈值，它可以无需强制实施数据阈值收集样本时保持准确的时间戳的支持。 但是，在这种情况下，驱动程序应筛选出不符合当前的数据阈值设置，交付给传感器类扩展之前的示例。

## <a name="sequence-diagram-examples"></a>顺序关系图示例


以下是显示如何使用批处理中提到的 DDSI 函数的可选数据的序列图[用于数据的可选 DDSI 函数批处理](#optional-ddsi-functions-for-data-batching)。 我们可以添加多个序列图根据需要以阐明方案基于合作伙伴的反馈意见。

**方案 1**

在此方案中，传感器类扩展启动传感器之前设置批处理的延迟和数据间隔。 一次在传感器开始时，它提供了批处理定期同时注意设置属性。

![显示方案类扩展将批处理的延迟和数据间隔设置启动传感器之前的序列关系图。](images/batch-scenario1.png)

**方案 2**

在此方案中，传感器类扩展启动传感器之前设置批处理延迟、 数据间隔和数据阈值。 一次在传感器开始时，它提供了批处理定期同时注意设置属性。 请注意驱动程序不应提供一批，除非提供了满足数据阈值的值，需要在指定的批处理滞后时间内发送的一个示例。

![序列图显示方案类扩展启动传感器之前在其中设置批处理的延迟、 数据间隔和数据阈值。](images/batch-scenario2.png)

**方案 3**

在此方案中，传感器类扩展启动传感器之前设置批处理的延迟和数据间隔。 一次在传感器开始时，它提供了批处理定期，同时遵循设置属性。 传感器正在运行，并且该驱动程序立即开始而不会丢失任何数据示例运行时提供新值根据示例时，传感器类扩展发生更改批处理的延迟和数据间隔时间。

![序列图显示方案，其中类扩展启动传感器之前设置的批次延迟、 数据间隔。 图还显示了如何在传感器继续响应中设置的更改时处理的数据传输。](images/batch-scenario3.png)

## <a name="data-batching-hardware-configurations"></a>数据批处理的硬件配置


必须在传感器硬件，而不需要应用程序处理器参与批处理的传感器数据。 这将允许处理器进入睡眠状态时数据需要批处理以节省电量。 下图显示了可能的传感器基于硬件的数据批处理配置。

-   **配置 1**:在传感器组件中，直接连接到应用程序处理器实现 FIFO 缓冲区。

-   **配置 2**:在传感器组件连接到的低功率传感器硬件核心实现 FIFO 缓冲区。 在这种情况下，可能会共享跨多个传感器，或甚至非传感器组件，具体取决于传感器核心设计与共享 FIFO 缓冲区。 低功率传感器 core 又、 连接到应用程序处理器和可能集成到 SoC. 或者，它可能是一个外部组件。

-   **配置 3**:在传感器组件中实现 FIFO 缓冲区。 传感器组件连接到已连接到应用程序处理器的低功率传感器核心。 传感器组件可能会将其集成到 SoC 也可能是一个外部组件。

-   **配置 4**:传感器组件和低功率传感器 core 实现 FIFO 缓冲区。 传感器组件连接到的低功率传感器核心反过来，并连接到应用程序处理器。 传感器组件可能会将其集成到 SoC，也可能是一个外部组件。 值得注意是传感器 core 可用于扩展 FIFO 是太浅表。

关键需要注意的事项是在传感器核心硬件或传感器的硬件和 / 或可实现 FIFO。 该驱动程序提取这对于操作系统，并提供了一个统一的界面，通过 DDSI。

下图说明了上述列表中所述的不同配置。

![显示用于托管的可能存在的硬件配置的关系图进行批处理的传感器数据。](images/sensor-batch-hw.png)

**在硬件中的缓冲区满行为**

在正常情况下，驱动程序应读取硬件缓冲区至少一次每个时间间隔等于*BatchLatencyMs*，以确保没有数据已被删除或丢失。 当硬件 FIFO 缓冲区填满时，它应环绕在周围和行为类似于一个循环缓冲区，覆盖较旧的事件。

 

 




