---
Description: 若要编写与 USB 设备进行通信的 Windows 桌面应用的最简单方法是使用 C /C++ WinUSB 模板。
title: 编写基于 WinUSB 模板的 Windows 桌面应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 131dfe9091b70673b7eedaed314397bc52afb6de
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393415"
---
# <a name="write-a-windows-desktop-app-based-on-the-winusb-template"></a>编写基于 WinUSB 模板的 Windows 桌面应用


**重要的 API**

-   [安装程序 Api 函数](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)
-   [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)

若要编写与 USB 设备进行通信的 Windows 桌面应用的最简单方法是使用 C /C++ WinUSB 模板。 对于此模板中，您需要使用 Windows Driver Kit (WDK) （包含有关 Windows 调试工具) 和 Microsoft Visual Studio （专业版或旗舰版） 的集成的环境。 该模板可以用作起始点。

## <a name="prerequisites"></a>先决条件


-   若要设置集成的开发环境，首先安装 Microsoft Visual Studio Ultimate 2012 或 Microsoft Visual Studio Professional 2012，然后安装 WDK。 有关如何获取 Visual Studio 和 WDK 的信息，你可以在[此处](https://go.microsoft.com/fwlink/p/?linkid=239721)找到。
-   在安装 WDK 时，调试工具的 Windows 是包含。 有关详细信息，请参阅[下载和为 Windows 中安装调试的工具](https://go.microsoft.com/fwlink/p/?linkid=235427)。

## <a name="creating-a-winusb-application"></a>创建 WinUSB 应用程序


若要从模板创建应用程序：

1.  打开 Microsoft Visual Studio。 上**文件**菜单中，选择**新建** &gt; **项目**。 **新的项目**对话框将打开，如以下屏幕截图中所示。
2.  在中**新的项目**对话框中，在左窗格中，找到并选择**USB**。
3.  在中间窗格中，选择**WinUSB 应用程序。**
4.  在中**名称**字段中，如果你想要更改项目名称。 在本主题中，我们将使用默认名称。
5.  在**位置**字段中，输入要在其中创建新项目的目录。
6.  选中“创建解决方案的目录”  。 单击 **“确定”** 。

    ![visual studio 中的 winusb 模板](images/winusb-template.png)

    Visual Studio 将创建两个项目和解决方案。 您可以看到解决方案、 两个项目，以及属于每个项目中的文件**解决方案资源管理器**窗口中，如以下屏幕截图中所示。 （如果未显示“解决方案资源管理器”  窗口，请从“视图”   菜单中选择“解决方案资源管理器”。）该解决方案包含C++应用程序项目中名为 USB Application1 和驱动程序程序包项目名为 USB Application1 包。 如果你想要查看应用程序源代码，你可以打开任何下显示的文件**源文件**。

    ![winusb 模板解决方案资源管理器](images/winusb-template1.png)

    USB Application1 项目具有该应用程序的源代码文件。

    USB Application1 包项目包含用于安装设备驱动程序作为由 Microsoft 提供 Winusb.sys 驱动程序的 INF 文件。

7.  INF 文件，USBApplication1.inf 中, 找到这些行：

    `%DeviceName% =USB_Install, USB\VID_vvvv&PID_pppp`

8.  替换为 VID\_vvvv & PID\_pppp 与你的设备的硬件 ID。 从设备管理器中获取的硬件 ID。 在设备管理器中，查看设备属性。 上**详细信息**选项卡上，查看**硬件 Id**属性值。
9.  在**解决方案资源管理器**窗口中，右键单击**解决方案"USB 应用程序 1"（2 个项目）** ，然后选择**Configuration Manager**。 选择的配置和平台，用于应用程序项目和包项目。 在此练习中，我们选择 Win8.1 调试和 x64 上，如以下屏幕截图中所示。

    ![winusb 应用程序模板](images/winusb-template2.png)

## <a name="building-deploying-and-debugging-the-project"></a>构建、 部署和调试项目


到目前为止本练习中，您用过 Visual Studio 来生成项目。 接下来需要配置设备连接到设备。 该模板要求 Winusb 驱动程序作为你的设备的驱动程序安装。

你的测试和调试环境可以有：

-   两个计算机设置： 主机计算机和目标计算机。 在开发和主机计算机上生成 Visual Studio 中的项目。 调试程序在主机上运行并且位于 Visual Studio 用户界面中。 当测试和调试应用程序，该驱动程序在目标计算机上运行。

-   单个计算机设置：您的目标和一台计算机上运行的主机。 开发和生成你的项目在 Visual Studio 中，并运行调试器和应用程序。

可以部署、 安装、 加载和调试你的应用程序和驱动程序通过执行以下步骤：

-   **两个计算机设置**

    1.  按照中的说明预配目标计算机[预配的计算机的驱动程序部署和测试](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。
        **注意**  
        预配名为，在目标计算机 WDKRemoteUser 上创建的用户。 完成预配后将看到切换到 WDKRemoteUser 的用户。 
    2.  在主计算机上，在 Visual Studio 中打开你的解决方案。
    3.  Main.cpp 中添加此行 OpenDevice 调用之前。

        `system ("pause")`

        在行导致应用程序启动时暂停。 这可在远程调试。

    4.  在 pch.h 中，包含以下行：

        `#include <cstdlib>`

        这包括语句是所必需的上一步中 system （） 调用。

    5.  在中**解决方案资源管理器**窗口中，右键单击 USB Application1 包，然后选择**属性**。
    6.  在中**USB Application1 包属性页**窗口中的，在左窗格中，导航到**配置属性&gt;驱动程序安装&gt;部署**，如中所示下面的屏幕截图。
    7.  检查**启用部署**，并检查**删除以前的驱动程序版本部署前**。
    8.  对于**远程计算机名**，请选择配置用于测试和调试的计算机名。 在此练习中，我们使用名为 dbg 目标的计算机。
    9.  选择**安装并验证**。 单击 **“确定”** 。

        ![winusb 模板](images/winusb-template4.png)

    10. 在属性页中，导航到**配置属性&gt;调试**，然后选择**调试工具的 Windows-远程调试器**，如以下屏幕截图中所示。

        ![winusb 模板调试设置](images/winusb-template5.png)

    11. 选择**生成解决方案**从**生成**菜单。 Visual Studio 显示生成进度**输出**窗口。 （如果**输出**窗口不可见，则从**视图**菜单中选择**输出**。）在此练习中，我们已构建运行 Windows 8.1 的 x-64 系统的项目。

在目标计算机上，你将看到运行驱动程序安装脚本。 驱动程序文件复制到 %systemdrive%\\drivertest\\目标计算机上的驱动程序文件夹。 请确认 .inf、.cat、测试证书和 .sys 文件以及其他任何必要的文件均位于 %systemdrive%\\drivertest\\drivers 文件夹下。 设备必须出现在设备管理器中未出现错误。

在主计算机中，你会看到此消息中的**输出**窗口。

```syntax
Deploying driver files for project 
"<path>\visual studio 12\Projects\USB Application1\USB Application1 Package\USB Application1 Package.vcxproj".  
Deployment may take a few minutes...
========== Build: 1 succeeded, 0 failed, 1 up-to-date, 0 skipped ==========
```

**若要调试应用程序**

1.  在主计算机上导航到**x64 &gt; Win8.1Debug**解决方案文件夹中。
2.  复制应用程序可执行文件，UsbApplication1.exe 到目标计算机。
3.  在目标计算机上启动应用程序。
4.  主机计算机上，从**调试**菜单中，选择**附加到进程**。
5.  在窗口中，选择**Windows 用户模式调试器**(有关 Windows 调试工具) 作为传输协议和目标计算机的名称，在本例中，dbg 目标与限定符此图中所示。

    ![winusb 模板调试设置](images/winusb-template6.png)

6.  从列表中选择的应用程序**可用进程**然后单击**附加**。 你现在可以使用调试**即时窗口**或通过使用中的选项**调试**菜单。

前面的说明使用调试应用程序**调试工具的 Windows-远程调试器**。 如果你想要使用**远程 Windows 调试器**（包含在 Visual Studio 调试器），然后按照这些说明进行操作：

1.  在目标计算机上，将添加到允许通过防火墙的应用的列表的 msvsmon.exe。
2.  启动 Visual Studio 远程调试监视器位于 c:\\DriverTest\\msvsmon\\msvsmon.exe。
3.  创建工作文件夹，如 c:\\remotetemp。
4.  复制应用程序可执行文件，UsbApplication1.exe 到目标计算机上的工作文件夹。
5.  在主计算机，在 Visual Studio 中，右键单击**USB Application1 包**项目，并选择**卸载项目**。
6.  右键单击**USB Application1**项目中，在项目属性中，展开**配置属性**节点，然后单击**调试**。
7.  更改**要启动的调试器**到**远程 Windows 调试器**。
8.  更改项目设置以在远程计算机上运行可执行文件，按照中的说明[远程调试的项目生成本地](https://docs.microsoft.com/visualstudio/debugger/remote-debugging?view=vs-2015)。 请确保**工作目录**并**远程命令**属性反映在目标计算机上的文件夹。
9.  若要在调试应用程序中，**构建**菜单中，选择**开始调试**，或按**F5。**

-   **单个计算机设置：**

    1.  若要生成你的应用程序和驱动程序安装包，请选择**生成解决方案**从**生成**菜单。 Visual Studio 显示生成进度**输出**窗口中，如以下屏幕截图中所示。 （如果**输出**窗口不可见，则从**视图**菜单中选择**输出**。）在此练习中，我们已构建运行 Windows 8.1 的 x-64 系统的项目。
    2.  若要查看包中，导航到 USB Application1 文件夹，在 Windows 资源管理器，然后导航到生成的驱动程序**x64 &gt; Win8.1Debug &gt; USB Application1 包**。 驱动程序包包含多个文件：USBApplication1.inf 信息使用的文件，Windows 安装驱动程序时，usbapplication1.cat 是安装程序使用来验证测试签名驱动程序包的目录文件。 另一个文件是为 Windows 驱动程序框架 (WDF) 共同安装程序。 以下屏幕截图中显示这些文件。

        ![winusb 应用程序模板](images/winusb-template3.png)

        **请注意**包含在包中没有驱动程序文件。 这是因为 INF 文件引用的现成驱动程序，Winusb.sys，在 Windows 中找到\\System32 文件夹。
    3.  手动安装驱动程序。 在设备管理器中，通过在包中指定 INF 更新驱动程序。 点到驱动程序包位于解决方案文件夹中，在上一部分中所示。
    4.  右键单击**USB Application1**项目中，在项目属性中，展开**配置属性**节点，然后单击**调试**。
    5.  更改**要启动的调试器**到**本地 Windows 调试器**。
    6.  7.  右键单击 USB Application1 包项目，然后选择**卸载项目**。
    8.  若要在调试应用程序中，**构建**菜单中，选择**开始调试**，或按**F5**。

## <a name="template-code-discussion"></a>模板代码讨论


该模板是桌面应用程序的起始点。 USB Application1 项目具有源文件 device.cpp 和 main.cpp。

Main.cpp 文件包含应用程序入口点， \_tmain。 Device.cpp 包含打开和关闭到设备的句柄的所有帮助器函数。

该模板还具有一个名为 device.h 的标头文件。 此文件包含设备接口 （稍后讨论） 的 GUID 和设备定义\_数据结构，用于存储信息获取应用程序。 例如，它将存储 WinUSB 接口句柄通过 OpenDevice 获得并在后续操作中使用。

```cpp
typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];

} DEVICE_DATA, *PDEVICE_DATA;
```

### <a href="" id="deviceinstance"></a>获取实例路径设备-请参阅 RetrieveDevicePath 中 device.cpp

若要访问的 USB 设备，应用程序会创建该设备的有效的文件句柄通过调用**CreateFile**。 该调用时，应用程序必须获取设备路径实例。 若要获取设备路径，该应用使用[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)例程，并在用于安装 Winusb.sys 的 INF 文件中指定设备接口的 GUID。 Device.h 声明一个名为 GUID 的 GUID 常量\_DEVINTERFACE\_USBApplication1。 通过使用这些例程，该应用程序枚举中指定的设备接口类的所有设备，并检索设备的设备路径。

```cpp
HRESULT
RetrieveDevicePath(
    _Out_bytecap_(BufLen) LPTSTR DevicePath,
    _In_                  ULONG  BufLen,
    _Out_opt_             PBOOL  FailureDeviceNotFound
    )
/*++

Routine description:

    Retrieve the device path that can be used to open the WinUSB-based device.

    If multiple devices have the same device interface GUID, there is no
    guarantee of which one will be returned.

Arguments:

    DevicePath - On successful return, the path of the device (use with CreateFile).

    BufLen - The size of DevicePath's buffer, in bytes

    FailureDeviceNotFound - TRUE when failure is returned due to no devices
        found with the correct device interface (device not connected, driver
        not installed, or device is disabled in Device Manager); FALSE
        otherwise.

Return value:

    HRESULT

--*/
{
    BOOL                             bResult = FALSE;
    HDEVINFO                         deviceInfo;
    SP_DEVICE_INTERFACE_DATA         interfaceData;
    PSP_DEVICE_INTERFACE_DETAIL_DATA detailData = NULL;
    ULONG                            length;
    ULONG                            requiredLength=0;
    HRESULT                          hr;

    if (NULL != FailureDeviceNotFound) {

        *FailureDeviceNotFound = FALSE;
    }

    //
    // Enumerate all devices exposing the interface
    //
    deviceInfo = SetupDiGetClassDevs(&GUID_DEVINTERFACE_USBApplication1,
                                     NULL,
                                     NULL,
                                     DIGCF_PRESENT | DIGCF_DEVICEINTERFACE);

    if (deviceInfo == INVALID_HANDLE_VALUE) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        return hr;
    }

    interfaceData.cbSize = sizeof(SP_DEVICE_INTERFACE_DATA);

    //
    // Get the first interface (index 0) in the result set
    //
    bResult = SetupDiEnumDeviceInterfaces(deviceInfo,
                                          NULL,
                                          &GUID_DEVINTERFACE_USBApplication1,
                                          0,
                                          &interfaceData);

    if (FALSE == bResult) {

        //
        // We would see this error if no devices were found
        //
        if (ERROR_NO_MORE_ITEMS == GetLastError() &&
            NULL != FailureDeviceNotFound) {

            *FailureDeviceNotFound = TRUE;
        }

        hr = HRESULT_FROM_WIN32(GetLastError());
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    //
    // Get the size of the path string
    // We expect to get a failure with insufficient buffer
    //
    bResult = SetupDiGetDeviceInterfaceDetail(deviceInfo,
                                              &interfaceData,
                                              NULL,
                                              0,
                                              &requiredLength,
                                              NULL);

    if (FALSE == bResult && ERROR_INSUFFICIENT_BUFFER != GetLastError()) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    //
    // Allocate temporary space for SetupDi structure
    //
    detailData = (PSP_DEVICE_INTERFACE_DETAIL_DATA)
        LocalAlloc(LMEM_FIXED, requiredLength);

    if (NULL == detailData)
    {
        hr = E_OUTOFMEMORY;
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    detailData->cbSize = sizeof(SP_DEVICE_INTERFACE_DETAIL_DATA);
    length = requiredLength;

    //
    // Get the interface's path string
    //
    bResult = SetupDiGetDeviceInterfaceDetail(deviceInfo,
                                              &interfaceData,
                                              detailData,
                                              length,
                                              &requiredLength,
                                              NULL);

    if(FALSE == bResult)
    {
        hr = HRESULT_FROM_WIN32(GetLastError());
        LocalFree(detailData);
        SetupDiDestroyDeviceInfoList(deviceInfo);
        return hr;
    }

    //
    // Give path to the caller. SetupDiGetDeviceInterfaceDetail ensured
    // DevicePath is NULL-terminated.
    //
    hr = StringCbCopy(DevicePath,
                      BufLen,
                      detailData->DevicePath);

    LocalFree(detailData);
    SetupDiDestroyDeviceInfoList(deviceInfo);

    return hr;
}
```

在前面的函数中，应用程序通过调用这些例程来获取设备路径：

1.  [**SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)若要获取的句柄*设备的信息集*，一个数组，包含有关所有已安装的设备的匹配指定的设备接口类，GUID信息\_DEVINTERFACE\_USBApplication1。 数组中的每个元素调用*设备接口*对应于已安装并向系统注册的设备。 设备接口类表示通过设备接口的 INF 文件中定义的 GUID 标识。 该函数返回到设备的信息集 HDEVINFO 句柄。
2.  [**SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)枚举设备接口中的设备信息设置，并获取有关设备接口的信息。

    此调用需要以下各项：

    -   调用方分配一个初始化[ **SP\_设备\_接口\_数据**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)结构，它具有其**cbSize**成员设置为结构的大小。
    -   步骤 1 中 HDEVINFO 句柄。
    -   设备接口的 INF 文件中定义的 GUID。

    [**SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)查找设备接口的指定索引的设备信息设置数组和填充初始化[ **SP\_设备\_接口\_数据**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)具有有关接口的基本数据结构。

    **请注意**若要枚举设备的信息集中的所有设备接口，请调用[ **SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)中，直到函数返回一个循环**FALSE**和失败的错误代码是错误\_否\_详细\_项。 错误\_否\_详细\_项错误代码可以检索通过调用**GetLastError**。 每次迭代时，便会递增成员索引。

    或者，可以调用[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo) ，枚举设备的信息集，并返回指定的索引，在调用方分配的设备界面元素有关的信息[ **SP\_DEVINFO\_数据**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)结构。 然后，可以传递到此结构中的引用*DeviceInfoData*的参数[ **SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)函数。

3.  [**SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)若要获取设备接口的详细的数据。 在返回的信息[ **SP\_设备\_接口\_详细信息\_数据**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)结构。 因为的大小**SP\_设备\_界面\_详细信息\_数据**结构各不相同， **SetupDiGetDeviceInterfaceDetail**称为两次。 第一次调用获取要为分配的缓冲区大小**SP\_设备\_界面\_详细信息\_数据**结构。 第二次调用将填充有关接口的详细信息分配的缓冲区。
    1.  调用[ **SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)与*DeviceInterfaceDetailData*参数设置为**NULL**。 该函数将返回正确的缓冲区大小，以*requiredlength*参数。 此调用失败，出现错误\_不足\_缓冲区错误代码。 预期此错误代码。
    2.  将内存分配给[ **SP\_设备\_接口\_详细信息\_数据**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)结构基于在中检索到的正确的缓冲区大小*requiredlength*参数。
    3.  调用[ **SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)试并将其传递到中的初始化结构的引用*DeviceInterfaceDetailData*参数。 当函数返回时，有关该接口的详细信息填充结构。 设备路径采用的是[ **SP\_设备\_接口\_详细信息\_数据**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_detail_data_a)结构的**DevicePath**成员。

### <a href="" id="filehandle"></a>创建文件句柄设备-device.cpp 中看到 OpenDevice

若要与设备交互，需求 WinUSB 接口在设备上的第一个 （默认值） 接口的句柄。 模板代码获取文件句柄和 WinUSB 接口句柄，并将其存储在设备\_数据结构。

```cpp
HRESULT
OpenDevice(
    _Out_     PDEVICE_DATA DeviceData,
    _Out_opt_ PBOOL        FailureDeviceNotFound
    )
/*++

Routine description:

    Open all needed handles to interact with the device.

    If the device has multiple USB interfaces, this function grants access to
    only the first interface.

    If multiple devices have the same device interface GUID, there is no
    guarantee of which one will be returned.

Arguments:

    DeviceData - Struct filled in by this function. The caller should use the
        WinusbHandle to interact with the device, and must pass the struct to
        CloseDevice when finished.

    FailureDeviceNotFound - TRUE when failure is returned due to no devices
        found with the correct device interface (device not connected, driver
        not installed, or device is disabled in Device Manager); FALSE
        otherwise.

Return value:

    HRESULT

--*/
{
    HRESULT hr = S_OK;
    BOOL    bResult;

    DeviceData->HandlesOpen = FALSE;

    hr = RetrieveDevicePath(DeviceData->DevicePath,
                            sizeof(DeviceData->DevicePath),
                            FailureDeviceNotFound);

    if (FAILED(hr)) {

        return hr;
    }

    DeviceData->DeviceHandle = CreateFile(DeviceData->DevicePath,
                                          GENERIC_WRITE | GENERIC_READ,
                                          FILE_SHARE_WRITE | FILE_SHARE_READ,
                                          NULL,
                                          OPEN_EXISTING,
                                          FILE_ATTRIBUTE_NORMAL | FILE_FLAG_OVERLAPPED,
                                          NULL);

    if (INVALID_HANDLE_VALUE == DeviceData->DeviceHandle) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        return hr;
    }

    bResult = WinUsb_Initialize(DeviceData->DeviceHandle,
                                &DeviceData->WinusbHandle);

    if (FALSE == bResult) {

        hr = HRESULT_FROM_WIN32(GetLastError());
        CloseHandle(DeviceData->DeviceHandle);
        return hr;
    }

    DeviceData->HandlesOpen = TRUE;
    return hr;
}
```

1.  应用程序调用**CreateFile**来通过指定设备路径创建设备的文件句柄之前检索到。 它使用该文件\_标志\_OVERLAPPED 标志，因为 WinUSB 依赖于此设置。
2.  通过使用设备的文件句柄，应用程序创建 WinUSB 接口句柄。 [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)使用此句柄来标识目标设备而不是文件句柄。 若要获取 WinUSB 接口句柄，应用程序调用[ **WinUsb\_初始化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)通过传递文件句柄。 在后续调用中使用收到的句柄，从设备获取信息并将 I/O 请求发送到设备。

### <a name="release-the-device-handles---see-closedevice-in-devicecpp"></a>发布设备句柄-device.cpp 中看到 CloseDevice

模板代码实现代码，以释放文件句柄和设备的 WinUSB 接口句柄。

-   **CloseHandle**释放已通过的句柄**CreateFile**，如中所述[为设备创建文件句柄](#filehandle)本演练的部分。
-   [**WinUsb\_免费**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)释放 WinUSB 接口为设备返回的句柄[ **WinUsb\_初始化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)。

```cpp
VOID
CloseDevice(
    _Inout_ PDEVICE_DATA DeviceData
    )
/*++

Routine description:

    Perform required cleanup when the device is no longer needed.

    If OpenDevice failed, do nothing.

Arguments:

    DeviceData - Struct filled in by OpenDevice

Return value:

    None

--*/
{
    if (FALSE == DeviceData->HandlesOpen) {

        //
        // Called on an uninitialized DeviceData
        //
        return;
    }

    WinUsb_Free(DeviceData->WinusbHandle);
    CloseHandle(DeviceData->DeviceHandle);
    DeviceData->HandlesOpen = FALSE;

    return;
}
```

## <a name="next-steps"></a>后续步骤


接下来，阅读这些主题，发送获取设备信息并将数据传输发送到设备：

-   [通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)

    了解有关查询有关特定于 USB 的信息，例如设备的速度、 接口描述符、 相关终结点和其管道设备。

-   [将 USB 同步传输发送从 WinUSB 桌面应用](getting-set-up-to-use-windows-devices-usb.md)

    传输数据传入和传出的 USB 设备的同步终结点。

## <a name="related-topics"></a>相关主题
[有关 USB 设备的 Windows 桌面应用程序](windows-desktop-app-for-a-usb-device.md)  
[预配的驱动程序部署和测试的计算机](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)  



