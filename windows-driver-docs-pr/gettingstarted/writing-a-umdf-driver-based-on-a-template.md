---
title: 基于模板编写通用 Windows 驱动程序 (UMDF 2)
description: 本主题介绍了如何使用用户模式驱动程序框架 (UMDF) 2 编写通用 Windows 驱动程序。 首先使用 Microsoft Visual Studio 模板，然后在单独的计算机上部署和安装驱动程序。
ms.assetid: 03A3E389-8350-4E4B-9345-E50DD425374D
keywords:
- 编写 UMDF 驱动程序
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22d87ddd88af414359d0f792cb4bc21987db7e4b
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67359294"
---
# <a name="write-a-universal-windows-driver-umdf-2-based-on-a-template"></a>基于模板编写通用 Windows 驱动程序 (UMDF 2)

本主题介绍了如何使用用户模式驱动程序框架 (UMDF) 2 编写[通用 Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 首先使用 Microsoft Visual Studio 模板，然后在单独的计算机上部署和安装驱动程序。

若要开始操作，请确保已安装最新版本的 Microsoft Visual Studio 和 Windows 驱动程序工具包 (WDK)。 有关下载链接，请参阅[下载 Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

安装 WDK 时，需要包括 [Windows 调试工具](https://go.microsoft.com/fwlink/p?linkid=223405)。

## <a name="create-and-build-a-driver"></a>创建和生成驱动程序

>[!NOTE]
>在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。

1. 打开 Visual Studio 在“文件”  菜单上，选择“新建”&gt;“项目”  。
2. 在“新建项目”对话框的左侧窗格中，依次转到  “Visual C++”&gt;“Windows 驱动程序”&gt;“WDF”。 选择“用户模式驱动程序(UMDF V2)”  。
3. 在“名称”  字段中，输入“UmdfDriver”作为项目名称。
4. 在“位置”  字段中，输入要在其中创建新项目的目录。
5. 选中“创建解决方案的目录”  。 单击“确定”  。

    ![“新建项目”对话框的屏幕截图，其中显示选中的 WDF 和用户模式驱动程序 ](images/vs2015-umdf2-template.png)

    Visual Studio 将创建一个项目和一个解决方案。 可以在“解决方案资源管理器”  窗口中看到它们。 （如果未显示“解决方案资源管理器”  窗口，请从“视图”   菜单中选择“解决方案资源管理器”。）该解决方案有一个名为 UmdfDriver 的驱动程序项目。 若要查看驱动程序源代码，请打开**源文件**下的任何文件。 可以先从 Driver.c 和 Device.c 开始。

    ![解决方案资源管理器的屏幕截图，其中显示驱动程序项目中的文件](images/vs2015-umdf2-solution-explorer.png)

6. 在“解决方案资源管理器”  窗口中，右键单击“解决方案‘UmdfDriver’(1 个项目)”  ，然后选择“配置管理器”  。 为驱动程序项目选择配置和平台。 例如，选择“调试”  和“x64”  。
7. 在“解决方案资源管理器”  窗口中，右键单击“UmdfDriver”  ，然后选择“属性”  。 导航到  “配置属性”&gt;“驱动程序设置”&gt;“常规”。请注意，“目标平台”  默认为“通用”  。
8. 若要生成驱动程序，请从“生成”  菜单中选择“生成解决方案”  。 Microsoft Visual Studio 将在“输出”  窗口中显示生成进度。 （如果“输出”  窗口不可见，请从“视图”  菜单中选择“输出”  。）

    验证生成输出是否包括：

    ``` syntax
    >  Driver is a Universal Driver.
    ```

    确认解决方案成功生成后，可以关闭 Visual Studio。

9. 若要查看生成的驱动程序，请在“文件资源管理器”中，依次转到 **UmdfDriver** 文件夹和 **x64\\Debug\\UmdfDriver**。 该目录包含以下文件：

    * UmdfDriver.dll -- 用户模式驱动程序文件
    * UmdfDriver.inf -- 在安装驱动程序时 Windows 使用的信息文件

## <a name="deploy-and-install-the-universal-windows-driver"></a>部署和安装通用 Windows 驱动程序

通常，在测试和调试驱动程序时，调试程序和驱动程序会在不同的计算机上运行。 运行调试程序的计算机称为“主计算机”  ，运行驱动程序的计算机称为“目标计算机”  。 目标计算机也称为“测试计算机”  。

到目前为止，你已在主计算机上使用 Visual Studio 生成了驱动程序。 现在，需要配置目标计算机。 按照[预配计算机以便进行驱动程序部署和测试 (WDK 10)](provision-a-target-computer-wdk-8-1.md) 中的说明进行操作。 然后，你可以随时部署、安装、加载和调试驱动程序：

1. 在主计算机上，在 Visual Studio 中打开你的解决方案。 可以在 UmdfDriver 文件夹中双击解决方案文件 UmdfDriver.sln。
2. 在“解决方案资源管理器”  窗口中，右键单击“UmdfDriver”  ，然后选择“属性”  。
3. 在“UmdfDriver 属性页”  窗口中，依次转到“配置属性”&gt;“驱动程序安装”&gt;“部署”  ，如此处所示。
4. 选中“部署前删除以前的驱动程序版本”  。
5. 对于“目标设备名称”  ，请选择配置用于测试和调试的计算机名。
6. 选择“硬件 ID 驱动程序更新”  ，然后输入驱动程序的硬件 ID。 在本练习中，硬件 ID 为“Root\\UmdfDriver”。 单击“确定”  。

    ![“umdfdriver 属性页”的屏幕截图，其中显示选择了“部署驱动程序安装”](images/vs2015-deploy.png)

    **注意**  在本练习中，硬件 ID 不标识真实的硬件。 它标识了虚构设备，该设备位于[设备树](https://go.microsoft.com/fwlink/p?linkid=399236)中，作为根节点的子节点。 对于真实的硬件，不要选择“硬件 ID 驱动程序更新”  ，而要选择“安装并验证”  。
    可以在驱动程序的信息 (INF) 文件中看到硬件 ID。 在“解决方案资源管理器”  窗口中，转到“UmdfDriver”&gt;“驱动程序文件”  ，然后双击 UmdfDriver.inf。 硬件 ID 位于 \[Standard.NT$ARCH$\] 下。

    ```ManagedCPlusPlus
    [Standard.NT$ARCH$]
    %DeviceName%=MyDevice_Install,Root\UmdfDriver
    ```

7. 在“调试”  菜单上，选择“开始调试”  或按键盘上的 **F5**。
8. 等待直至已在目标计算机上部署、安装以及加载驱动程序。 这可能需要几分钟的时间。

## <a name="using-the-driver-module-framework-dmf"></a>使用驱动程序模块框架 (DMF)

[驱动程序模块 Framework (DMF)](https://github.com/Microsoft/DMF) 是 WDF 的一个扩展，可为 WDF 驱动程序开发人员提供额外的功能。 它可以帮助开发人员更快、更好地编写任何类型的 WDF 驱动程序。

作为一个框架，DMF 可用于创建称作“DMF 模块”的 WDF 对象。 可以在不同的驱动程序之间共享这些 DMF 模块的代码。 此外，DMF 捆绑了为我们为驱动程序开发的 DMF 模块库，可为其他驱动程序开发人员提供价值。

DMF 不会取代 WDF。 DMF 是与 WDF 搭配使用的另一个框架。 利用 DMF 的开发人员仍需使用 WDF 及其所有基元来编写设备驱动程序。

有关详细信息，请参阅[驱动程序模块框架 (DMF)](https://github.com/Microsoft/DMF)。

## <a name="related-topics"></a>相关主题

[开发、测试以及部署驱动程序](https://go.microsoft.com/fwlink/p?linkid=399234)

[Windows 调试工具](https://go.microsoft.com/fwlink/p?linkid=223405)

[编写第一个驱动程序](writing-your-first-driver.md)
