---
title: 访问类注册表项下的注册表项值
description: 访问类注册表项下的注册表项值
ms.assetid: 771b5751-db9f-43fa-90d1-1c43918a3a80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9570d9debd51e2863a010edd32556ac77a66ce2a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734359"
---
# <a name="accessing-registry-entry-values-under-the-class-registry-key"></a>访问类注册表项下的注册表项值


在 Windows Vista 和更高版本的 Windows 中，[统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括不具有相应 SPCRP_*Xxx*标识符的[设备安装程序类属性](accessing-device-setup-class-properties.md)。 这些属性描述设备安装程序类的特征。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持其中的大多数设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 通过使用类注册表项下的相应系统定义的注册表项值表示这些属性。 为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持这些系统定义的注册表项值。 但是，在 Windows Vista 和更高版本上，你应该使用属性键来访问这些属性。

有关系统定义的设备安装程序类属性的列表，请参阅没有 [相应 SPCRP_Xxx 标识符的设备安装程序类属性](/previous-versions/ff542250(v=vs.85))。 设备安装程序类属性由用于访问 Windows Vista 和更高版本中的属性的属性键标识符列出。 使用属性键提供的信息还包含相应的注册表项值，你可以使用这些值来访问 Windows Server 2003、Windows XP 和 Windows 2000 上的属性。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备安装程序类属性的信息，请参阅 [访问设备类属性 (Windows vista 和更高版本) ](accessing-device-class-properties--windows-vista-and-later-.md)。

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上访问这些属性，请打开类注册表项，并使用 Windows 注册表功能访问对应于这些属性的注册表项值。

若要检索设备安装程序类的类注册表项的句柄，请调用 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 函数并提供以下参数值：

-   将 *ClassGuid* 设置为指向 GUID 的指针，该 GUID 标识所请求的类注册表项的设备安装程序类。

-   将 *samDesired* 设置为 REGSAM 类型的值，该值指定所需的访问权限。

-   将 *标志* 设置为 DIOCR_INSTALLER。

-   将 *MachineName* 设置为指向以 NULL 结尾的字符串的指针，该字符串包含要在其上打开请求的类注册表项的计算机的名称。 如果计算机是本地计算机，请将 *MachineName* 设置为 **NULL**。

-   将 *保留* 设置为 **NULL**。

如果对 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 的此调用成功，则 **SetupDiOpenClassRegKeyEx** 将返回请求的句柄。 如果函数调用失败，则 **SetupDiOpenClassRegKeyEx** 将返回 INVALID_HANDLE_VALUE 并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

检索类注册表项的句柄之后，在对 [RegQueryValueEx](/windows/win32/api/winreg/nf-winreg-regqueryvalueexa) 和 [RegSetValueEx](/windows/win32/api/winreg/nf-winreg-regsetvalueexa) 的调用中提供句柄，以检索或设置与设备安装程序类属性相对应的注册表项值。

调用 [RegCloseKey](/windows/win32/api/winreg/nf-winreg-regclosekey) 函数可在不再需要访问密钥后关闭类注册表项。

