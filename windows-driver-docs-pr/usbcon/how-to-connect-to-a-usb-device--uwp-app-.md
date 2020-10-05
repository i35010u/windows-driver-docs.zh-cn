---
description: 在 Windows 8.1 中，可以编写与 USB 设备交互的 UWP 应用。
title: 如何连接到 USB 设备（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ea6c056698eae0c41603df6268fdeb5d62de7dd
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733609"
---
# <a name="how-to-connect-to-a-usb-device-uwp-app"></a>如何连接到 USB 设备（UWP 应用）


**摘要**

-   如何使用 [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) 对象来检测设备
-   如何打开设备进行通信
-   如何在使用完设备后关闭设备

**重要的 API**

-   [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice)
-   [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)

当你编写与 USB 设备交互的 UWP 应用时，该应用可以发送控制命令、获取设备信息，以及在大容量和中断终结点之间读取和写入数据。 在执行所有这些操作之前，必须找到设备并建立连接。

## <a name="before-you-start"></a>开始之前...


-   这是一个系列中的第一个主题。 开始本教程之前，必须已创建一个可在本教程中扩展的基本 Visual Studio 项目。 有关详细信息，请阅读 [UWP 应用](/windows/uwp/get-started/) 入门。
-   代码示例基于 CustomUsbDeviceAccess 示例。 您可以从此代码库页下载完整的示例。
-   本教程中使用的 USB 设备是 SuperMUTT 设备。
-   为了使用 [**windows. u**](/uwp/api/Windows.Devices.Usb) 命名空间来编写与 Usb 设备交互的 windows 应用程序，设备必须将 Winusb.sys 驱动程序加载为其函数驱动程序。 Winusb.sys 由 Microsoft 提供，并包含在** \\ windows \\ System32 \\ 驱动程序**文件夹中的 windows 中。

## <a name="flowchart-finding-the-device"></a>流程图：查找设备


若要连接到 USB 设备，你必须首先根据各种发现模式查找设备，然后连接到该设备：

-   使用特定设备接口 GUID 连接到任何 USB 设备。
-   使用特定的供应商 ID 和产品 ID 连接到 USB 设备，该设备具有特定的设备接口 GUID。
-   使用特定供应商 ID 和产品 ID 连接到 USB 设备，而无需知道设备接口 GUID。
-   连接到具有已知设备类的 USB 设备。

![usb 设备发现](images/scenario1-flowchart.png)

## <a name="key-concepts"></a>关键概念


**什么是设备接口 GUID？**

内核模型驱动程序在其初始化期间注册并公开名为 *设备接口 guid*的 guid。 通常，应用使用公开的 GUID 来查找关联的驱动程序及其设备，然后打开设备的句柄。 检索句柄用于后续的读取和写入操作。

但是，在 Winusb.sys 的情况下，它可以通过以下两种方式之一提供，而不是驱动程序公开设备接口 GUID：

