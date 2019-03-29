---
title: WMI 通用属性页提供程序
description: WMI 通用属性页提供程序
ms.assetid: 44cfafdf-c8e2-4175-95e5-3c5d03dc206d
keywords:
- WMI WDK 内核，属性表
- 属性表 WDK WMI
- 泛型属性页提供程序 WDK WMI
- 属性页 WDK WMI
- 属性限定符 WDK WMI
- 设备属性表 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eab65252dafb71934012a8abc7a7ac397c234249
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562890"
---
# <a name="wmi-generic-property-page-provider"></a>WMI 通用属性页提供程序





在 Windows XP 和更高版本操作系统上，驱动程序可以公开它们通过 WMI 泛型属性页提供程序的 WMI 类。 提供程序使用每个类声明为创建一个简单的属性页类属性。

### <a name="how-property-qualifiers-determine-the-property-page"></a>属性限定符如何确定属性页

WMI 通用的属性页提供程序类中使用适用于每个属性的数据类型的控件。 以下属性限定符修改控件使用的类型：

-   **编写**

    具有的属性**编写**限定符可通过属性页进行更改。 否则该属性是只读的。

-   **值**和**ValuesMap**

    泛型属性页提供程序使用列表框来表示可能的值。

-   **Range**

    泛型属性页提供程序来验证输入的数据符合指定的范围。

-   **DisplayName**

    泛型属性页提供程序使用此属性的限定符的值作为标签的属性。

-   **DisplayInHex**

    如果存在，是以十六进制形式显示的属性值。

驱动程序编写人员应本地化属性限定符的字符串。 请参阅[本地化 MOF 文件](localizing-mof-files.md)有关详细信息。

### <a name="enabling-the-generic-property-page-provider"></a>启用通用的属性页提供程序

用于公开类以供 Wmiprop.dll 每个设备必须启用 Wmiprop.dll 作为辅助安装程序。 若要执行此操作，请增加了以下步骤向共同安装程序*添加注册表部分*： 添加的类 GUID 的值项下**HKLM\\系统\\CurrentControlSet\\控件\\CoDeviceInstallers**注册表项。 值项的值是"WmiProp.dll，WmiPropCoInstaller"。

例如：

```cpp
; This section is defined in the Co-installer section, as follows.
; [Co-installer]
; AddReg = CoInstaller_AddReg

[CoInstaller_AddReg] 
HKLM, System\CurrentControlSet\Control\CoDeviceInstallers, ClassGUID,
    0x00010000, "WmiProp.dll, WmiPropCoInstaller"
```

*ClassGUID*是 WMI 类的 GUID。 请参阅[注册类共同安装程序](https://msdn.microsoft.com/library/windows/hardware/ff549801)有关详细信息。

您还必须指定要通过泛型属性提供程序公开的特定 WMI 类。 若要执行此操作，设置**WmiConfigClasses**中的值的项都必须是一列以逗号分隔的 WMI 类*添加注册表部分*的设备类或设备硬件实例。

```cpp
; the device class AddReg section.
[device_class_AddReg]
HKR,,"WmiConfigClasses",0x00000000,"class1,class2"

; the device hardware instance AddReg section.
[device_hw_inst_AddReg]
HKR,,"WmiConfigClasses",0x00000000,"class3"
```

请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)有关的说明*添加注册表部分*INF 文件中。

Wmiprop.dll 假定每个类的一个实例。 由属性表上的选项卡表示每个类。 使用**DisplayName**要设置的选项卡的标题文本的属性限定符。如果当前类的实例，才会显示一个类的属性页。 因此，如果设备已删除或未启动，不显示这些页。

 

 




