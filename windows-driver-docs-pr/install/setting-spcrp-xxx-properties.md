---
title: 设置 SPCRP_Xxx 属性
description: 设置 SPCRP_Xxx 属性
ms.assetid: efb0d02e-ec4c-4c1b-900b-c81f504d2919
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dcec79183394c92371b9298d37896d5e477c0cc
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095989"
---
# <a name="setting-spcrp_xxx-properties"></a>设置 SPCRP_Xxx 属性


在 Windows Vista 和更高版本的 Windows 中，[统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持与*setupapi.log*中定义的 SPCRP_Xxx 标识符对应的[设备安装程序类属性](/previous-versions/ff542239(v=vs.85))。 这些属性描述设备安装程序类的特征。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持其中的大多数设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 使用 SPCRP_*Xxx* 标识符来表示设备安装程序类属性。 为了保持与早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持使用 SPCRP_*Xxx* 标识符来访问设备安装程序类属性。 但是，你应该使用统一设备属性模型的属性键来访问设备安装程序类属性。

有关系统定义的设备安装程序类属性的列表，请参阅 [与 SPCRP_Xxx 标识符对应的设备安装程序类属性](/previous-versions/ff542245(v=vs.85))。 设备安装程序类属性由用于访问 Windows Vista 和更高版本中的属性的属性键标识符列出。 使用属性键提供的信息还包括相应的 SPCRP_*Xxx* 标识符，可用于访问 windows Server 2003、windows XP 和 windows 2000 上的属性。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备安装程序类属性的信息，请参阅 [访问设备类属性 (Windows vista 和更高版本) ](accessing-device-class-properties--windows-vista-and-later-.md)。

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上设置设备安装程序类属性，请调用 [**SetupDiSetClassRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya) 并提供以下参数值：

-   将 *ClassGuid* 设置为指向表示要为其设置属性的设备安装程序类的 GUID 的指针。

-   将 *属性* 设置为要设置前缀 "SPCRP_" 的属性的标识符。

-   将 *PropertyBuffer* 设置为指向包含属性值的缓冲区的指针。

-   将 *PropertyBufferSize* 设置为正确数据的大小（以字节为单位）。

-   将 *MachineName* 设置为计算机名称。

-   将 *保留* 设置为 **NULL**。

如果对 [**SetupDiSetClassRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya) 的此调用成功，则 **SetupDiSetClassRegistryProperty** 将设置设备安装程序类属性并返回 **TRUE**。 如果函数调用失败， **SetupDiSetClassRegistryProperty** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回最近记录的错误代码。

 

