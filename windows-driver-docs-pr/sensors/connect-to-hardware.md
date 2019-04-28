---
title: 连接到硬件
description: 本主题说明如何传感器驱动程序确定的已分配的硬件资源，并将连接到 I2C 驱动程序控制器。
ms.assetid: 88D9162B-2B99-4608-B31A-48B1810747A9
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4cfe5b54c8c43d2dc35ae1f82d71ec073e7be032
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330096"
---
# <a name="connect-to-hardware"></a>连接到硬件


本主题演示如何传感器驱动程序确定的已分配的硬件资源，然后连接到 I2C 驱动程序控制器，以便它可以连接到 ADXL345 硬件。

以下各节将使用来自示例驱动程序开发的代码片段 ADXL345 加速感应器，为测试用例来显示如何使连接到硬件传感器驱动程序。 如果尚未这样做，导航到[ADXL345Acc 示例](https://github.com/Microsoft/Windows-driver-samples/tree/1fbea08887e10e087c3f6bb0be8968e29e20cc84/sensors/ADXL345Acc)GitHub 上，以便你可以遵循说明。

这些代码段突出显示某些传感器驱动程序文件的重要部分。 但你必须查看整个，若要获取该驱动程序的工作原理，更好地理解并能够找出如何自定义这些文件可以获得您的传感器中的所有驱动程序文件。

## <a name="prepare-hardware-resources"></a>准备硬件资源


1. 单击*device.cpp*文件将其打开，然后查找**OnPrepareHardware**函数。 在该函数中，找到以下代码：
   ```cpp
   // Create WDFOBJECT for the sensor
    WDF_OBJECT_ATTRIBUTES sensorAttributes;
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&sensorAttributes, ADXL345AccDevice);
   ```

前面的代码创建一个传感器对象，并为其分配适当的设备上下文。

2. 找到以下代码：
   ```cpp
   // Register sensor instance with clx
    SENSOROBJECT SensorInstance = NULL;
    NTSTATUS Status = SensorsCxSensorCreate(Device, &sensorAttributes, &SensorInstance);
   ```

前面的代码中使用传感器类扩展注册传感器实例。 传感器实例创建而不是设备实例，以允许你必须在同一芯片中的多个传感器的场景。

3. 找到以下代码：
   ```cpp
   // Initialize sensor instance with clx
    SENSOR_CONFIG SensorConfig;
    SENSOR_CONFIG_INIT(&SensorConfig);
    SensorConfig.pEnumerationList = pAccDevice->m_pEnumerationProperties;
    Status = SensorsCxSensorInitialize(SensorInstance, &SensorConfig);
   ```

前面的代码中使用传感器类扩展来初始化传感器实例。

4. 找到以下代码：
   ```cpp
   Status = pAccDevice->ConfigureIoTarget(ResourcesRaw, ResourcesTranslated);
   ```

前面的代码中配置的传感器驱动程序的 I/O 目标对象。 I/O 目标对象，传感器驱动程序与其他驱动程序进行通信。

## <a name="configure-the-device-with-default-settings"></a>使用默认设置来配置设备


请记住，D0 设备的活动状态。 若要将设备置于 D0，需要在寄存器中的设备本身，此配置设置，并将通过 I2C 与设备通信。 必须在执行写入之前持有此资源的锁或读取。

内*device.cpp*文件中，找到**OnD0Entry**函数，并请注意，它调用**电源打开**，使用 ADXL345 上下文来执行的打开设备的工作。 内**电源打开**函数中，找到以下代码：
1.
```cpp
WdfWaitLockAcquire(m_I2CWaitLock, NULL);
```

前面的代码用于获取 I2C 总线的锁。

2. 找到以下代码：
   ```cpp
   // Write the default device configuration to the device
   For (DWORD i = 0; i < ARRAYSIZE(g_ConfigurationSettings); i++)
   {
       REGISTER_SETTING setting = g_ConfigurationSettings[i];
       Status = I2CSensorWriteRegister(m_I2CIoTarget, setting.Register, &setting.Value, sizeof(setting.Value));
       if (!NT_SUCCESS(Status))
       {
           TraceError("ACC %!FUNC! I2CSensorReadRegister from 0x%02x failed! %!STATUS!", setting.Register, Status);
           WdfWaitLockRelease(m_I2CWaitLock);
           return Status

       }
    }
   ```

For 循环用于写入到设备注册配置设置的默认值。

3. 找到以下代码：
   ```cpp
   // Release the I2C bus lock
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);

   InitPropVariantFromUInt32(SensorState_Idle, &(m_pSensorProperties->List[SENSOR_PROPERTY_STATE].Value));
   m_PoweredOn = true;
   ```

已成功配置设备后，WdfWaitLockRelease 用于释放为 I2C 总线锁。

4. 关闭*device.cpp*文件。
   ## <a name="start-the-device-activity"></a>启动设备活动


5. 单击*client.cpp*文件将其打开，并查找**OnStart**函数。
6. 查看下面的代码，用于获取传感器设备上的锁：
   ```cpp
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   ```

7. 找到以下代码：
   ```cpp
   // Set accelerometer to measurement mode
   REGISTER_SETTING RegisterSetting = { ADXL345_POWER_CTL, ADXL345_POWER_CTL_MEASURE };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

在上述代码中，I2C 连接用于加速感应器设置为*度量模式*以使其可供读取传感器值。 请参阅*adxl345.h*标头文件定义 ADXL345\_POWER\_CTL、 ADXL345\_POWER\_CTL\_度量值和本示例中使用的一些其他常量传感器驱动程序。

4. 找到以下代码：
   ```cpp
   // Enable interrupts
   RegisterSetting = { ADXL345_INT_ENABLE, ADXL345_INT_ACTIVITY };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);
   ```

*RegisterSetting*参数启用传感器的中断。 WdfWaitLockRelease 用于释放 I2C 总线上的锁。

## <a name="stop-the-device-activity-and-set-device-to-standby"></a>停止设备活动和备用设置设备


1. 内*client.cpp*文件中，查找中的以下代码**OnStop**函数：
   ```cpp
   // Disable interrupts
   REGISTER_SETTING RegisterSetting = { ADXL345_INT_ENABLE, 0 };
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

