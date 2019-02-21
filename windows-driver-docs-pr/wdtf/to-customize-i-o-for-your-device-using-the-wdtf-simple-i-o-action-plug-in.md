---
title: 自定义设备 I/O 使用插件 WDTF 简单 I/O 操作
description: 若要从设备基础测试和测试您可能需要编写使用 Visual Studio 测试模板获取最大效益，应通过一个简单的 I/O 插件支持你的设备。
ms.assetid: 96BC880B-79DC-4CB1-BD79-87B0A4717634
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 284247bde18720594753b2cd323aa25818fd6832
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526244"
---
# <a name="how-to-customize-io-for-your-device-using-the-wdtf-simple-io-action-plug-in"></a>如何使用 WDTF 简单 I/O 操作插件为你的设备自定义 I/O


若要从设备基础测试和测试您可能需要编写使用 Visual Studio 测试模板获取最大效益，应通过一个简单的 I/O 插件支持你的设备。 若要查看你的设备类型是否受支持并确定是否有用于测试的特定要求，请参阅[提供 WDTF 简单 I/O 插件](provided-wdtf-simpleio-plug-ins.md)。如果不支持你的设备，你可以创建插件在 Microsoft Visual Studio 中使用**WDTF 简单 I/O 操作插件**模板。

### <a name="prerequisites"></a>必备条件

