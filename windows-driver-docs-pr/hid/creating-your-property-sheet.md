---
title: 创建属性表
description: 创建属性表
ms.assetid: 04fa34fd-86d6-4017-a6da-9882d65674e3
keywords:
- 属性表 WDK DirectInput，创建
- 游戏控制器 WDK DirectInput，属性表创建
- 控制面板 WDK DirectInput，属性表创建
- 示例属性表应用程序 WDK DirectInput
- 自定义属性表 WDK DirectInput
- 模板 WDK DirectInput
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7f02d5883325fcda76b9cef2e2e9d803e1d6fbe2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375759"
---
# <a name="creating-your-property-sheet"></a>创建属性表

此示例演示了 DirectInput 的许多方面，并为你自己的自定义属性表提供很好的起点。

## <a name="create-your-own-property-sheet"></a>创建你自己的属性表

从头开始创建自定义属性表是一个相对简单的过程。

1. 创建 GUID 来标识属性页：

   * 使用 GuidGen 工具 （它包含在 Microsoft Windows SDK 中），创建属性页 （无论多少页只有一个） 的 GUID。 在你的特定于应用程序的包含文件中定义此操作。
   * 创建所需的 DllGetClassObject 和 DllCanUnloadNow。
   * 创建 COM ClassFactory Dicpl.h 中定义的实现。
   * 创建用于实现**IDIGamgeCntrlPropSheet**接口。
   * 使用注册表编辑器，将定义的 GUID 添加到我的电脑\\HKEY\_类\_根\\CLSID 项。 然后将密钥 InProcHandler32 和 InProcServer32 添加到你的密钥。
   * 修改 InProcServer32 项来在属性表 DLL 的位置 （默认值） 条目。 一个示例是："C:\\我\_设备\\我\_propertysheet.dll"。 此示例显示了 ProgID 的条目。 这不是必需的但通常用来存储有关驻留在该 GUID，该模块的信息。

2. 创建对话框模板和对话框过程就像任何 Windows 应用程序。

    > [!NOTE]
    > 您可能想要编写为一个窗口，将启动作为独立的对话框页面属性表的测试容器。 此时，你无法将可能具有任何现有控件面板转换为 DirectInput 控制面板。

3. 填充[ **DIGCPAGEINFO** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538484(v=vs.85))并[ **DIGCSHEETINFO** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538492(v=vs.85))结构并的实现中返回该信息[**IDIGameCntrlPropSheet::GetPageInfo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540026(v=vs.85))并[ **IDIGameCntrlPropSheet::GetSheetInfo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540029(v=vs.85))分别。

通过属性表页的新一代**属性表**函数。 此函数的所有行为是都所固有的属性表页。 例如，属性表页反映了其接收的最大对话框模板。 如果用户创建一个页面，并且其关联的模板非常小，这反映了直接对生成的对话框中的大小。

对话框模板仍请务必记住考虑 visual 对齐和居中页面上的控件时。 例如，假设用户在其中创建包含指定要在页面上居中的项的两个页面。 要在居中的一项的宽度; 是 200 对话框单元 (Dlu)另一个是 100 个单位。 在这种情况下后, 一项不位于页面中央。 相反，该控件居中到其模板和其他空白 （或灰色，因为它可能处于） 添加到更窄的页的宽度。 即使不使用其所有，应创建对话框模板的大小相同。 (有关详细信息**属性表**函数中，请参阅 Microsoft Win32 SDK。)
