---
title: 使用 WDTF 简单 i/o 操作插件自定义设备 i/o
description: 若要从使用 Visual Studio 测试模板编写的设备基础测试和测试中获得最大好处，你的设备应由简单的 i/o 插件支持。
ms.assetid: 96BC880B-79DC-4CB1-BD79-87B0A4717634
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdeb8b063816163eceb4194ff0a19d967ec3c8d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844385"
---
# <a name="how-to-customize-io-for-your-device-using-the-wdtf-simple-io-action-plug-in"></a>如何使用 WDTF 简单 I/O 操作插件为你的设备自定义 I/O


若要从使用 Visual Studio 测试模板编写的设备基础测试和测试中获得最大好处，你的设备应由简单的 i/o 插件支持。 若要查看设备类型是否受支持，并确定是否有特定的测试要求，请参阅[提供的 WDTF 简单 i/o 插件](provided-wdtf-simpleio-plug-ins.md)。如果你的设备不受支持，则可以使用**WDTF 简单的 I/o 操作插件**模板在 Microsoft Visual Studio 中创建插件。

### <a name="prerequisites"></a>必备条件

-   测试中的设备已安装在测试计算机上。
-   在测试计算机上对其进行测试签名和安装的驱动程序包。 若要验证是否正确安装了驱动程序，请参阅[如何测试驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。
-   测试针对部署配置和预配的计算机。 请参阅[使用 Visual Studio 在运行时测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

<a name="instructions"></a>说明
------------

### <a href="" id="create-a-project-for-a-wdtf-simple-i-o-action-plug-in-"></a>步骤1：为 WDTF 简单 i/o 操作插件创建项目

1. 从**文件**菜单中，单击**新建&gt;项目**。
2. 从 "**新建项目**" 对话框的已安装模板列表中，选择 **" C++ Visual &gt; Windows 驱动程序 &gt; 测试" &gt; WDTF Simple i/o 操作插件**。
3. 提供简单的 i/o 项目和位置的名称（或使用默认值）。
4. 项目模板生成 Visual Studio 解决方案。 此解决方案包含为设备创建简单的 i/o 插件所需的所有文件。 这些文件的名称采用 WDTF&gt;SimpleIoAction\*<em>&lt;项目</em>格式。 简单 i/o 项目的默认名称为 DeviceType。
5. 模板为你的项目创建 WDTF 简单 i/o 操作接口。 接口作用于 IWDTFTarget2 接口的实例。
6. 构建 WDTF 简单的 i/o 插件解决方案，验证是否存在所有必需的文件。
7. 实现方法，通过在实现文件中添加代码来设置目标并实现简单的 i/o 操作（Open、Close 和 RunIO）。 该文件的名称采用 CWDTF*project*SimpleIoActionImpl 文件格式。

### <a href="" id="implement-the-settarget-method-for-your-device"></a>步骤2：为设备实现 SetTarget 方法

- 打开项目的实现文件（例如 CWDTFmyDeviceTypeSimpleIoActionImpl），找到[**IAction：： SetTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iaction-settarget) SetTarget 方法的实例。 此方法有一个标记为注释和 TODO 的部分：指示应在何处实现代码以检查与设备的兼容性。

  对于每个实例， **SetTarget**方法只调用一次 WDTF。 它有两个主要用途：

  - 以便 WDTF 可以确定该对象是否支持设备目标、pMainTarget
  - 因此，CWDTF<em>&lt;项目&gt;</em>SimpleIoActionImpl 实例可以从目标获取所需的信息，以完成以后打开（）、Close （）、RunIO （）方法调用。

  此方法的实现应返回 E\_NOINTERFACE，以指示目标不受支持。 如果支持目标，方法应返回\_OK。 如果发生其他任何失败，则该方法应返回 HRESULT 以指示错误。

  ```ManagedCPlusPlus
       
      ////
      // TODO: 1)  Perform your checks to see if your implementation is compatible with the target.
      //       Use the ITarget::GetValue() & ITarget::Eval() method to get the necessary data , info 
      //       to determine that. 
      //       2)  Also get the necessary info and save it in a member variable 
      //       to accomplish the later Open() method call.
  ```

### <a href="" id="implement-simpleioaction-to-open-the-interface"></a>步骤3：实现 SimpleIoAction 以打开接口

接下来，需要通过实现提供的 Open （）方法打开 ITarget 以进行测试。

此[**Open**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nf-wdtfinterfaces-iwdtfsimpleioex2-open)方法应尝试打开目标设备。 如果该方法无法执行此操作，则该方法应返回一个 HRESULT，指示失败。 如果已打开（初始化） SimpleIO 接口，此方法应失败。 实现此方法的方式取决于您的 ITarget 类型，以及在您的情况下最有用的内容。 也许，这意味着您应该使用 CreateFile （）打开它的句柄。 也许，这意味着您初始化了上下文结构，以便您可以跟踪正在进行的测试用例。 如果发生错误，方法应理想使用 COMReportError （），并应提供错误的说明以及可帮助防止将来出现的任何信息或步骤。

**请注意**  如果已打开 ISimpleIO\_操作，此方法应失败。

 

-   打开项目的实现文件（例如 CWDTFmyDeviceTypeSimpleIoActionImpl），找到[**open**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nf-wdtfinterfaces-iwdtfsimpleioex2-open)方法的实例。 此方法具有标记为注释和 TODO 的部分：

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

### <a href="" id="implement-the-simpleioaction-method-to--close-the-interface"></a>步骤4：实现 SimpleIoAction 方法以关闭接口

此方法应关闭先前打开的测试上下文。 即使您必须报告失败的 HRESULT，您也应该清除您的上下文。 只有在少数情况下，当您结束时出现的错误才有意义。 在此方法中，应恢复在 Open （）中执行的任何操作。 也许，这意味着您应该用 CloseHandle （）关闭先前打开的句柄。 如果发生错误，请为其提供可操作的说明。

**请注意**  此方法应在 ISimpleIO\_操作已关闭或从未打开的情况下失败。

 

-   打开项目的实现文件，例如 CWDTFmyDeviceTypeSimpleIoActionImpl，并找到[**Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfinterfaces/nf-wdtfinterfaces-iwdtfsimpleioex2-close)方法的实例。 此方法具有标记为注释和 TODO 的部分：

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

### <a href="" id="implement-the-simpleioaction-method-to-perform-simple-i-o-operations-"></a>步骤5：实现 SimpleIoAction 方法以执行简单的 i/o 操作

此方法应对目标执行少量的输入和输出操作。 然后，该方法应验证 i/o 操作是否已正确完成。 然后，每个测试都可以控制它对设备执行 i/o 的时间。 每次调用 RunIo （）方法时，只应执行少量的 i/o。 WDTF 将在循环中反复调用 RunIo （）以执行更多 i/o。 一般情况下，尝试将单个 RunIo （）方法调用保存到几秒钟。

**请注意**  在当前关闭 ISimpleIO\_操作时，此方法应失败。

 

-   打开项目的实现文件，例如 CWDTFmyDeviceTypeSimpleIoActionImpl，并找到 RunIO 方法的实例。 此方法具有标记为注释和 TODO 的部分：

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

### <a href="" id="build-and-install-the-simple-i-o-action-plugin-"></a>步骤6：生成并安装简单 i/o 操作插件

如果尚未执行此操作，你将需要配置计算机进行测试。 有关详细信息，请参阅为[驱动程序部署和测试预配计算机（wdk 8.1）](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)或[设置用于驱动程序部署和测试的计算机（wdk 8）](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

1. 生成解决方案。

   生成简单的 i/o 操作插件后，会创建两个测试。 这些测试将在测试计算机上安装和卸载插件。 默认情况下，简单的 i/o 操作插件文件显示在测试**组资源管理器**的 "测试类别"**我的测试类别**中。

2. 若要安装简单的 i/o 操作插件，请在测试计算机上运行名为**REGISTER WDTF** <em>&lt;项目&gt;</em> **SimpleIOAction**的测试。 有关选择和运行测试的信息，请参阅[如何使用 Visual Studio 在运行时测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。
3. 若要验证简单的 i/o 操作插件是否已安装，请在测试计算机上运行**具有 WDTF 简单 I/o 插件的显示设备**测试。 插件和设备应出现在结果中。 有关详细信息，请参阅[如何确定设备是否需要自定义 WDTF 简单 I/o 操作插件](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)。
4. 若要卸载简单的 i/o 操作插件，请在测试**计算机上运行**名为 "**取消注册" WDTF** <em>&lt;项目&gt;</em>"的测试。 可以通过运行**具有 WDTF 简单 i/o 插件测试的显示设备**来验证是否已卸载了插件。

## <a name="related-topics"></a>相关主题
[测试授权和执行框架 (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index)  
[如何确定设备是否需要自定义 WDTF 简单的 i/o 操作插件](test-your-device-to-see-if-you-need-to-customize-the-wdtf-simple-i-o-action-plug-in.md)  
[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)  



