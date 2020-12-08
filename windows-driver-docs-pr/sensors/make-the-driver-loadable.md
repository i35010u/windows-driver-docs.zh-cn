---
title: 使驱动程序可加载
description: 若要使驱动程序可加载，你必须添加一个函数，该函数将注册所需的驱动程序回调例程 (DriverEntry) 、将驱动程序附加到设备堆栈的函数 (DeviceAdd) ，以及一个将在不再需要该驱动程序的情况下卸载该驱动程序 (DriverUnload) 的函数。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a19c08c9b9adba42950e85eb2238f0bc0c37b7f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812289"
---
# <a name="make-the-driver-loadable"></a>使驱动程序可加载


若要使驱动程序可加载，你必须添加一个函数，该函数将注册所需的驱动程序回调例程 (**DriverEntry**) 、将驱动程序附加到设备堆栈的函数 (**DeviceAdd**) ，以及一个将在不再需要该驱动程序的情况下卸载该驱动程序 (**DriverUnload**) 的函数。

以下各节将使用为 ADXL345 加速感应器开发的示例驱动程序中的代码片段，作为演示如何使传感器驱动程序可加载的测试用例。 如果尚未执行此操作，请导航到 GitHub 上的 [ADXL345Acc 示例](https://github.com/Microsoft/Windows-driver-samples/tree/1fbea08887e10e087c3f6bb0be8968e29e20cc84/sensors/ADXL345Acc) ，以便可以按照说明进行操作。

这些代码段突出显示了传感器驱动程序文件的一些重要部分。 但您必须完全查看所有驱动程序文件，才能充分了解驱动程序的工作原理，并能够确定如何为传感器自定义这些文件。

## <a name="register-the-driver---driverentry"></a>注册驱动程序-DriverEntry


1. 单击打开 *驱动程序 .cpp* 文件，然后查找以 NTSTATUS DriverEntry 开头的代码块。 **DriverEntry** 函数通过配置和初始化 DriverObject 来注册传感器驱动程序。 此函数还通过使用 WPP 跟踪来初始化日志记录。
2. 在 **DriverEntry** 中找到以下代码：
   ```cpp
   WPP_INIT_TRACING(DriverObject, NULL);
   ```

此代码配置驱动程序的日志记录。

3. 查找 WDF \_ 驱动程序 \_ CONFIG \_ INIT 语句。 调用 WDF \_ 驱动程序 \_ 配置 \_ INIT 函数以设置 **DeviceAdd** 回调。
   ```cpp
   WDF_DRIVER_CONFIG_INIT(&DriverConfig, ADXL345AccDevice::OnDeviceAdd);
   ```

4. 查找以 NTSTATUS Status = WdfDriverCreate 开头的代码块。
   ```cpp
   NTSTATUS Status = WdfDriverCreate(DriverObject, RegistryPath, WDF_NO_OBJECT_ATTRIBUTES, &DriverConfig, WDF_NO_HANDLE);
   ```

WdfDriverCreate 函数用于初始化驱动程序对象。

5. 关闭 *驱动程序 .cpp* 文件。
   ## <a name="set-up-the-device-object---deviceadd"></a>设置设备对象-DeviceAdd


6. 单击打开 *设备 .cpp* 文件，然后查找 **OnDeviceAdd** 函数。 此函数将驱动程序附加到设备堆栈，并向设备分配每个设备的上下文结构。 通常在对驱动程序进行的第二次调用期间调用 **OnDeviceAdd** 。 开发驱动程序时，还可以包括处理 PnP、电源管理和 i/o 的代码。
7. 找到以下代码：
   ```cpp
   // Create WDFOBJECT for the sensor
   WDF_OBJECT_ATTRIBUTES attributes;
   WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(WDFDRIVER Driver, &attributes, ADXL345AccDevice);
   ```

此代码为设备对象设置类型为 ADXL345AccDevice 的上下文结构。

3. 找到以下代码：
   ```cpp
   // Call the framework to create the device
   NTSTATUS Status = WdfDeviceCreate(&pAccDeviceInit, &FdoAttributes, &Device);
   ```

此函数用于创建 WDFDEVICE 对象。 WDF 创建设备对象，然后将 ADXL345 加速感应上下文分配给该对象。

4. 关闭 *设备 .cpp* 文件。
   ## <a name="unload-the-driver---driverunload"></a>卸载驱动程序-DriverUnload


5. 单击打开 *驱动程序 .cpp* 文件，查找 **OnDriverUnload** 函数。 此函数用于在 IO 管理器从内存中卸载驱动程序后执行清除。
6. 找到以下代码：
   ```cpp
   WPP_CLEANUP(WdfDriverWdmGetDriverObject(Driver));
   ```

此代码将关闭 WPP 诊断跟踪。

 

 




