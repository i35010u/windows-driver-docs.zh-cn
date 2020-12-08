---
title: WMI 通用属性页提供程序
description: WMI 通用属性页提供程序
keywords:
- WMI WDK 内核，属性表
- 属性表 WDK WMI
- 泛型属性页提供程序 WDK WMI
- 属性页 WDK WMI
- 属性限定符 WDK WMI
- 设备属性表 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a73ed9f4c938ba2d63172e43a1b68feb1c725d50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782665"
---
# <a name="wmi-generic-property-page-provider"></a>WMI 通用属性页提供程序





在 Windows XP 和更高版本的操作系统上，驱动程序可以通过 WMI 通用属性页提供程序公开其 WMI 类。 提供程序使用每个类声明为类属性创建一个简单的属性页。

### <a name="how-property-qualifiers-determine-the-property-page"></a>属性限定符如何确定属性页

WMI 泛型属性页提供程序使用的控件适用于类中每个属性的数据类型。 以下属性限定符修改所使用的控件类型：

-   **写入**

    可以通过属性页更改带有 **写入** 限定符的属性。 否则，该属性是只读的。

-   **Values** 和 **ValuesMap**

    泛型属性页提供程序使用列表框来表示可能的值。

-   **范围**

    泛型属性页提供程序验证输入的数据是否符合指定范围。

-   **DisplayName**

    泛型属性页提供程序使用此属性限定符的值作为属性的标签。

-   **DisplayInHex**

    如果存在，则该属性值以十六进制显示。

驱动程序编写器应本地化作为字符串的属性限定符。 有关详细信息，请参阅 [本地化 MOF 文件](localizing-mof-files.md) 。

### <a name="enabling-the-generic-property-page-provider"></a>启用泛型属性页提供程序

公开 Wmiprop.dll 要使用的类的每个设备都必须启用 Wmiprop.dll 作为共同安装程序。 为此，请在 " **HKLM \\ System \\ CurrentControlSet \\ Control \\ CoDeviceInstallers** " 注册表项下，为类 GUID 添加一个值项，并添加到 "共同安装程序 *外接* 程序" 部分。 值项的值为 "WmiProp.dll，WmiPropCoInstaller"。

例如：

```cpp
; This section is defined in the Co-installer section, as follows.
; [Co-installer]
; AddReg = CoInstaller_AddReg

[CoInstaller_AddReg] 
HKLM, System\CurrentControlSet\Control\CoDeviceInstallers, ClassGUID,
    0x00010000, "WmiProp.dll, WmiPropCoInstaller"
```

*ClassGUID* 是 WMI 类的 GUID。 有关详细信息，请参阅 [注册类共同安装程序](../install/registering-a-class-co-installer.md) 。

您还必须指定要通过泛型属性提供程序公开的特定 WMI 类。 为此，请将 **WmiConfigClasses** 值输入设置为设备类或设备硬件实例的 " *外接程序" 部分* 中的 WMI 类的逗号分隔列表。

```cpp
; the device class AddReg section.
[device_class_AddReg]
HKR,,"WmiConfigClasses",0x00000000,"class1,class2"

; the device hardware instance AddReg section.
[device_hw_inst_AddReg]
HKR,,"WmiConfigClasses",0x00000000,"class3"
```

有关 INF 文件中的 "*添加注册表" 部分* 的说明，请参阅 [**inf AddReg 指令**](../install/inf-addreg-directive.md)。

Wmiprop.dll 假设每个类只有一个实例。 每个类由属性表上的一个选项卡表示。 使用 **DisplayName** 属性限定符设置选项卡的标题文本。仅当当前存在类的实例时，才会显示类的属性页。 因此，如果设备已删除或未启动，则不会显示这些页面。

 

