---
description: 编写与 USB 设备通信的 Windows 桌面应用程序的最简单方法是使用 C/c + + WinUSB 模板。
title: 编写基于 WinUSB 模板的 Windows 桌面应用
ms.date: 07/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ecd406c88028c23ab2de8d8abed3db44f54b52b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732699"
---
# <a name="write-a-windows-desktop-app-based-on-the-winusb-template"></a>编写基于 WinUSB 模板的 Windows 桌面应用

编写与 USB 设备通信的 Windows 桌面应用程序的最简单方法是使用 C/c + + WinUSB 模板。 对于此模板，需要一个集成的环境，其中包含 Windows 驱动程序工具包 (WDK)  (，其中包含适用于 Windows 的调试工具) 以及 Microsoft Visual Studio 的专业版或旗舰版 (。 您可以使用模板作为起点。

## <a name="prerequisites"></a>先决条件

- 若要设置集成开发环境，请首先安装 Microsoft Visual Studio Ultimate 2019 或 Microsoft Visual Studio Professional 2019，然后安装 WDK。 可以在 [WDK 下载页](../download-the-wdk.md)上找到有关如何设置 Visual STUDIO 和 wdk 的信息。
- 安装 WDK 时包含 Windows 调试工具。 有关详细信息，请参阅 [下载和安装适用于 Windows 的调试工具](../debugger/index.md)。

## <a name="creating-a-winusb-application"></a>创建 WinUSB 应用程序

若要从模板创建应用程序：

1. 在 " **新建项目** " 对话框顶部的 "搜索" 框中，键入 " **USB"。**
2. 在中间窗格中，选择 " **WinUSB Application (通用) **"。
3. 选择“**下一页**”。
4. 输入项目名称，选择 "保存位置"，然后选择 " **创建**"。

    以下屏幕截图显示了 WinUSB 应用程序的 " **新建项目** " 对话框 ** (通用) ** 模板。

    ![winusb 模板新建项目第一个屏幕](images/winusb-template-creation-1.png)

    ![winusb 模板新项目创建第二个屏幕](images/winusb-template-creation-2.png)

    本主题假定 Visual Studio 项目的名称为 *USB Application1*。

    Visual Studio 将创建一个项目和一个解决方案。 如以下屏幕截图所示，你可以在 " **解决方案资源管理器** " 窗口中查看解决方案、项目和属于项目的文件。  (如果**解决方案资源管理器**窗口不可见，请从 "**视图**" 菜单中选择 "**解决方案资源管理器**"。 ) 解决方案包含名为 Application1 的 c + + 应用程序项目。

    ![winusb 模板解决方案资源管理器1](images/winusb-template-solution-explorer-1.png)

    USB Application1 项目具有应用程序的源文件。 若要查看应用程序源代码，可以打开 " **源文件**" 下显示的任何文件。  

5. 向解决方案添加驱动程序包项目。 选择并按住 (或右键单击) 解决方案 (解决方案 "USB Application1" ) ，然后选择 " **添加** \> **新项目** "，如以下屏幕截图所示。

    ![winusb 模板创建第二个项目添加](images/winusb-template-creation-3.png)

6. 在 " **新建项目** " 对话框顶部的 "搜索" 框中，再次键入 " **USB"。**
7. 在中间窗格中，选择 " **WINUSB INF 驱动程序包**"。
8. 选择“**下一页**”。
9. 输入项目名称，然后选择 " **创建**"。

    以下屏幕截图显示了**WINUSB INF 驱动程序包**模板的 "**新建项目**" 对话框。

    ![winusb 模板第二个项目第一个项目创建屏幕](images/winusb-template-creation-4.png)

    ![winusb 模板第二个项目创建第二个屏幕](images/winusb-template-creation-5.png)

    本主题假定 Visual Studio 项目的名称为 " *USB Application1 Package*"。

    USB Application1 包项目包含用于将 Microsoft 提供的 Winusb.sys 驱动程序安装为设备驱动程序的 INF 文件。

    **解决方案资源管理器**现在应包含这两个项目，如以下屏幕截图所示。

    ![winusb 模板解决方案资源管理器2](images/winusb-template-solution-explorer-2.png)

10. 在 INF 文件 USBApplication1 中，找到以下代码：   `%DeviceName% =USB_Install, USB\VID_vvvv&PID_pppp`

11. 将 VID \_ vvvv&PID \_ pppp 替换为设备的硬件 ID。 从设备管理器获取硬件 ID。 在设备管理器中，查看设备属性。 在 " **详细信息** " 选项卡上，查看 " **硬件 id** " 属性值。
12. 在 " **解决方案资源管理器** " 窗口中，选择并按住 (或右键单击) **解决方案 "USB Application1" (2 个项目) **，然后选择 " **Configuration Manager**"。 为应用程序项目和包项目选择配置和平台。 在此练习中，我们选择 "调试" 和 "x64"，如下面的屏幕截图所示。

![显示 "Configuration Manager" 窗口的屏幕截图，其中选择了 "调试" 和 "x64"。](images/winusb-template-configuration-manager.png)

## <a name="building-deploying-and-debugging-the-project"></a>生成、部署和调试项目

到目前为止，已使用 Visual Studio 创建项目。 接下来，需要配置设备连接到的设备。 该模板要求将 Winusb 驱动程序安装为设备的驱动程序。

测试和调试环境可以：

- 两台计算机设置：主计算机和目标计算机。 在主计算机上的 Visual Studio 中开发和生成项目。 调试程序在主计算机上运行，并在 Visual Studio 用户界面中可用。 测试和调试应用程序时，驱动程序将在目标计算机上运行。

- 单台计算机设置：目标和主机在一台计算机上运行。 在 Visual Studio 中开发和生成项目，并运行调试器和应用程序。

可以按照以下步骤部署、安装、加载和调试应用程序和驱动程序：

- **两台计算机安装**

  1. 按照 [设置计算机以进行驱动程序部署和测试](../gettingstarted/provision-a-target-computer-wdk-8-1.md)中的说明，预配目标计算机。
        **注意：**  预配将在名为 WDKRemoteUser 的目标计算机上创建用户。 预配完成后，会看到用户切换到 WDKRemoteUser。
  2. 在主计算机上，在 Visual Studio 中打开你的解决方案。
  3. 在 main 中，.cpp 将此行添加到 OpenDevice 调用之前。

  ```syntax
  system ("pause")
  ```

  该行会使应用程序在启动时暂停。 这对于远程调试非常有用。
  
  4. 在 pch 中包括以下行：

  ```syntax
  #include <cstdlib>
  ```

  `system()`上一步中的调用需要此 include 语句。

  5. 在 " **解决方案资源管理器** " 窗口中，选择并按住 (或右键单击) USB Application1 包，然后选择 " **属性**"。
  6. 在 " **USB Application1 包属性页** " 窗口的左窗格中，导航到 " **配置属性 &gt; 驱动程序安装 &gt; 部署**"，如以下屏幕截图所示。
  7. 选中“部署前删除以前的驱动程序版本”。
  8. 对于**远程计算机名**，请选择配置用于测试和调试的计算机名。 在此练习中，我们将使用名为 dbg 目标的计算机。
  9. 选择 " **安装/重新安装并验证**"。 选择“应用”。

        ![winusb 模板部署](images/winusb-template-deployment.png)

  10. 在属性页中，导航到 " **配置 &gt; 属性**" "调试"，然后选择 " **Windows 调试工具-远程调试器**"，如下面的屏幕截图所示。

        ![winusb 模板远程调试器](images/winusb-template-remote-debugger.png)

  11. 从 "**生成**" 菜单中选择 "**生成解决方案**"。 Visual Studio 会在 " **输出** " 窗口中显示生成进度。  (如果 "**输出**" 窗口不可见，请从 "**视图**" 菜单中选择 "**输出**"。在此练习中，我们为运行 Windows 10 的 x64 系统生成了项目 ) 。
  12. 从 "**生成**" 菜单中选择 "**部署解决方案**"。

在目标计算机上，会看到驱动程序安装脚本正在运行。 驱动程序文件将复制到目标计算机上的% Systemdrive% \\ drivertest \\ 驱动程序文件夹中。 请确认 .inf、.cat、测试证书和 .sys 文件以及其他任何必要的文件均位于 %systemdrive%\\drivertest\\drivers 文件夹下。 设备必须在设备管理器出现错误。

在主计算机上，会在 " **输出** " 窗口中看到此消息。

```syntax
Deploying driver files for project
"<path>\visual studio 14\Projects\USB Application1\USB Application1 Package\USB Application1 Package.vcxproj".  
Deployment may take a few minutes...
========== Build: 1 succeeded, 0 failed, 1 up-to-date, 0 skipped ==========
```

### <a name="to-debug-the-application"></a>若要调试该应用程序

1. 在主计算机上，在 "解决方案" 文件夹中导航到 **x64 &gt; Win 8.1 调试** 。
2. 将应用程序可执行文件（UsbApplication1.exe）复制到目标计算机。
3. 在目标计算机上启动应用程序。
4. 在主计算机上，从 " **调试** " 菜单中选择 " **附加到进程**"。
5. 在窗口中，选择 " **Windows 用户模式调试器** " ("Windows) 调试工具" 作为传输，将目标计算机的名称（在本例中为 "dbg-目标"）作为限定符，如图所示。

    ![winusb 模板调试设置](images/winusb-template6.png)

6. 从 **可用进程** 列表中选择应用程序，并选择 " **附加**"。 你现在可以使用 " **即时" 窗口** 或使用 " **调试** " 菜单中的选项进行调试。

上述说明使用 **Windows 调试工具调试应用程序–远程调试器**。 如果要使用 **远程 Windows 调试器** (包含在 Visual Studio) 中的调试器，请按照以下说明操作：

1. 在目标计算机上，将 msvsmon.exe 添加到通过防火墙允许的应用列表中。
2. 启动位于 C： \\ DriverTest msvsmonmsvsmon.exe 中的 Visual Studio 远程调试监视器 \\ \\ 。
3. 创建工作文件夹，例如 C： \\ remotetemp。
4. 将 UsbApplication1.exe 的应用程序复制到目标计算机上的工作文件夹。
5. 在主计算机上的 Visual Studio 中，右键单击 **USB Application1 包** 项目，然后选择 " **卸载项目**"。
6. 选择并按住 (或右键单击) **USB Application1** 项目，在 "项目属性" 中展开 " **配置属性** " 节点，然后选择 " **调试**"。
7. 更改 **调试器以启动** 到 **远程 Windows 调试器**。
8. 按照 [远程调试本地生成的项目](/visualstudio/debugger/remote-debugging?view=vs-2015)中提供的说明更改项目设置以在远程计算机上运行可执行文件。 请确保 " **工作目录** " 和 " **远程命令** 属性" 反映目标计算机上的文件夹。
9. 若要调试应用程序，请在 " **生成** " 菜单中选择 " **启动调试**"，或按 **F5。**

- **单台计算机安装：**

  1. 若要生成应用程序和驱动程序安装包，请从 "**生成**" 菜单中选择 "**生成解决方案**"。 Visual Studio 会在 " **输出** " 窗口中显示生成进度。  (如果 "**输出**" 窗口不可见，请从 "**视图**" 菜单中选择 "**输出**"。在此练习中，我们为运行 Windows 10 的 x64 系统生成了项目 ) 。
  2. 若要查看生成的驱动程序包，请在 Windows 资源管理器中导航到 USB Application1 文件夹，然后导航到 **x64 \> 调试 \> USB Application1 包**。 驱动程序包包含多个文件： MyDriver 是 Windows 在安装驱动程序时使用的信息文件，mydriver.cat 是安装程序用来验证驱动程序包的测试签名的目录文件。 以下屏幕截图显示了这些文件。

        ![winusb 应用程序模板](images/winusb-template3.png)

        **注意**  包中没有任何驱动程序文件。 这是因为 INF 文件引用 Windows System32 文件夹中的内置驱动程序 Winusb.sys \\ 。
  3. 手动安装驱动程序。 在设备管理器中，通过在包中指定 INF 来更新驱动程序。 指向位于解决方案文件夹中的驱动程序包，如上一节所示。
  4. 选择并按住 (或右键单击) **USB Application1** 项目，在 "项目属性" 中展开 " **配置属性** " 节点，然后选择 " **调试**"。
  5. 更改 **调试器以启动** 到 **本地 Windows 调试器**。
  6. 选择并按住 (或右键单击 USB Application1 包项目) ，然后选择 " **卸载项目**"。
  7. 若要调试应用程序，请在 " **生成** " 菜单中选择 " **启动调试**"，或按 **F5**。

## <a name="template-code-discussion"></a>模板代码讨论

模板是桌面应用程序的起点。 USB Application1 项目包含源文件设备 .cpp 和 main .cpp。

主 .cpp 文件包含应用程序入口点 \_ tmain。 设备 .cpp 包含打开并关闭设备句柄的所有帮助程序函数。

该模板还有一个名为 "设备" 的头文件。 此文件包含 (后面讨论的设备接口 GUID 的定义) 和 \_ 存储应用程序获取的信息的设备数据结构。 例如，它存储由 OpenDevice 获取并在后续操作中使用的 WinUSB 接口句柄。

```cpp
typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];

} DEVICE_DATA, *PDEVICE_DATA;
```

### <a name="getting-the-instance-path-for-the-device---see-retrievedevicepath-in-devicecpp"></a>获取设备的实例路径-请参阅 RetrieveDevicePath in node.js

若要访问 USB 设备，应用程序可以通过调用 **CreateFile**为设备创建一个有效的文件句柄。 对于该调用，应用程序必须获取设备路径实例。 为了获取设备路径，应用使用 [setupapi.log](../install/setupapi.md) 例程，并指定 INF 文件中用于安装 Winusb.sys 的设备接口 GUID。 Device 将声明一个名为 GUID DEVINTERFACE USBApplication1 的 GUID 常量 \_ \_ 。 通过使用这些例程，应用程序会枚举指定设备接口类中的所有设备，并检索设备的设备路径。

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

在前面的函数中，应用程序通过调用以下例程获取设备路径：

1. [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsexa) 获取 *设备信息集*的句柄，它是一个数组，其中包含与指定的设备接口类、GUID DEVINTERFACE USBApplication1 匹配的所有已安装设备的相关信息 \_ \_ 。 数组中名为 *设备接口* 的每个元素对应于在系统中安装和注册的设备。 通过传递您在 INF 文件中定义的设备接口 GUID 来标识设备接口类。 函数将返回设备信息集的 HDEVINFO 句柄。
2. [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 用于枚举设备信息集中的设备接口，并获取有关设备接口的信息。

    此调用需要以下项：

   - 一个已初始化的调用方分配的 [**SP \_ 设备 \_ 接口 \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data) 结构，它将其 **cbSize** 成员设置为结构的大小。
   - 步骤1中的 HDEVINFO 句柄。
   - 在 INF 文件中定义的设备接口 GUID。

    [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 为设备接口的指定索引查找设备信息集数组，并用有关接口的基本数据填充已初始化的 [**SP \_ 设备 \_ 接口 \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data) 结构。

    **注意**   若要枚举设备信息集中的所有设备接口，请在循环中调用 [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) ，直到该函数返回 **FALSE** ，并且失败的错误代码为 "错误" \_ \_ \_ 。 错误：无法再 \_ \_ \_ 调用 **GetLastError**来检索更多项错误代码。 对于每个迭代，递增成员索引。

    或者，您可以调用 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 来枚举设备信息集，并返回由调用方分配的 [**SP \_ lnk-devinfo \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构中的索引指定的设备接口元素的相关信息。 然后，你可以在[**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)函数的*DeviceInfoData*参数中传递对此结构的引用。

3. [**SetupDiGetDeviceInterfaceDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila) 获取设备接口的详细数据。 该信息在 [**SP \_ 设备 \_ 接口 \_ 详细信息 \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_detail_data_a) 结构中返回。 由于 **SP \_ 设备 \_ 接口 \_ 详细信息 \_ 数据** 结构的大小不同， **SetupDiGetDeviceInterfaceDetail** 调用了两次。 第一次调用获取为 **SP \_ 设备 \_ 接口 \_ 详细信息 \_ 数据** 结构分配的缓冲区大小。 第二次调用用有关接口的详细信息填充分配的缓冲区。
   1. 调用 [**SetupDiGetDeviceInterfaceDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila) ，并将 *DeviceInterfaceDetailData* 参数设置为 **NULL**。 函数在 *requiredlength* 参数中返回正确的缓冲区大小。 此调用失败，出现错误 \_ \_ 缓冲区错误代码。 应为此错误代码。
   2. 基于在*requiredlength*参数中检索到的正确缓冲区大小为[**SP \_ 设备 \_ 接口 \_ 详细信息 \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_detail_data_a)结构分配内存。
   3. 再次调用 [**SetupDiGetDeviceInterfaceDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila) ，并向其传递对 *DeviceInterfaceDetailData* 参数中已初始化结构的引用。 当函数返回时，该结构将填充有关接口的详细信息。 设备路径在 [**SP \_ 设备 \_ 接口 \_ 详细信息 \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_detail_data_a) 结构的 **DevicePath** 成员中。

### <a name="creating-a-file-handle-for-the-device"></a>为设备创建文件句柄

请参阅 OpenDevice in node.js。

若要与设备交互，需要设备上第一个 (默认) 接口的 WinUSB 接口句柄。 模板代码获取文件句柄和 WinUSB 接口句柄，并将其存储在设备 \_ 数据结构中。

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

1. 此应用通过指定先前检索到的设备路径来调用 **CreateFile** 来创建设备的文件句柄。 \_ \_ 由于 WinUSB 依赖于此设置，因此它使用文件标志重叠标志。
2. 通过使用设备的文件句柄，应用程序将创建 WinUSB 接口句柄。 [WinUSB 函数](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb) 使用此句柄来标识目标设备，而不是文件句柄。 若要获取 WinUSB 接口句柄，应用通过传递文件句柄来调用 [**WinUSB \_ Initialize**](/windows/win32/api/winusb/nf-winusb-winusb_initialize) 。 使用后续调用中接收的句柄从设备获取信息，并将 i/o 请求发送到设备。

### <a name="release-the-device-handles---see-closedevice-in-devicecpp"></a>释放设备句柄-请参阅 CloseDevice in node.js

模板代码实现代码以释放文件句柄和设备的 WinUSB 接口句柄。

- **CloseHandle** 释放由 **CreateFile**创建的句柄，如本演练的为 [设备创建文件句柄](#creating-a-file-handle-for-the-device) 部分所述。
- [**WinUsb\_Free**](/windows/win32/api/winusb/nf-winusb-winusb_free) 释放设备的 WinUSB 接口句柄，该句柄由 [**WinUsb\_Initialize**](/windows/win32/api/winusb/nf-winusb-winusb_initialize) 返回。

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

接下来，请阅读以下主题，以发送获取设备信息和将数据传输到设备：

- [使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)

    了解如何查询设备以获取 USB 特定的信息，例如设备速度、接口描述符、相关终结点及其管道。

- [发送来自 UWP 桌面应用的 USB 常时等量传输](getting-set-up-to-use-windows-devices-usb.md)

    在 USB 设备的同步终结点之间传输数据。

## <a name="related-topics"></a>相关主题

[USB 设备的 Windows 桌面应用](windows-desktop-app-for-a-usb-device.md)  
[预配用于驱动程序部署和测试的计算机](../gettingstarted/provision-a-target-computer-wdk-8-1.md)