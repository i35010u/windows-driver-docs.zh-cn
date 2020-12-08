---
title: 连接到硬件
description: 本主题演示传感器驱动程序如何确定分配的硬件资源并连接到 I2C 驱动程序控制器。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: babcdb807ddf1ab7c1d68f1eb924bf2c095416d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812361"
---
# <a name="connect-to-hardware"></a>连接到硬件


本主题演示传感器驱动程序如何确定分配的硬件资源，然后连接到 I2C 驱动程序控制器以便它能够连接到 ADXL345 硬件。

以下各节将使用为 ADXL345 加速感应器开发的示例驱动程序中的代码片段，作为显示如何使传感器驱动程序连接到硬件的测试用例。 如果尚未执行此操作，请导航到 GitHub 上的 [ADXL345Acc 示例](https://github.com/Microsoft/Windows-driver-samples/tree/1fbea08887e10e087c3f6bb0be8968e29e20cc84/sensors/ADXL345Acc) ，以便可以按照说明进行操作。

这些代码段突出显示了传感器驱动程序文件的一些重要部分。 但您必须完全查看所有驱动程序文件，才能充分了解驱动程序的工作原理，并能够确定如何为传感器自定义这些文件。

## <a name="prepare-hardware-resources"></a>准备硬件资源


1. 单击要打开的 *设备 .cpp* 文件，然后找到 **OnPrepareHardware** 函数。 在该函数中，查找以下代码：
   ```cpp
   // Create WDFOBJECT for the sensor
    WDF_OBJECT_ATTRIBUTES sensorAttributes;
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&sensorAttributes, ADXL345AccDevice);
   ```

上面的代码创建一个传感器对象，并为其分配相应的设备上下文。

2. 找到以下代码：
   ```cpp
   // Register sensor instance with clx
    SENSOROBJECT SensorInstance = NULL;
    NTSTATUS Status = SensorsCxSensorCreate(Device, &sensorAttributes, &SensorInstance);
   ```

前面的代码将向传感器类扩展注册传感器实例。 将创建一个传感器实例而不是一个设备实例，以允许在同一芯片中具有多个传感器的方案。

3. 找到以下代码：
   ```cpp
   // Initialize sensor instance with clx
    SENSOR_CONFIG SensorConfig;
    SENSOR_CONFIG_INIT(&SensorConfig);
    SensorConfig.pEnumerationList = pAccDevice->m_pEnumerationProperties;
    Status = SensorsCxSensorInitialize(SensorInstance, &SensorConfig);
   ```

前面的代码使用传感器类扩展来初始化传感器实例。

4. 找到以下代码：
   ```cpp
   Status = pAccDevice->ConfigureIoTarget(ResourcesRaw, ResourcesTranslated);
   ```

前面的代码为传感器驱动程序配置 i/o 目标对象。 I/o target 对象使传感器驱动程序能够与其他驱动程序通信。

## <a name="configure-the-device-with-default-settings"></a>用默认设置配置设备


请记住，D0 是设备的活动状态。 若要将设备置于 D0 状态，需要在设备本身的寄存器中设置此配置，并通过 I2C 与设备进行通信。 在执行写入或读取之前，必须持有此资源的锁定。

在 *设备 .cpp* 文件中，找到 **OnD0Entry** 函数，并注意它将调用 **PowerOn**，并使用 ADXL345 上下文来完成设备的打开工作。 在 **PowerOn** 函数中，查找以下代码：
1.
```cpp
WdfWaitLockAcquire(m_I2CWaitLock, NULL);
```

前面的代码用于获取 I2C 总线的锁定。

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

For 循环用于将默认配置设置写入设备寄存器。

3. 找到以下代码：
   ```cpp
   // Release the I2C bus lock
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);

   InitPropVariantFromUInt32(SensorState_Idle, &(m_pSensorProperties->List[SENSOR_PROPERTY_STATE].Value));
   m_PoweredOn = true;
   ```

成功配置设备后，WdfWaitLockRelease 将用于释放 I2C 总线的锁定。

4. 关闭 *设备 .cpp* 文件。
   ## <a name="start-the-device-activity"></a>启动设备活动


5. 单击 *客户端 .cpp* 文件以将其打开，并找到 **OnStart** 函数。
6. 查看以下用于在传感器设备上获取锁定的代码：
   ```cpp
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   ```

7. 找到以下代码：
   ```cpp
   // Set accelerometer to measurement mode
   REGISTER_SETTING RegisterSetting = { ADXL345_POWER_CTL, ADXL345_POWER_CTL_MEASURE };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

在前面的代码中，使用 I2C 连接将加速感应器设置为 *度量模式* ，使其可供读取传感器值。 请参阅 *adxl345* 头文件，了解 adxl345 power ctl 的定义 \_ \_ 、adxl345 \_ power \_ ctl \_ 度量值以及示例传感器驱动程序中使用的其他一些常量。

4. 找到以下代码：
   ```cpp
   // Enable interrupts
   RegisterSetting = { ADXL345_INT_ENABLE, ADXL345_INT_ACTIVITY };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   WdfWaitLockRelease(pAccDevice->m_I2CWaitLock);
   ```

*RegisterSetting* 参数启用传感器的中断。 WdfWaitLockRelease 用于释放 I2C 总线上的锁。

## <a name="stop-the-device-activity-and-set-device-to-standby"></a>停止设备活动并将设备设置为待机


1. 在 *客户端 .cpp* 文件中，在 **OnStop** 函数中找到以下代码：
   ```cpp
   // Disable interrupts
   REGISTER_SETTING RegisterSetting = { ADXL345_INT_ENABLE, 0 };
   WdfWaitLockAcquire(pAccDevice->m_I2CWaitLock, NULL);
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

在上面的代码中， *RegisterSetting* 参数捕获寄存器地址和配置代码。 在这种情况下，RegisterSetting 是中断启用注册的地址，而 RegisterSetting 则配置注册以停止设备发出中断。

2. 找到以下代码，此代码将清除可能仍处于挂起状态的设备的所有未处理的中断：
   ```cpp
   // Clear any stale interrupts
   RegisterSetting = { ADXL345_INT_SOURCE, 0 };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

3. 找到以下用于将设备设置为备用模式的代码。 此设置停止设备活动：
   ```cpp
   // Set accelerometer to standby
   RegisterSetting = { ADXL345_POWER_CTL, ADXL345_POWER_CTL_STANDBY };
   Status = I2CSensorWriteRegister(pAccDevice->m_I2CIoTarget, RegisterSetting.Register, &RegisterSetting.Value, sizeof(RegisterSetting.Value));
   ```

## <a name="disconnect-hardware-resources"></a>断开硬件资源连接


请注意，框架使用 **OnReleaseHardware** 函数来断开硬件资源的响应，以响应 i/o 请求数据包 (IRP) ，以停止或删除设备。

1. 在 *客户端 .cpp* 文件中，在 **DeInit** 函数中，在 OnReleaseHardware *文件中* 由 **OnReleaseHardware** 调用 () 查找以下代码：
   ```cpp
   // Delete lock
   WdfObjectDelete(m_I2CWaitLock);
   m_I2CWaitLock = NULL;
   ```

前面的代码用于删除设备对象上的等待锁。

2. 找到以下用于删除传感器实例的代码：
   ```cpp
   // Delete sensor instance
   WdfObjectDelete(m_SensorInstance);
   ```

3. 关闭 *客户端 .cpp* 文件。