-   在测试计算机上安装待测试的设备。
-   是测试签名，并且在测试计算机上安装的驱动程序包。 若要验证您的驱动程序是否正确安装，请参阅[如何测试驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/test_a_driver_package)。
-   测试针对部署配置和预配的计算机。 请参阅[测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

<a name="instructions"></a>说明
------------

### <a href="" id="create-a-project-for-a-wdtf-simple-i-o-action-plug-in-"></a>步骤 1:为 WDTF 简单 I/O 操作插件创建项目

1. 从**文件**菜单中，单击**新建&gt;项目**。
2. 从列表中已安装模板**新的项目**对话框中，选择**Visual c + + &gt; Windows 驱动程序&gt;测试&gt;WDTF 简单 I/O 操作插件**。
3. 提供简单的 I/O 项目和位置的名称 （或使用默认值）。
4. 项目模板生成的 Visual Studio 解决方案。 该解决方案包含需要创建一个简单的 I/O 设备插件的所有文件。 文件的名称采用以下形式 WDTF<em>&lt;项目&gt;</em>SimpleIoAction\*。 简单的 I/O 项目的默认名称是设备类型。
5. 该模板将创建一个 WDTF 相当简单的 I/O 操作接口，用于你的项目。 接口对 IWDTFTarget2 接口的实例。
6. 生成 WDTF 简单 I/O 插件解决方案以验证所需的所有文件都都存在。
7. 实现方法以设置目标，然后通过在实现文件中添加代码来实现简单的 I/O 操作 （打开、 关闭、 和 RunIO）。 文件的名称采用以下格式 CWDTF*项目*SimpleIoActionImpl.cpp 文件。

### <a href="" id="implement-the-settarget-method-for-your-device"></a>步骤 2:实现你的设备的 settarget 定位方法

- 打开你的项目，例如，CWDTFmyDeviceTypeSimpleIoActionImpl.cpp，实现文件并找到的实例[ **IAction::SetTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff538790) settarget 定位方法。 此方法中有一部分标有注释，而 TODO:，该值指示应在其中实现与你的设备的兼容性检查的代码。

  **Settarget 定位**方法由调用一次 WDTF 每个实例。 它具有两个主要目的：

  - 以便 WDTF 可以确定对象是否支持设备目标，pMainTarget
  - 以便 CWDTF<em>&lt;项目&gt;</em>SimpleIoActionImpl 实例可以从目标中，以便实现更高版本 open （），close （），RunIO() 方法调用来获取所需的信息。

  此方法的实现应返回 E\_NOINTERFACE 以指示不支持目标。 该方法应返回 S\_确定目标是否支持。 如果发生任何其他故障，该方法应返回 HRESULT 来指示错误。

  ```ManagedCPlusPlus
       
      ////
      // TODO: 1)  Perform your checks to see if your implementation is compatible with the target.
      //       Use the ITarget::GetValue() & ITarget::Eval() method to get the necessary data , info 
      //       to determine that. 
      //       2)  Also get the necessary info and save it in a member variable 
      //       to accomplish the later Open() method call.
  ```

### <a href="" id="implement-simpleioaction-to-open-the-interface"></a>步骤 3:若要打开该接口的实现 SimpleIoAction

接下来，您需要打开 ITarget 用于测试的实现提供的 open （） 方法。

这[**打开**](https://msdn.microsoft.com/library/windows/hardware/hh451153)方法应尝试打开目标设备。 如果该方法无法执行此操作，该方法应返回一个 HRESULT，指示失败。 如果 SimpleIO 接口是已打开 （初始化），此方法应失败。 如何实现此方法取决于 ITarget 类型和最适合您的情况。 也许这意味着您应使用 createfile （） 打开的句柄。 这可能意味着初始化上下文结构，以便你可以跟踪的正在进行的测试用例。 发生错误时该方法应在理想情况下使用 COMReportError （），并且应提供错误任何信息或步骤，可以帮助防止将来再次发生的说明。

**请注意**  如果此方法应失败 ISimpleIO\_操作已打开。

 

-   打开你的项目，例如，CWDTFmyDeviceTypeSimpleIoActionImpl.cpp，实现文件并找到的实例[**开放**](https://msdn.microsoft.com/library/windows/hardware/hh451153)方法。 此方法有标有注释，而 TODO 部分：

    ```cpp
    //
       //   TODO: Add code for your implementation of Open() here.
       //
       //
       //  To return failure use COMReportError(,,,).  For example the following 
       //  will return E_FAIL as the error code and "My Device error String"  as
       //  the error string.
       //
       //  COMReportError(WDTF, E_FAIL, "My Device error String");
       //
    ```

### <a href="" id="implement-the-simpleioaction-method-to--close-the-interface"></a>步骤 4:实现 SimpleIoAction 方法以关闭界面

此方法应关闭以前打开的测试上下文。 您应清除您的上下文，即使必须报告失败的 HRESULT。 有仅几种的情况其中错误发生在关闭时的实际意义。 在此方法中，应还原在 open （） 中执行任何操作。 这可能意味着应关闭 CloseHandle() 与您以前打开的句柄。 发生错误，请为它提供可操作的说明。

**请注意**  如果此方法应失败 ISimpleIO\_操作已关闭或从未打开。

 

-   打开你的项目，例如，CWDTFmyDeviceTypeSimpleIoActionImpl.cpp，实现文件并找到的实例[**关闭**](https://msdn.microsoft.com/library/windows/hardware/hh451151)方法。 此方法有标有注释，而 TODO 部分：

    ```cpp
    //
       //  //
       //   TODO: Add code for your implementation of Close() here.
       //
       // 
       //
       //  To return failure use COMReportError(,,,).  For example the following 
       //  will return E_FAIL as the error code and "My Device error String"  as
       //  the error string.
       //
       //  COMReportError(WDTF, E_FAIL, "My Device error String");
       //
     
       //
    ```

### <a href="" id="implement-the-simpleioaction-method-to-perform-simple-i-o-operations-"></a>步骤 5:实现 SimpleIoAction 方法以执行简单的 I/O 操作

此方法应执行少量的目标系统上的输入和输出操作。 然后，该方法应验证已正确完成 I/O 操作。 然后，每个测试可以控制多长时间对设备执行 I/O。 每次调用 RunIo() 方法仅应执行少量的 I/O。 WDTF 将重复调用 RunIo()，在一个循环，以便执行更多的 I/O。 一般情况下，尝试保留对几秒钟的单个 RunIo() 方法调用。

**请注意**  如果此方法应失败 ISimpleIO\_操作当前已关闭。

 

-   打开你的项目，例如，CWDTFmyDeviceTypeSimpleIoActionImpl.cpp，实现文件并找到 RunIO 方法的实例。 此方法有标有注释，而 TODO 部分：

    ```cpp
    //
       //  //
       //   TODO: Add code for your implmentaiton of RunIO() here.
       //
       // 
       //
       //  To return failure use COMReportError(,,,).  For example the following 
       //  will return E_FAIL as the error code and "My Device error String"  as
       //  the error string.
       //
       //  COMReportError(WDTF, E_FAIL, "My Device error String");
       //
     
       //
    ```

### <a href="" id="build-and-install-the-simple-i-o-action-plugin-"></a>步骤 6:生成并安装简单的 I/O 操作插件

如果尚未这样做，您需要配置用于测试的计算机。 有关详细信息，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/dn745909)。

1. 生成解决方案。

   生成简单插件的 I/O 操作时，创建两个测试。 这些测试安装和卸载测试计算机上的插件。 默认情况下，简单的 I/O 操作的插件文件出现在**测试组资源管理器**，在测试类别**我的测试类别**。

2. 若要安装简单的 I/O 操作插件，请运行名为测试**注册 WDTF**<em>&lt;项目&gt;</em>**SimpleIOAction.DLL**在测试计算机上. 测试的选择和运行的信息，请参阅[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)。
3. 若要验证是否安装了简单的 I/O 操作插件，请运行**显示了 WDTF 简单 I/O 插件设备**测试计算机上进行测试。 你的插件和设备应显示在结果中。 有关详细信息，请参阅[方法如何确定是否需要为你的设备自定义 WDTF 简单 I/O 操作插件](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)。
4. 若要卸载简单的 I/O 操作插件，请运行名为测试**取消注册 WDTF**<em>&lt;项目&gt;</em>**SimpleIOAction.DLL**上测试计算机。 你可以验证已通过运行卸载插件**显示了 WDTF 简单 I/O 插件设备**测试。

## <a name="related-topics"></a>相关主题
[测试创作和执行框架 (TAEF)](https://msdn.microsoft.com/library/windows/hardware/hh439725)  
[如何确定自定义 WDTF 简单 I/O 操作插件是否需要为你的设备](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)  
[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)  



