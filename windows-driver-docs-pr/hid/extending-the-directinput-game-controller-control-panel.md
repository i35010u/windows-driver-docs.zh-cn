---
title: 扩展 DirectInput 游戏控制器控制面板
description: 扩展 DirectInput 游戏控制器控制面板
ms.assetid: 45df8aee-10e0-43b3-8878-3ad83d822028
keywords:
- 属性表 WDK DirectInput
- 游戏控制器 WDK DirectInput
- 控制面板 WDK DirectInput
- 游戏控制器 WDK HID，游戏控制器支持
- 强制反馈驱动程序 WDK HID、属性表
- 游戏板支持 WDK DirectInput
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9291bda0d2ee61078e57416f4f5f0df078560950
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355963"
---
# <a name="extending-the-directinput-game-controller-control-panel"></a>扩展 DirectInput 游戏控制器控制面板

本部分提供有关创建 Microsoft DirectInput 游戏控制器控制面板的属性表的信息。

## <a name="about-the-directinput-control-panel"></a>关于 DirectInput 控制面板

DirectInput 提供游戏控制器（如游戏垫、游戏杆和强制反馈设备）的支持。 在 Microsoft DirectX 5.0 及更高版本中，DirectInput 提供了一个名为 Joy.cpl 的新游戏控制器控制面板。 此版本的 "控制面板" 是第一个允许扩展性的第一种方式：为每个控制器显示的属性表可以替换为特定于该控制器的属性页。 这是通过创建包含这些属性表相关信息的 DLL 来完成的。 此 DLL 公开由 DirectInput 控制面板调用的 COM 接口。

游戏控制器硬件供应商建议使用此扩展功能为其游戏控制器提供自定义属性表，而不是创建单独的控制面板。 这样，用户就可以打开一个控制面板来配置和测试游戏控制器。

## <a name="directinput-control-panel-architecture"></a>DirectInput 控制面板体系结构

本部分介绍 DirectInput 控制面板可扩展属性表的基本结构。 以下主题对此结构进行了说明：

### <a name="game-controller-control-panel"></a>游戏控制器控制面板

DirectInput 控制面板的基本体系结构包括 DirectInput 游戏控制器控制面板、支持 **IDIGameCntrlPropSheet** COM 接口的抽象层库和每个游戏控制器属性表的 COM 对象。

> [!NOTE]
>"对象" 一词描述了由 CreateInstance 创建的实体，以支持 COM 接口的方法，即使这些方法不是通过面向对象的编程语言（如 c + +）调用的。 "工作表" 一词描述了页面要插入到的对话框。 "页" 一词描述 "属性表" 对话框的内容对话框。

由于 Microsoft Windows 95/98/Me 与 Windows NT 4.0 及更高版本之间的可移植性，DirectInput 控制面板直接与 DirectInput 配合使用，而后者又直接适用于设备驱动程序。 作为此项的一种产品，DirectInput 控制面板可以访问输入设备，即使应用程序处于后台时也是如此。

### <a name="gcdefdll-the-default-analog-device-property-sheet"></a>Gcdef.dll，默认的模拟设备属性表

不创建自己的控制面板的硬件供应商使用 Gcdef.dll 提供的默认模拟设备属性表的服务。 注册表中没有**ConfigCLSID**密钥的任何控制器在其**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Control \\ windows.media.mediaproperties \\ PrivateProperties \\ 游戏杆 \\ OEM \\ **<em>控制器 \_ 名称</em>条目下均使用此默认属性表。 此属性表包含以下两个页面：

- **测试：** 此页说明设备响应正常。 它将返回与设备属性相关联的注册表设置的图形表示形式，并允许用户查看这些设置。

- **设置：** 此页允许用户将有关设备的特定信息写入系统。 提供的服务用于校准和方向舵或脚踏板。

### <a name="integration-with-windows"></a>与 Windows 集成

因为属性表页是一个 COM 对象，所以需要注册它。 这可以通过 INF 文件或通过 DirectInput 的 **IDirectInputJoyConfig8** 接口完成。 示例 INF 文件是 (DDK) 的 DirectX 驱动程序开发工具包中的示例属性表的一部分。

**注册属性表页：**

