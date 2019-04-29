---
title: 将 KMDF 外设驱动程序连接到串行端口
description: 外围设备 SerCx2 托管的串行端口上的 KMDF 驱动程序需要特定硬件资源操作设备。 这些资源中包含的是该驱动程序必须打开的逻辑连接到串行端口的信息。
ms.assetid: EDE62C5E-3563-42EE-884E-DF473CD724A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f57862d4c09e57d3c92c30ce9640b2a7b1dcfddc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324233"
---
# <a name="connecting-a-kmdf-peripheral-driver-to-a-serial-port"></a>将 KMDF 外设驱动程序连接到串行端口


外围设备 SerCx2 托管的串行端口上的 KMDF 驱动程序需要特定硬件资源操作设备。 这些资源中包含的是该驱动程序必须打开的逻辑连接到串行端口的信息。 其他资源可能包括中断，以及一个或多个 GPIO 输入或输出插针。

此驱动程序实现了一组插和电源管理事件回调函数。 若要注册这些函数与 KMDF，驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)事件回调函数调用[ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546135)方法。 框架在调用电源管理事件回调函数来通知中的外围设备电源状态更改的驱动程序。 包含在这些函数是[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)函数，用于执行使该设备驱动程序可以访问所需的任何操作。

按顺序连接的外围设备进入未初始化的 D0 设备电源状态后，驱动程序框架将调用*EvtDevicePrepareHardware*函数以告知要准备用于设备的外围设备驱动程序。 在此调用，驱动程序将收到硬件资源的两个的列表作为输入参数。 *ResourcesRaw*参数是 WDFCMRESLIST 对象句柄的列表[*原始资源*](https://msdn.microsoft.com/library/windows/hardware/ff544561)，以及*ResourcesTranslated*参数是 WDFCMRESLIST 对象句柄的列表[*资源转换*](https://msdn.microsoft.com/library/windows/hardware/ff544561)。 翻译后的资源包括*连接 ID*驱动程序需要以建立与外围设备的逻辑连接。

下面的代码示例演示如何*EvtDevicePrepareHardware*函数可获取的连接 ID *ResourcesTranslated*参数。

```cpp
BOOLEAN fConnectionIdFound = FALSE;
LARGE_INTEGER connectionId = 0;
ULONG resourceCount;
NTSTATUS status = STATUS_SUCCESS;

resourceCount = WdfCmResourceListGetCount(ResourcesTranslated);

// Loop through the resources and save the relevant ones.

for (ULONG ix = 0; ix < resourceCount; ix++)
{
    PCM_PARTIAL_RESOURCE_DESCRIPTOR pDescriptor;

    pDescriptor = WdfCmResourceListGetDescriptor(ResourcesTranslated, ix);

    if (pDescriptor == NULL)
    {
        status = E_POINTER;
        break;
    }

    // Determine the resource type.
    switch (pDescriptor->Type)
    {
    case CmResourceTypeConnection:
        {
            // Check against the expected connection types.

            UCHAR Class = pDescriptor->u.Connection.Class;
            UCHAR Type = pDescriptor->u.Connection.Type;

            if (Class == CM_RESOURCE_CONNECTION_CLASS_SERIAL)
            {
                if (Type == CM_RESOURCE_CONNECTION_TYPE_SERIAL_UART)
                {
                    if (fConnectionIdFound == FALSE)
                    {
                        // Save the connection ID.

                        connectionId.LowPart = pDescriptor->u.Connection.IdLowPart;
                        connectionId.HighPart = pDescriptor->u.Connection.IdHighPart;
                        fConnectionIdFound = TRUE;
                    }
                }
            }

            if (Class == CM_RESOURCE_CONNECTION_CLASS_GPIO)
            {
                // Check for GPIO pin resource.
                ...
            }
        }
        break;

    case CmResourceTypeInterrupt:
        {
            // Check for interrupt resource.
            ...
        }
        break;

    default:
        // Don't care about other resource descriptors.
        break;
    }
}
```

前面的代码示例将按顺序连接的外围设备的连接 ID 复制到一个名为变量`connectionId`。

下面的代码示例演示如何将此连接 ID 合并到可用于打开到外围设备的逻辑连接的设备路径名称。 此设备路径名称作为系统组件，从中获取访问外围设备所需的参数标识的资源中心。

```cpp
// Use the connection ID to create the full device path name.
 
DECLARE_UNICODE_STRING_SIZE(szDeviceName, RESOURCE_HUB_PATH_SIZE);

status = RESOURCE_HUB_CREATE_PATH_FROM_ID(&szDeviceName,
                                          connectionId.LowPart,
                                          connectionId.HighPart);

if (!NT_SUCCESS(status))
{
     // Error handling
     ...
}
```

在前面的代码示例中， **DECLARE\_UNICODE\_字符串\_大小**宏创建的一个初始化声明[ **UNICODE\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff564879)名为变量`szDeviceName`具有缓冲区足够大以包含资源中心使用的格式中的设备路径名称。 Ntdef.h 标头文件中定义此宏。 **资源\_中心\_路径\_大小**常量设备路径名称中指定的字节数。 **资源\_中心\_创建\_路径\_FROM\_ID**宏生成的设备路径名称从连接 id。 **资源\_集线器\_路径\_大小**并**资源\_中心\_创建\_路径\_FROM\_ID**是Reshub.h 标头文件中定义。

下面的代码示例使用的设备路径名称来打开文件句柄 (名为`SerialIoTarget`) 到串行连接的外围设备。

```cpp
// Open the peripheral device on the serial port as a remote I/O target.
 
WDF_IO_TARGET_OPEN_PARAMS openParams;
WDF_IO_TARGET_OPEN_PARAMS_INIT_OPEN_BY_NAME(&openParams,
                                            &szDeviceName,
                                            (GENERIC_READ | GENERIC_WRITE));

openParams.ShareAccess = 0;
openParams.CreateDisposition = FILE_OPEN;
openParams.FileAttributes = FILE_ATTRIBUTE_NORMAL;

status = WdfIoTargetOpen(SerialIoTarget, &openParams);

if (!NT_SUCCESS(status))
{
    // Error handling
    ...
}
```

在前面的代码示例中， [ **WDF\_IO\_目标\_打开\_PARAMS\_INIT\_打开\_BY\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff552381)函数初始化[ **WDF\_IO\_目标\_打开\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552377)结构，以便可以打开该驱动程序与通过指定设备的名称按顺序连接的外围设备的逻辑连接。 `SerialIoTarget`变量是 framework I/O 目标对象的 WDFIOTARGET 句柄。 此句柄已获取从上次调用[ **WdfIoTargetCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548591)方法，而不会显示在示例中。 如果在调用[ **WdfIoTargetOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff548634)方法成功，驱动程序可以使用`SerialIoTarget`句柄将 I/O 请求发送到外围设备。

在中*EvtDriverDeviceAdd*事件回调函数，可以调用外围设备驱动程序[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)方法，以供分配一个框架请求对象驱动程序。 随后，当不再需要对象时，该驱动程序将调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)方法来删除该对象。 该驱动程序可以重复使用从获取 framework request 对象**WdfRequestCreate**多次调用将 I/O 请求发送到外围设备。 若要以同步方式发送读取、 写入或 IOCTL 请求，该驱动程序调用[ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)， [ **WdfIoTargetSendWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548672)，或[ **WdfIoTargetSendIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548660)方法。

