---
Description: 在 Windows 8.1，可以编写与 USB 设备进行交互的 UWP 应用。
title: 如何连接到 USB 设备（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5eca6881309b15cda4619af2df05e708a826aa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364822"
---
# <a name="how-to-connect-to-a-usb-device-uwp-app"></a>如何连接到 USB 设备（UWP 应用）


**摘要**

-   如何使用[ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)对象以检测设备
-   如何打开用于通信的设备
-   如何使用它完成后关闭设备

**重要的 Api**

-   [**UsbDevice**](https://msdn.microsoft.com/library/windows/apps/dn263883)
-   [**DeviceWatcher**](https://msdn.microsoft.com/library/windows/apps/br225446)

在编写与 USB 设备进行交互的 UWP 应用时，应用可以发送控制命令，获取设备信息和读取和写入数据传入/传出大容量和中断终结点。 您可以执行所有这些之前，必须找到设备，并建立连接。

## <a name="before-you-start"></a>开始之前...


-   这是一系列的第一个主题。 在开始本教程之前，您必须创建一个基本的 Visual Studio 项目，您可以充分利用本教程中。 读取[UWP 应用入门](https://go.microsoft.com/fwlink/p/?linkid=617681)的详细信息。
-   代码示例基于 CustomUsbDeviceAccess 示例。 您可以从该页的代码库下载完整的示例。
-   在教程中使用的 USB 设备是 SuperMUTT 设备。
-   若要使用[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)命名空间编写与 USB 设备，设备进行交互的 Windows 应用程序必须具有作为其功能驱动程序加载 Winusb.sys 驱动程序。 Winusb.sys 由 Microsoft 提供且包含在 Windows  **\\Windows\\System32\\驱动程序**文件夹。

## <a name="flowchart-finding-the-device"></a>流程图：查找设备


若要连接到 USB 设备，必须首先找到基于各种发现模式的设备并与其进行连接：

-   连接到特定设备接口的 GUID 与任何 USB 设备。
-   供应商 ID 和产品 ID 与特定连接到 USB 设备并具有特定设备接口的 GUID。
-   连接到 USB 设备与特定供应商 ID 和产品 ID 而不必知道设备接口的 GUID。
-   连接到已知设备类的 USB 设备。

![usb 设备发现](images/scenario1-flowchart.png)

## <a name="key-concepts"></a>重要概念


**什么是设备接口的 GUID？**

内核模式驱动程序，在其初始化、 注册和公开 GUID 调用期间*设备接口的 GUID*。 通常情况下，该应用使用公开的 GUID 查找关联的驱动程序和其设备，然后打开到设备的句柄。 检索到的句柄用于后续的读取和写入操作。

但是，对于 Winusb.sys，而不是驱动程序公开设备接口的 GUID，它可以提供两种方法之一：

-   在设备的 MS OS 描述符。 设备制造商集**DeviceInterfaceGUID**中设备的扩展的属性描述符中的自定义属性。 有关更多详细信息，请参阅中的"扩展属性描述符"文档[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=617682)。
-   如果您安装了自定义 INF 通过手动 Winusb.sys，INF 在 INF 中注册一个 GUID。 请参阅[WinUSB (Winusb.sys) 安装](winusb-installation.md)。

如果找到设备，则发现 GUID 设备接口，UWP 应用可以找到与该设备接口的 GUID 相匹配的所有设备。

**如何在 Windows 中显示 USB 设备标识？**

每个 USB 设备必须包含两个相关的信息： 供应商 ID 和产品 id。

USB-如果将这些标识符和设备制造商必须将它们显示在该设备。 你可以那么，如何获得该信息？

-   即使设备没有加载设备驱动程序，即 Windows 检测到它为"未知设备"，你仍然可以查看标识符在设备管理器中**硬件 Id**属性值。 该值是这些两个标识符的组合。 例如，对于 SuperMUTT 设备**硬件 Id**是"USB\\VID\_045E & PID\_F001"; 供应商 id 为"0x045E"，产品 id 为"0xF001"。

-   如果设备 INF，获取从该字符串**模型**部分。
-   您可以检查各种注册表设置。 最简单方法是请参阅

    **HKEY\_本地\_MACHINE\\系统\\ControlSet001\\枚举\\USB\\&lt;硬件 id&gt;**

    有关详细信息，请参阅[USB 设备注册表条目](usb-device-specific-registry-settings.md)。

-   应用程序清单使用硬件 ID 来标识设备。

    &lt;Device Id="vidpid:045e f001"&gt;

UWP 应用可以查找与特定供应商和产品 id 匹配的所有设备。 可以通过指定设备接口的 GUID 来缩小搜索结果。

**USB 设备类有哪些？**

大多数 USB 设备符合批准的 USB 设备类规范-如果。 通过使用这些规范，性质类似的设备可能会表现出它们的功能以标准方式。 此方法的最大优点是设备可以使用 Microsoft 提供的内置类驱动程序或通用 Winusb.sys 驱动程序。

某些设备可能不遵循 USB-如果规范。 相反，它们公开*供应商定义*功能。 对于此类设备供应商必须提供设备驱动程序，或者可以使用 Winusb.sys。

是否在设备供应商定义或符合的设备类，它必须描述此设备类的相关信息：

-   类代码：指示设备所属的设备类。
-   子类代码：在设备类中，指示设备的子类。
-   协议代码：设备使用的协议。

例如，SuperMUTT 设备供应商定义的设备，信息将由类代码是 FF。 如果你的设备显示为 FEh、 02，作为子类代码和协议代码 00 h 类代码，您可以得出结论： 该设备是否类兼容的 IrDA 桥接设备。
UWP 应用可以与属于这些设备类的设备进行通信：

-   ActiveSync
-   CdcControl
-   DeviceFirmwareUpdate
-   IrDA
-   度量值
-   PalmSync
-   PersonalHealthcare
-   物理
-   VendorSpecific

UWP 应用可以找到匹配一组特定的类、 子类和协议代码的所有设备。

## <a name="get-the-advanced-query-syntax-aqs-string-for-the-device"></a>获取设备的高级查询语法 (AQS) 字符串


生成包含你想要检测的设备的标识信息的高级的查询字符串 (AQS)。 通过指定的供应商/产品 Id，设备接口的 GUID，或设备类，可以生成字符串。

-   如果你想要提供的供应商 ID/产品 ID 或设备接口的 GUID，则调用的任何重载[ **GetDeviceSelector**](https://msdn.microsoft.com/library/windows/apps/dn264022)。

    在示例中的 SuperMUTT 设备[ **GetDeviceSelector** ](https://msdn.microsoft.com/library/windows/apps/dn264022)检索与此字符串类似 AQS 字符串：

    `"System.Devices.InterfaceClassGuid:="{DEE824EF-729B-4A0E-9C14-B7117D33A817}" AND System.Devices.InterfaceEnabled:=System.StructuredQueryType.Boolean#True AND System.DeviceInterface.WinUsb.UsbVendorId:=1118 AND System.DeviceInterface.WinUsb.UsbProductId:=61441"`

    **请注意**  请注意设备接口在字符串中出现的 GUID 不是指定。 该 GUID 是实际的设备接口由 Winusb.sys 注册适用于 UWP 应用的 GUID。

     

-   如果您知道的设备或其类、 子类和协议代码的设备类，调用[ **GetDeviceClassSelector** ](https://msdn.microsoft.com/library/windows/apps/dn264013)生成 AQS 字符串。

    创建[ **UsbDeviceClass** ](https://msdn.microsoft.com/library/windows/apps/dn263894)对象指定[ **ClassCode**](https://msdn.microsoft.com/library/windows/apps/dn263948)， [ **SubclassCode**](https://msdn.microsoft.com/library/windows/apps/dn263956)，并[ **ProtocolCode** ](https://msdn.microsoft.com/library/windows/apps/dn263951)属性值。 或者，如果您知道该设备的设备类，则可以调用构造函数通过指定特定[ **UsbDeviceClasses** ](https://msdn.microsoft.com/library/windows/apps/dn263904)属性。

## <a name="finding-the-devicethe-basic-way"></a>查找设备 — 的基本方法


这是查找 USB 设备的最简单方法。 有关详细信息，请参阅[快速入门： 枚举通常使用设备](https://msdn.microsoft.com/library/windows/apps/xaml/hh872189)。

1.  检索到 AQS 将字符串传递给[ **FindAllAsync**](https://msdn.microsoft.com/library/windows/apps/br225432)。 该调用会检索[ **DeviceInformationCollection** ](https://msdn.microsoft.com/library/windows/apps/br225395)对象。
2.  循环访问集合。 每次迭代获取[ **DeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/br225393)对象。
3.  获取[ **DeviceInformation.Id** ](https://msdn.microsoft.com/library/windows/apps/br225437)属性值。 字符串值是设备实例路径。 例如，"\\\\\\\\？\\\\USB\#VID\_045E & PID\_078F\#6 1b8ff026 0 & 5\#{dee824ef-729b-4a0e-9c14-b7117d33a817}"。
4.  调用[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264010)通过设备实例字符串和 get [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象。 然后，可以使用**UsbDevice**对象来执行其他操作，例如发送控制传输。 当应用程序使用完**UsbDevice**对象，该应用程序必须将其释放通过调用[**关闭**](https://msdn.microsoft.com/library/windows/apps/dn263990)。
    **请注意**  时 UWP 应用程序挂起，设备会自动关闭。 若要避免使用过时的句柄用于将来的操作，该应用程序必须释放[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)引用。

     

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

## <a name="find-the-deviceusing-devicewatcher"></a>查找设备 — 使用 DeviceWatcher


或者，可以动态地枚举设备。 然后，您的应用程序可以接收通知，如果添加或删除，设备或设备属性更改。 有关详细信息，请参阅[如何获取通知，如果设备被添加、 移除或更改](https://msdn.microsoft.com/library/windows/apps/xaml/hh967756)。

一个[ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)对象，应用程序以添加用户以及他们获取从系统中删除动态检测设备。

1.  创建[ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)对象无法检测何时添加或从系统中删除设备。 您必须创建该对象通过调用[ **CreateWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225427)并指定 AQS 字符串。
2.  实现和注册的处理程序[ **Added** ](https://msdn.microsoft.com/library/windows/apps/br225450)并[**已删除**](https://msdn.microsoft.com/library/windows/apps/br225453)上的事件[ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)对象。 添加或从系统中删除 （具有相同的标识信息） 的设备时，将调用这些事件处理程序。
3.  启动和停止[ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)对象。

    应用必须启动[ **DeviceWatcher** ](https://msdn.microsoft.com/library/windows/apps/br225446)对象通过调用[**启动**](https://msdn.microsoft.com/library/windows/apps/br225454) ，以便它可以开始检测设备，因为当他们添加或从系统中删除。 相反，必须停止该应用程序**DeviceWatcher**通过调用[**停止**](https://msdn.microsoft.com/library/windows/apps/br225456)，当不再需要以检测设备时。 此示例具有两个按钮，使用户可以启动和停止**DeviceWatcher**。

此代码示例演示如何创建和启动设备观察程序要查找的 SuperMUTT 设备实例。

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


若要打开设备，应用必须启动异步操作通过调用静态方法[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264010)并传递设备实例路径 (从获取[ **DeviceInformation.Id**](https://msdn.microsoft.com/library/windows/apps/br225437))。 获取该操作的结果是[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象，用于将来的通信设备，如执行数据传输。

在完成后使用[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象，必须将其释放。 通过释放对象，则将取消所有挂起的数据传输。 仍以已取消的错误或操作已完成，调用这些操作的完成回调例程。

C++应用必须通过使用发布的引用**删除**关键字。 C#/VB 应用必须调用[ **UsbDevice.Dispose** ](https://msdn.microsoft.com/library/windows/apps/dn264007)方法。 JavaScript 应用程序必须调用[ **UsbDevice.Close**](https://msdn.microsoft.com/library/windows/apps/dn263990)。

[ **FromIdAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264010)失败，如果设备处于使用或找不到。

 

 




