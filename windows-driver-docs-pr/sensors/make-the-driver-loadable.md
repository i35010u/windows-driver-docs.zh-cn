---
title: 使驱动程序可加载
description: 若要使驱动程序可加载，必须添加将注册所需驱动程序回调例程 (DriverEntry) 的函数、 函数会将驱动程序连接到设备堆栈 (DeviceAdd) 和 （已不再需要时将卸载该驱动程序的函数DriverUnload)。
ms.assetid: 6BEB7CBC-0179-41B3-BD3D-126290940768
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 522791f3f858b57ea2ced94220ae02b6a944619b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542416"
---
# <a name="make-the-driver-loadable"></a>使驱动程序可加载


若要使驱动程序可加载，必须将添加将注册所需驱动程序回调例程的函数 (**DriverEntry**)，会将驱动程序连接到设备堆栈的函数 (**DeviceAdd**)，和一个当不再需要时将卸载该驱动程序的函数 (**DriverUnload**)。

以下各节将使用来自示例驱动程序开发的代码片段 ADXL345 加速感应器，为测试用例来显示如何使传感器驱动程序可加载。 如果尚未这样做，导航到[ADXL345Acc 示例](https://github.com/Microsoft/Windows-driver-samples/tree/1fbea08887e10e087c3f6bb0be8968e29e20cc84/sensors/ADXL345Acc)GitHub 上，以便你可以遵循说明。

这些代码段突出显示某些传感器驱动程序文件的重要部分。 但你必须查看整个，若要获取该驱动程序的工作原理，更好地理解并能够找出如何自定义这些文件可以获得您的传感器中的所有驱动程序文件。

## <a name="register-the-driver---driverentry"></a>注册驱动程序-DriverEntry


1. 单击此项可打开*driver.cpp*文件，然后查找块的代码开头 NTSTATUS DriverEntry。 **DriverEntry**函数的配置和初始化 DriverObject 注册传感器驱动程序。 此函数还可以通过使用 WPP 跟踪初始化日志记录。
2. 内**DriverEntry**，查找以下代码：
   ```cpp
   WPP_INIT_TRACING(DriverObject, NULL);
   ```

此代码将配置日志记录驱动程序。

3. 查找 WDF\_驱动程序\_CONFIG\_INIT 语句。 WDF\_驱动程序\_CONFIG\_INIT 函数调用来设置**DeviceAdd**回调。
   ```cpp
   WDF_DRIVER_CONFIG_INIT(&DriverConfig, ADXL345AccDevice::OnDeviceAdd);
   ```

4. 查找块的代码开头 NTSTATUS 状态 = WdfDriverCreate。
   ```cpp
   NTSTATUS Status = WdfDriverCreate(DriverObject, RegistryPath, WDF_NO_OBJECT_ATTRIBUTES, &DriverConfig, WDF_NO_HANDLE);
   ```

WdfDriverCreate 函数用于初始化的驱动程序对象。

5. 关闭*driver.cpp*文件。
   ## <a name="set-up-the-device-object---deviceadd"></a>设置设备对象-DeviceAdd


6. 单击此项可打开*device.cpp*文件，然后查找**OnDeviceAdd**函数。 此函数将驱动程序附加到设备堆栈，并分配到设备的每个设备上下文结构。 **OnDeviceAdd**现在成为了驱动程序在第二个调用期间通常会对其进行调用。 开发驱动程序还可能包括代码来处理即插即用、 电源管理和 I/O。
7. 找到以下代码：
   ```cpp
   // Create WDFOBJECT for the sensor
   WDF_OBJECT_ATTRIBUTES attributes;
   WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(WDFDRIVER Driver, &attributes, ADXL345AccDevice);
   ```

此代码设置类型 ADXL345AccDevice 设备对象的上下文结构。

3. 找到以下代码：
   ```cpp
   // Call the framework to create the device
   NTSTATUS Status = WdfDeviceCreate(&pAccDeviceInit, &FdoAttributes, &Device);
   ```

此函数用于创建 WDFDEVICE 对象。 WDF 创建设备对象，然后分配给它的 ADXL345 加速感应器上下文。

4. 关闭*device.cpp*文件。
   ## <a name="unload-the-driver---driverunload"></a>卸载驱动程序-DriverUnload


5. 单击此项可打开*driver.cpp*文件，并查找**OnDriverUnload**函数。 此函数用于 IO manager 卸载内存中的驱动程序后执行清理。
6. 找到以下代码：
   ```cpp
   WPP_CLEANUP(WdfDriverWdmGetDriverObject(Driver));
   ```

此代码将关闭 WPP 诊断跟踪。

 

 