在下面的代码示例，该驱动程序将调用**WdfIoTargetSendWriteSynchronously**若要以同步方式发送[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)对外围设备的请求。 在此示例中，开头`pBuffer`变量指向包含要写入到外围设备的数据的非分页缓冲区和`dataSize`变量指定的大小，以字节为单位，此类数据。

```cpp
ULONG_PTR bytesWritten;
NTSTATUS status;

// Describe the input buffer.

WDF_MEMORY_DESCRIPTOR memoryDescriptor;
WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&memoryDescriptor, pBuffer, dataSize);

// Configure the write request to time out after 2 seconds.

WDF_REQUEST_SEND_OPTIONS requestOptions;
WDF_REQUEST_SEND_OPTIONS_INIT(&requestOptions, WDF_REQUEST_SEND_OPTION_TIMEOUT);
requestOptions.Timeout = WDF_REL_TIMEOUT_IN_SEC(2);

// Send the write request synchronously.

status = WdfIoTargetSendWriteSynchronously(SerialIoTarget,
                                           SerialRequest,
                                           &memoryDescriptor,
                                           NULL,
                                           &requestOptions,
                                           &bytesWritten);
if (!NT_SUCCESS(status))
{
    // Error handling
    ...
}
```

前面的代码示例将执行以下操作：

1.  [ **WDF\_内存\_描述符\_INIT\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552393)函数调用初始化`memoryDescriptor`变量，这是[ **WDF\_内存\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff552392)描述输入的缓冲区的结构。 以前，该驱动程序调用例程如[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)无法分配从非分页缓冲池的缓冲区和写入数据复制到此缓冲区。
2.  [ **WDF\_请求\_发送\_选项\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552497)函数调用初始化`requestOptions`变量，这是[ **WDF\_请求\_发送\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff552491)结构，其中包含写入请求的可选设置。 在此示例中，结构配置对超时的请求，如果它不会在两秒后完成。
3.  在调用**WdfIoTargetSendWriteSynchronously**方法将写入请求发送到外围设备。 该方法以同步方式，返回后写入操作完成或超时。如有必要，可以调用另一个驱动程序线程[ **WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941)取消请求。

在中**WdfIoTargetSendWriteSynchronously**调用，该驱动程序提供了一个名为变量`SerialRequest`，这是以前创建的驱动程序框架请求对象的句柄。 之后**WdfIoTargetSendWriteSynchronously**调用时，通常应调用该驱动程序[ **WdfRequestReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff550026)方法以准备 framework 请求对象为再次使用。

 

 