-   在设备的 MS OS 描述符中。 设备制造商将 **DeviceInterfaceGUID** 设置为设备中扩展属性描述符中的自定义属性。 有关更多详细信息，请参阅 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10))中的 "扩展属性描述符" 文档。
-   如果通过自定义 INF 手动安装 Winusb.sys，则 INF 会在 INF 中注册一个 GUID。 请参阅 [WinUSB ( # A0) 安装](winusb-installation.md)。

如果找到设备的设备接口 GUID，则 UWP 应用可查找与该设备接口 GUID 匹配的所有设备。

**USB 设备标识在 Windows 中的显示方式是什么？**

每个 USB 设备都必须有两条信息：供应商 ID 和产品 ID。

USB-如果分配这些标识符，则设备制造商必须在设备中公开它们。 那么如何获取该信息呢？

-   即使设备没有加载设备驱动程序，即 Windows 将它检测为 "未知设备"，仍可以在 " **硬件 Id** " 属性值的设备管理器中查看标识符。 该值是这两个标识符的组合。 例如，对于 SuperMUTT 设备， **硬件 id** 为 "USB \\ VID \_ 045E&PID \_ F001"; 供应商 id 为 "0x045E"，产品 Id 为 "0xF001"。

-   如果设备有 INF，请从 " **模型** " 部分获取该字符串。
-   你可以检查各种注册表设置。 最简单的方法是查看

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ ControlSet001 \\ 枚举 \\ USB \\ &lt; 硬件 id&gt;**

    有关详细信息，请参阅 [USB 设备注册表项](usb-device-specific-registry-settings.md)。

-   应用程序清单使用硬件 ID 来标识设备。

    &lt;Device Id = "vidpid： 045e f001"&gt;

UWP 应用可查找与特定供应商和产品 id 匹配的所有设备。 可以通过指定设备接口 GUID 缩小搜索结果的范围。

**什么是 USB 设备类？**

大多数 USB 设备都符合 USB 批准的设备类规范。 通过使用这些规范，具有相似性质的设备可以采用标准方式展示其功能。 此方法的最大优点是设备可以使用 Microsoft 提供的内置类驱动程序或通用 Winusb.sys 驱动程序。

某些设备可能不遵循 USB IF 规范。 相反，它们会公开 *供应商定义的* 功能。 对于此类设备，供应商必须提供设备驱动程序，或者可以使用 Winusb.sys。

无论设备是供应商定义的还是符合设备类，它都必须描述此设备类相关的信息：

-   类代码：指示设备所属的设备类。
-   子类代码：在设备类中，表示设备的子类。
-   协议代码：设备使用的协议。

例如，SuperMUTT 设备是供应商定义的设备，并且类代码指示的信息是 FF。 如果你的设备以 FEh 形式显示类代码，将代码作为02h，并使用协议代码00h，你可以断定设备是符合类的 IrDA bridge 设备。
UWP 应用可与属于以下设备类的设备通信：

-   ActiveSync
-   CdcControl
-   DeviceFirmwareUpdate
-   IrDA
-   度量
-   PalmSync
-   PersonalHealthcare
-   物理
-   VendorSpecific

UWP 应用可查找匹配一组特定类、子类和协议代码的所有设备。

## <a name="get-the-advanced-query-syntax-aqs-string-for-the-device"></a>获取设备的高级查询语法 (AQS) 字符串


生成一个 (AQS) 的高级查询字符串，其中包含有关要检测的设备的标识信息。 可以通过指定供应商/产品 Id、设备接口 GUID 或设备类来生成字符串。

-   如果要提供供应商 ID/产品 ID 或设备接口 GUID，请调用 [**GetDeviceSelector**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_GetDeviceSelector_System_UInt32_System_UInt32_System_Guid_)的任何重载。

    在 SuperMUTT 设备的示例中， [**GetDeviceSelector**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_GetDeviceSelector_System_UInt32_System_UInt32_System_Guid_) 检索类似于以下字符串的 AQS 字符串：

    `"System.Devices.InterfaceClassGuid:="{DEE824EF-729B-4A0E-9C14-B7117D33A817}" AND System.Devices.InterfaceEnabled:=System.StructuredQueryType.Boolean#True AND System.DeviceInterface.WinUsb.UsbVendorId:=1118 AND System.DeviceInterface.WinUsb.UsbProductId:=61441"`

    **注意**   请注意，在字符串中出现的设备接口 GUID 不是您指定的 GUID。 此 GUID 是为 UWP 应用 Winusb.sys 注册的实际设备接口 GUID。

     

-   如果知道设备的设备类或它的类、子类和协议代码，请调用 [**GetDeviceClassSelector**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_GetDeviceClassSelector_Windows_Devices_Usb_UsbDeviceClass_) 生成 AQS 字符串。

    通过指定[**ClassCode**](/uwp/api/Windows.Devices.Usb.UsbDeviceClass#Windows_Devices_Usb_UsbDeviceClass_ClassCode)、 [**SubclassCode**](/uwp/api/Windows.Devices.Usb.UsbDeviceClass#Windows_Devices_Usb_UsbDeviceClass_SubclassCode)和[**ProtocolCode**](/uwp/api/Windows.Devices.Usb.UsbDeviceClass#Windows_Devices_Usb_UsbDeviceClass_ProtocolCode)属性值创建[**UsbDeviceClass**](/uwp/api/Windows.Devices.Usb.UsbDeviceClass)对象。 或者，如果知道设备的设备类，可以通过指定特定的 [**UsbDeviceClasses**](/uwp/api/Windows.Devices.Usb.UsbDeviceClasses) 属性来调用构造函数。

## <a name="finding-the-devicethe-basic-way"></a>查找设备-基本方法


这是查找 USB 设备的最简单方法。 有关详细信息，请参阅 [快速入门：枚举常用设备](/previous-versions/windows/apps/hh872189(v=win.10))。

1.  将检索到的 AQS 字符串传递到 [**FindAllAsync**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_FindAllAsync_System_String_)。 调用会检索 [**DeviceInformationCollection**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationCollection) 对象。
2.  遍历集合。 每个迭代都将获取一个 [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) 对象。
3.  获取 [**DeviceInformation.Id**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_Id) 属性值。 该字符串值为设备实例路径。 例如，" \\ \\ \\ \\ \\ ？ \\USB \# VID \_ 045E&PID \_ 078F \# 6&1b8ff026&0&5 \# {dee824ef-729b-4a0e-9c14-b7117d33a817} "。
4.  通过传递设备实例字符串并获取[**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice)对象来调用[**FromIdAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_FromIdAsync_System_String_) 。 然后，可以使用 **UsbDevice** 对象来执行其他操作，如发送控件传输。 当应用程序完成使用 **UsbDevice** 对象时，应用程序必须通过调用 [**Close**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)将其释放。
    **注意**   当 UWP 应用挂起时，设备将自动关闭。 若要避免使用陈旧的句柄来执行将来的操作，应用程序必须发布 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 引用。

     

```CSharp
    private async void OpenDevice()
    {
        UInt32 vid = 0x045E;
        UInt32 pid = 0x0611;

        string aqs = UsbDevice.GetDeviceSelector(vid, pid);

        var myDevices = await Windows.Devices.Enumeration.DeviceInformation.FindAllAsync(aqs);

        try
        {
            usbDevice = await UsbDevice.FromIdAsync(myDevices[0].Id);
        }
        catch (Exception exception)
        {
            ShowStatus(exception.Message.ToString());
        }
        finally        
        {
            ShowStatus("Opened device for communication.");
        }

    }
```

## <a name="find-the-deviceusing-devicewatcher"></a>查找设备-使用 DeviceWatcher


或者，可以动态枚举设备。 然后，如果添加或删除设备，或者设备属性更改，你的应用程序会收到通知。 有关详细信息，请参阅 [如何在添加、删除或更改设备时获取通知](/previous-versions/windows/apps/hh967756(v=win.10))。

使用 [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) 对象，应用可以在设备添加到系统或从系统中删除时动态检测设备。

1.  创建一个 [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) 对象，以检测何时将设备添加到系统或从系统中删除设备。 必须通过调用 [**CreateWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_CreateWatcher) 并指定 AQS 字符串来创建对象。
2.  实现并注册[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)对象上[**添加**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher#Windows_Devices_Enumeration_DeviceWatcher_Added)和[**移除**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher#Windows_Devices_Enumeration_DeviceWatcher_Removed)事件的处理程序。 当在系统中添加或删除 (具有相同标识信息) 的设备时，将调用这些事件处理程序。
3.  启动和停止 [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) 对象。

    应用必须通过调用[**start**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher#Windows_Devices_Enumeration_DeviceWatcher_Start)启动[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)对象，以便在设备添加或删除系统时可以开始检测设备。 相反，如果不再需要检测设备，应用程序必须通过调用[**stop**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher#Windows_Devices_Enumeration_DeviceWatcher_Stop)来停止**DeviceWatcher** 。 该示例有两个按钮，使用户可以启动和停止 **DeviceWatcher**。

此代码示例演示如何创建和启动设备观察程序，以便查找 SuperMUTT 设备的实例。

```CSharp
void CreateSuperMuttDeviceWatcher(void)
{
    UInt32 vid = 0x045E;
    UInt32 pid = 0x0611;

    string aqs = UsbDevice.GetDeviceSelector(vid, pid);  
    
    var superMuttWatcher = DeviceInformation.CreateWatcher(aqs);
  
    superMuttWatcher.Added += new TypedEventHandler<DeviceWatcher, DeviceInformation>
                              (this.OnDeviceAdded);

    superMuttWatcher.Removed += new TypedEventHandler<DeviceWatcher, DeviceInformationUpdate>
                            (this.OnDeviceRemoved);

    superMuttWatcher.Start();
 }
```

## <a name="open-the-device"></a>打开设备


若要打开设备，应用必须通过调用静态方法 [**FromIdAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_FromIdAsync_System_String_) 并传递) 从 [**DeviceInformation.Id**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_Id) 获取的设备实例 (路径来启动异步操作。 此操作的结果是一个 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象，用于将来与设备进行通信，例如执行数据传输。

使用完 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象后，必须将其释放。 通过释放对象，会取消所有挂起的数据传输。 仍会通过取消的错误或操作完成调用这些操作的完成回调例程。

C + + 应用程序必须使用 **delete** 关键字发布引用。 C #/VB 应用程序必须调用 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Dispose) 方法。 JavaScript 应用程序必须调用 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)。

如果设备正在使用或找不到， [**FromIdAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_FromIdAsync_System_String_) 将失败。