1. 使用 Microsoft Windows SDK) 中 (的 "Guidgen.exe" 工具创建属性表的 CLSID， (这与) 前面提到的 **ConfigCLSID** 条目中输入的工具相同。 请记住，这是特定于设备的属性表 GUID，并且应与代码中的 GUID 相同。

2. 使用此新 GUID 在注册表中创建新密钥， **我的电脑 \\ HKEY \_ 类 \_ 根 \\ CLSID** (应类似于 {B9EA2BE1-E8E9-11D0-9880-00AA0044480F} ) 。

3. 在该密钥中，创建名为 **InProcHandler32** 和 **InProcServer32**的子项。

4. 在 **InProcServer32** 项中，编辑 (默认) 项，以反映属性表 DLL 的位置和名称。

设备还必须正确地注册为游戏设备。 这可以通过 DirectInput 或通过 INF 文件来完成。

**注册设备：**

1. 在注册表项 **我的电脑 \\ HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ control \\ windows.media.mediaproperties \\ PrivateProperties \\ 操纵杆 \\ OEM**中，输入设备的密钥。 建议将此密钥名称设置为与设备 OEM 名称相同。

2. 创建以下条目：

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>键值</th>
    <th>键值类型</th>
    <th>键值类型内容</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ConfigCLSID</p></td>
    <td><p>“字符串值”</p></td>
    <td><p>"{您的属性表 CLSID}"</p></td>
    </tr>
    <tr class="even">
    <td><p>OEMName</p></td>
    <td><p>“字符串值”</p></td>
    <td><p>"设备的产品名称"</p></td>
    </tr>
    </tbody>
    </table>

> [!NOTE]
> 这两个条目是开始所需的最小值。 有关所有可用条目及其关联服务的其他信息，请参阅 DirectX DDK。

## <a name="directinput-control-panel-essentials"></a>DirectInput 控制面板概要

本部分介绍 DirectInput 控制面板的概念和组件，并提供相关信息，帮助你开始实现自己的特定于设备的属性表。 此信息如下所述：

### <a name="files-and-your-build-environment"></a>文件和生成环境

至少需要使用直接 X 直接开发工具包 (DDK) 头文件 Dicpl。 此文件提供必要的接口、结构、类定义和错误。 建议将 DirectInput 的 **IDirectInputJoyConfig8** 接口用于所有注册表访问，以确保属性表也可以在 Windows NT 4.0 及更高版本上工作。 如果计划在属性页中使用 DirectInput，则还必须使用关联的 DirectX SDK 文件。 DirectInput 控制面板中的所有结构都打包在8字节边界上。 验证属性表在8字节边界上包结构。

**注意**   测试 "控制面板" 时，请确保在 "主显示器" 设置为 640 x 480 像素分辨率的系统上进行测试。 确保所有控件在此降低的分辨率下仍然可见。

## <a name="creating-your-property-sheet"></a>创建属性表

此示例演示了 DirectInput 的许多方面，并为您自己的自定义属性表提供了一个很好的起点。

### <a name="create-your-own-property-sheet"></a>创建自己的属性表

从头开始创建自定义属性表是一个相对简单的过程。

1. 创建 GUID 来标识属性页：

    - 使用 Microsoft Windows SDK) 中 (的 "Guidgen.exe" 工具，无论) 多少页，都只 (一个属性页创建一个 GUID。 在应用程序特定的包含文件中定义此项。
    - 创建所需的 DllGetClassObject 和 DllCanUnloadNow。
    - 为在 Dicpl 中定义的 COM ClassFactory 创建实现。
    - 创建 **IDIGamgeCntrlPropSheet** 接口的实现。
    - 使用 Regedit 将定义的 GUID 添加到我的电脑 \\ HKEY \_ 类的 \_ 根 \\ CLSID 密钥。 然后向密钥添加密钥 "InProcHandler32" 和 "InProcServer32"。
    - 修改 InProcServer32 项的 (默认) 项，以指向属性表 DLL 的位置。 例如： "C： \\ my \_ device \\ my \_propertysheet.dll"。 此示例显示 ProgID 条目。 这并不是必需的，但通常用于存储有关位于该 GUID 上的模块的信息。

2. 为任何 Windows 应用程序创建对话框模板和对话框过程。

    > [!NOTE]
    > 您可能想要将属性表的测试容器编写为作为独立对话框启动页面的窗口。 此时，你还可以将你可能具有的任何现有控制面板转换为 DirectInput 控制面板。

3. 填充 [**DIGCPAGEINFO**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538484(v=vs.85)) 和 [**DIGCSHEETINFO**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538492(v=vs.85)) 结构，并分别在 [**IDIGameCntrlPropSheet：： GetPageInfo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540026(v=vs.85)) 和 [**IDIGameCntrlPropSheet：： GetSheetInfo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540029(v=vs.85)) 的实现中返回该信息。

属性表页的生成通过 **属性表** 函数完成。 在属性表页面中，此函数的所有行为都是固有的。 例如，"属性页" 页面反映了它接收的最大的对话框模板。 如果用户创建了一个页面，并且其关联的模板非常小，则会直接反映结果对话框的大小。

在考虑视觉对象对齐和页面上的控件居中时，还必须记住对话框模板。 例如，假设用户创建两个页面，其中包含指定为在页面上居中的项目。 要居中的一项为200对话单位 (Dlu) 宽度;另一个为100单位。 在这种情况下，后一项不在页面上居中。 相反，控件将围绕其模板和其他空白 (或灰色，因为它可能会) 添加到更窄的页的宽度。 您应该创建相同大小的对话框模板，即使您不使用所有这些模板。  (有关 **属性表** 函数的详细信息，请参阅 MICROSOFT Win32 SDK。 ) 

### <a name="testing-your-property-sheet"></a>测试属性表

强烈建议在测试属性表页的过程中，运行 DirectInput 和 DirectInput 控制面板的调试版本。 DirectX 组件设计用于向调试窗口/终端颁发有用的错误和警告消息。

调试 "控制面板" 应用程序可能比较棘手。 使用以下步骤在 Microsoft Developer Studio 5.0 和更高版本的 (中调试自定义属性页，其他编译器) 具有类似的行为。

1. 从 " **项目** " 菜单中选择 " **设置**"。

2. 选择 " **调试** " 选项卡。

3. 对于调试会话的可执行文件，请输入 C： \\ windows \\RUNDLL32.EXE (假定 c： \\ windows 是 windows 95/98/me 目录) 如果你运行的是 windows 95/98/me，则为 c： \\ winnt \\ SYSTEM32 \\RUNDLL32.EXE (假定 C： \\ winnt 是操作系统目录) 如果你运行的是 windows NT 4.0 或更高版本。

4. 对于程序参数，请输入 **shell32.dll、Control \_ RunDLL c： \\ windows \\ system \\joy.cpl**。 同样，这假定 C： \\ windows 是您的 windows 目录。 它区分大小写，必须严格按所示输入。

完成后，设置断点，然后从 "生成" 菜单中选择 " **启动调试**" **，然后选择**"执行"。 你现在已准备好调试自定义属性表页。
