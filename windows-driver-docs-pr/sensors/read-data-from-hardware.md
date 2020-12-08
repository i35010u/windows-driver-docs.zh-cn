---
title: 从硬件读取数据
description: 本主题介绍了示例传感器驱动程序如何从传感器硬件 (加速感应器) 响应读取请求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a90c6452abb04acc05dd6e11514ffd70db06caf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805105"
---
# <a name="read-data-from-hardware"></a>从硬件读取数据


本主题介绍了示例传感器驱动程序如何从传感器硬件 (加速感应器) 响应读取请求。

通常，传感器驱动程序的 "前端" 设计为可供连接到传感器的应用程序访问，以读取数据。 在示例传感器驱动程序中，驱动程序的 "前端" 直接绑定到数据读取功能，以便从加速感应器读取示例数据。 以下部分说明如何在示例传感器驱动程序中实现数据读取。

## <a name="handle-read-requests"></a>处理读取请求


1. 单击 *客户端 .cpp* 文件以将其打开，并找到 **OnInterruptIsr** 函数。
2. 找到以下代码：

```cpp
// Read the Interrupt source
   BYTE IntSrcBuffer = 0;
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   Status = I2CSensorReadRegister(pAccDevice->m_I2CIoTarget, ADXL345_INT_SOURCE, &IntSrcBuffer, sizeof(IntSrcBuffer));
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);
```

前面的代码首先获取设备上的锁，然后使用 **I2CSensorReadRegister** 函数确定中断的源。 代码最终在设备上释放锁。

3. 找到以下代码：

```cpp
// Create work item
   InterruptRecognized = TRUE;

   BOOLEAN WorkItemQueued = WdfInterruptQueueWorkItemForIsr(Interrupt);
   TraceVerbose("%!FUNC! Work item %s queued for interrupt", WorkItemQueued ? "" : " already");
```

传感器驱动程序成功确定中断的源后，传感器驱动程序将使用 **WdfInterruptQueueWorkItemForIsr** 为框架创建已排队的工作项。

## <a name="read-sensor-data"></a>读取传感器数据


示例传感器驱动程序使用驱动器 **驱动器来检索** 传感器实例，在设备上获取锁定，然后读取传感器数据。 当工作 **功能函数** 调用返回时，将释放该锁。

1. 在 *客户端 .cpp* 文件中，找到 **OnInterruptWorkItem** 函数。 然后，在该函数内查看以下代码：

```cpp
// Invoke the function that Reads the device data
   WdfInterruptAcquireLock(Interrupt);
   Status = pAccDevice->GetData();
   WdfInterruptReleaseLock(Interrupt);
```

2. 找到 " **功能的函数"，** 并找到以下代码：
   ```cpp
   // Read the device data
   BYTE DataBuffer[ADXL345_DATA_REPORT_SIZE_BYTES];
   WdfWaitLockAcquire(m_I2CWaitLock, NULL);
   Status = I2CSensorReadRegister(m_I2CIoTarget, ADXL345_DATA_X0, &DataBuffer[0], sizeof(DataBuffer));
   WdfWaitLockRelease(m_I2CWaitLock);
   ```

前面的代码将 *DataBuffer* 大小的缓冲区，并通过 I2C 连接将设备数据读入缓冲区。

3. 找到以下代码：
   ```cpp
   // Add timestamp
   FILETIME Timestamp = {};
   GetSystemTimeAsFileTime(&Timestamp);
   InitPropVariantFromFileTime(&Timestamp, &(m_pSensorData->List[SENSOR_DATA_TIMESTAMP].Value));

   SensorsCxSensorDataReady(m_SensorInstance, m_pSensorData);
   ```

前面的代码将时间戳添加到设备数据，然后将数据保存到设备上下文中的某个位置，并使用 *m \_ pSensorData* 指向该位置。 这使得数据在堆栈中的进一步可用到类扩展。

4. 关闭 *客户端 .cpp* 文件。
 

 




