---
title: 从硬件中读取数据
description: 本主题说明如何示例传感器驱动程序来读取请求的响应中读取的传感器硬件 （加速感应器） 中的数据。
ms.assetid: 4C01324D-3C4D-4028-A7DE-0AD8F2233071
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01470a45d3bf3760020a9cd8f8edd1cf8ed13586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565626"
---
# <a name="read-data-from-hardware"></a>从硬件中读取数据


本主题说明如何示例传感器驱动程序来读取请求的响应中读取的传感器硬件 （加速感应器） 中的数据。

通常的"顶端"传感器驱动程序被旨在作为可以连接到传感器读取数据的应用程序可以访问。 示例传感器驱动程序中的"顶端"驱动程序的直接绑定到数据读取函数以读取加速感应器的示例数据。 以下部分介绍如何在示例传感器驱动程序中实现数据读取。

## <a name="handle-read-requests"></a>读取请求的句柄


1. 单击*client.cpp*文件将其打开，并查找**OnInterruptIsr**函数。
2. 找到以下代码：

```cpp
// Read the Interrupt source
   BYTE IntSrcBuffer = 0;
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   Status = I2CSensorReadRegister(pAccDevice->m_I2CIoTarget, ADXL345_INT_SOURCE, &IntSrcBuffer, sizeof(IntSrcBuffer));
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);
```

前面的代码将首先获取的锁在设备上，并确定源的中断，然后使用**I2CSensorReadRegister**函数。 最后，代码释放设备上的锁。

3. 找到以下代码：

```cpp
// Create work item
   InterruptRecognized = TRUE;

   BOOLEAN WorkItemQueued = WdfInterruptQueueWorkItemForIsr(Interrupt);
   TraceVerbose("%!FUNC! Work item %s queued for interrupt", WorkItemQueued ? "" : " already");
```

传感器驱动程序已成功确定源的中断后，传感器驱动程序将使用**WdfInterruptQueueWorkItemForIsr**创建框架的已排队的工作项。

## <a name="read-sensor-data"></a>读取传感器数据


示例传感器驱动程序将使用**GetData**若要检索的传感器实例，获取在设备上的锁，然后读取传感器数据。 当**GetData**函数调用返回，该锁被释放。

1. 内*client.cpp*文件中，找到**OnInterruptWorkItem**函数。 然后在该函数，查看下面的代码：

```cpp
// Invoke the function that Reads the device data
   WdfInterruptAcquireLock(Interrupt);
   Status = pAccDevice->GetData();
   WdfInterruptReleaseLock(Interrupt);
```

2. 查找**GetData**函数，并查找以下代码：
   ```cpp
   // Read the device data
   BYTE DataBuffer[ADXL345_DATA_REPORT_SIZE_BYTES];
   WdfWaitLockAcquire(m_I2CWaitLock, NULL);
   Status = I2CSensorReadRegister(m_I2CIoTarget, ADXL345_DATA_X0, &DataBuffer[0], sizeof(DataBuffer));
   WdfWaitLockRelease(m_I2CWaitLock);
   ```

前面的代码放在一边设置大小的缓冲区*DataBuffer*，并将设备数据读入的缓冲区，通过 I2C 连接。

3. 找到以下代码：
   ```cpp
   // Add timestamp
   FILETIME Timestamp = {};
   GetSystemTimeAsFileTime(&Timestamp);
   InitPropVariantFromFileTime(&Timestamp, &(m_pSensorData->List[SENSOR_DATA_TIMESTAMP].Value));

   SensorsCxSensorDataReady(m_SensorInstance, m_pSensorData);
   ```

前面的代码将时间戳添加到设备数据，然后将数据保存到设备上下文中的位置并使用*m\_pSensorData*来指向它。 这使可用的数据更上层的堆栈，至类扩展。

4. 关闭*client.cpp*文件。
 

 




