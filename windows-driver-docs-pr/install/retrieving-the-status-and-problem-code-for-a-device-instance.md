---
title: 检索设备实例的状态和问题代码
description: 检索设备实例的状态和问题代码
ms.assetid: 22ca9ac2-fe67-427d-a6e4-f1d9cbbede52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64149e27e36ac13ef09df63b4545069a39f1865f
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558406"
---
# <a name="retrieving-the-status-and-problem-code-for-a-device-instance"></a>检索设备实例的状态和问题代码


在 Windows Vista 和更高版本的 Windows 中，[统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包括[设备状态属性和问题代码属性](https://docs.microsoft.com/previous-versions/ff542254(v=vs.85))。 统一设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 不支持统一属性模型的属性键，也不支持表示这些属性的相应注册表项值。 但是，可以通过调用[**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)函数来检索相应的信息。 为了保持与早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持**CM_Get_DevNode_Status**。 但是，你应该使用统一设备属性模型的属性键来访问设备驱动程序属性。

设备驱动程序属性由用于访问 Windows Vista 和更高版本中的属性的属性键标识符列出。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备驱动程序属性的信息，请参阅[访问设备实例属性（Windows vista 和更高版本）](accessing-device-instance-properties--windows-vista-and-later-.md)。

若要访问 Windows Server 2003、Windows XP 和 Windows 2000 上的设备实例的状态和问题代码，请调用**CM_Get_DevNode_Status**并提供以下参数：

-   将*pulStatus*设置为指向 ULONG 类型值的指针，该类型的值接收为设备实例设置的状态位标志。 Status 值可以是在*Cfg*中定义前缀为 "DN_" 的任何位标志的组合。

-   将*pulProblemNumber*设置为指向 ULONG 类型值的指针，该类型的值接收为设备实例设置的问题号。 问题编号是在*Cfg*中定义的前缀为 "CM_PROB_" 的常量之一。 仅当在*pulStatus*中设置 DN_HAS_PROBLEM 时， **CM_Get_DevNode_Status**才设置问题号。

-   将*dnDevInst*设置为要为其检索状态和问题代码的设备的设备实例句柄。

-   将*ulFlags*设置为零。

如果对**CM_Get_DevNode_Status**的调用成功，则**CM_Get_DevNode_Status**会检索设备实例的请求状态和问题代码，并返回 CR_SUCCESS。 如果函数调用失败， **CM_Get_DevNode_Status**将返回一个错误代码，其中包含*Cfgmgr32*中定义的前缀 "CR_"。

## <a name="see-also"></a>另请参阅
 
* [**DEVPKEY_Device_ProblemCode**](devpkey-device-problemcode.md)
* [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