在前面的代码中， *RegisterSetting*参数捕获注册地址和配置代码。 在这种情况下 RegisterSetting.Register 是中断启用寄存器的地址，而 RegisterSetting.Value 配置注册，以停止发出中断的设备。

2. 查找以下代码，这会清除任何未处理的中断，可能仍处于挂起状态的设备：
   ```cpp
   // Clear any stale interrupts
   RegisterSetting = { ADXL345_INT_SOURCE, 0 };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

3. 找到以下代码，它将在设备设置为备用服务器模式。 此设置会停止设备活动：
   ```cpp
   // Set accelerometer to standby
   RegisterSetting = { ADXL345_POWER_CTL, ADXL345_POWER_CTL_STANDBY };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

## <a name="disconnect-hardware-resources"></a>断开连接的硬件资源


请注意，框架将使用**OnReleaseHardware**函数断开连接的 I/O 请求数据包 (IRP)，响应中的硬件资源来停止或删除该设备。

1. 内*client.cpp*文件中，在**DeInit**函数 (由调用**OnReleaseHardware**中*device.cpp*文件) 查找以下代码：
   ```cpp
   // Delete lock
   WdfObjectDelete(m_I2CWaitLock);
   m_I2CWaitLock = NULL;
   ```

前面的代码用于删除的设备对象上的等待锁。

2. 找到以下代码，用于删除传感器实例：
   ```cpp
   // Delete sensor instance
   WdfObjectDelete(m_SensorInstance);
   ```

3. 关闭*client.cpp*文件。







