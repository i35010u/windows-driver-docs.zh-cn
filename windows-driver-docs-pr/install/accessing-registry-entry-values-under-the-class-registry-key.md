---
title: 访问类注册表项下的注册表项值
description: 访问类注册表项下的注册表项值
ms.assetid: 771b5751-db9f-43fa-90d1-1c43918a3a80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3152632f359ff866192e58150fb3fc42ae5e1124
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386047"
---
# <a name="accessing-registry-entry-values-under-the-class-registry-key"></a>访问类注册表项下的注册表项值


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备安装程序类属性](accessing-device-setup-class-properties.md)不具有相应 SPCRP_*Xxx*标识符。 这些属性描述设备安装程序类的特征。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 还支持大部分设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些版本的 Windows 通过使用类注册表项下的相应系统定义的注册表条目值，表示这些属性。 若要保持与这些早期版本的 Windows 兼容性，Windows Vista 和更高版本还支持这些系统定义的注册表条目的值。 但是，应使用属性键来访问这些属性在 Windows Vista 和更高版本上。

系统定义的设备安装程序类属性的列表，请参阅[设备安装程序类属性，请执行不具有相应 SPCRP_Xxx 标识符](https://docs.microsoft.com/previous-versions/ff542250(v=vs.85))。 属性的密钥标识符用于访问在 Windows Vista 和更高版本中的属性按列出的设备安装程序类属性。 与属性键一起提供的信息还包括可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性的相应注册表项值。

有关如何使用属性键来访问在 Windows Vista 和更高版本的设备安装程序类属性的信息，请参阅[访问设备类属性 （Windows Vista 和更高版本）](accessing-device-class-properties--windows-vista-and-later-.md)。

若要访问这些属性在 Windows Server 2003 上的，Windows XP 和 Windows 2000 中，打开类注册表项并使用 Windows 注册表函数来访问注册表条目对应于这些属性的值。

若要检索的句柄设备安装程序类的类注册表项，请调用[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)函数，并提供以下参数值：

-   设置*ClassGuid*为指向标识请求的类注册表项的设备安装程序类的 GUID。

-   设置*samDesired*到 REGSAM 类型化值，该值指定所需的访问权限。

-   设置*标志*DIOCR_INSTALLER 到。

-   设置*MachineName*为指向包含要打开请求的类注册表项的计算机的名称的以 NULL 结尾的字符串。 如果计算机是本地计算机，设置*MachineName*到**NULL**。

-   设置*保留*到**NULL**。

如果此调用[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)成功， **SetupDiOpenClassRegKeyEx**返回请求的句柄。 如果函数调用失败， **SetupDiOpenClassRegKeyEx**将返回 INVALID_HANDLE_VALUE 和调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

检索的句柄类注册表项后，提供对的调用中的句柄[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)并[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)以检索或设置相对应的注册表项值为设备设置类属性。

调用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)函数之后不再需要访问密钥时关闭类注册表项。

 

 





