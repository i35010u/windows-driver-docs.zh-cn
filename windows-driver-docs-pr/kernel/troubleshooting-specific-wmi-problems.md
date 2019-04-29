---
title: 排查具体的 WMI 问题
description: 排查具体的 WMI 问题
ms.assetid: 966191e7-aec4-4eff-b975-99a6d3eb8d02
keywords:
- WMI WDK 内核故障排除
- 排查 WMI 问题 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1759ae885a46d2e8a45e08e5916ac25ca7723025
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377035"
---
# <a name="troubleshooting-specific-wmi-problems"></a>排查具体的 WMI 问题





### <a href="" id="driver-s-wmi-classes-do-not-appear-in-the--root-wmi-namespace"></a>驱动程序的 WMI 类不显示在\\根\\wmi Namespace

1.  使用[wmimofck](using-wmimofck-exe.md)driver.bmf 来检查二进制的 MOF 文件格式是否正确。 其他错误消息可能位于 mofcomp.log。

2.  检查[系统事件日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)若要查看驱动程序是否能返回格式不正确[ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)到注册请求的响应中的数据结构。

3.  检查驱动程序返回的正确值**RegistryPath**并**MofResourceName**内**WMIREGINFO**结构。

4.  如果该驱动程序提供了其 MOF 数据在单独的文件，检查[MofImagePath](setting-the-mofimagepath-registry-value.md)驱动程序的注册表值是否设置正确。

5.  检查[WMI WDM 提供程序日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)的错误。

6.  使用[Mofcomp](compiling-a-driver-s-mof-file.md)重新编译和重新加载您 MOF 的文本文件。 例如，命令**mofcomp-N： 根/wmi driver.mof**将尝试重新编译并重新加载 driver.mof 文件中的所有 MOF 数据。 检查以查看哪些错误消息 Mofcomp mofcomp.log 中生成。 (请注意，如果你的 MOF 文件使用预处理器指令，如**\#定义**，将需要使用已预处理的 MOF 文件中，而不是原始源代码文件。

    **警告**  如果此操作成功，它实际上注册新的 WMI 类数据与系统。 将需要删除这些类 （例如，使用 Wbemtest，） 来测试是否正确读取驱动程序的 MOF 数据。

     

7.  如果在上一步骤成功，则最可能的问题在于的成员**WMIREGINFO**，如**MofResourceName**，未正确指定。 或者，问题可能是 MOF 文件指定从一个基类，不存在该类派生的类。

8.  如果该驱动程序使用的动态的 MOF 数据 (请参阅[实现动态 MOF 数据](implementing-dynamic-mof-data.md))，检查驱动程序正在接收的 MSWmi 的 WMI IRP 请求\_MofData\_GUID GUID 和完成 IRP记录成功和出现任何错误。

### <a name="drivers-wmi-properties-or-methods-cannot-be-accessed"></a>不能访问驱动程序的 WMI 属性或方法

1. 使用**wmimofck driver.bmf**来检查二进制的 MOF 文件格式是否正确。 有关详细信息，请参阅[使用 wmimofck.exe](using-wmimofck-exe.md)。

2. 检查系统事件日志的错误。 有关详细信息，请参阅[WMI Irp 和系统事件日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)。

3. 检查[WMI WDM 提供程序日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)的错误。

4. 请确保该驱动程序接收 WMI IRP，只要您使用 Wbemtest 查询驱动程序的类。 如果没有，然后检查在 MOF 文件中指定的 GUID 与驱动程序应为 GUID 匹配。 检查驱动程序正在接收的 WMI 注册请求，它取得成功，并且该驱动程序正在注册正确的 Guid。

5. 如果驱动程序接收 IRP，请确保已成功，完成 IRP 和驱动程序返回了正确的类型的**WNODE\_* XXX*** 结构。

6. 如果 Wbemtest 返回错误，请单击**详细信息**按钮，并检查**说明**属性有关的错误说明。

7. 对于方法，检查您的驱动程序支持处理[ **IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)并[ **IRP\_MN\_查询\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)方法的 GUID 的请求。 WMI 将始终执行这些两个请求的一个执行方法之前。

### <a name="drivers-wmi-events-are-not-being-received"></a>未正在接收的驱动程序的 WMI 事件

1.  检查[系统事件日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)的错误。 例如，如果该驱动程序调用时指定静态事件名称[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)但该驱动程序未注册任何静态事件名称，这将生成系统事件日志中的条目。

2.  检查[WMI WDM 提供程序日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)的错误。

3.  如果该驱动程序发送事件引用，该驱动程序应会收到[ **IRP\_MN\_查询\_单一\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)立即请求之后发送的事件引用。 如果该驱动程序不会接收 IRP [ **WNODE\_事件\_引用**](https://msdn.microsoft.com/library/windows/hardware/ff566374)结构可能已格式不正确。 如果驱动程序接收 IRP，它应会完成它并返回状态 STATUS\_成功。

4.  如果驱动程序使用[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)若要发送的事件或事件引用，请确保事件结构 (任一[ **WNODE\_单一\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff566377)或**WNODE\_事件\_引用**) 正确填写。 具体而言，如果事件 GUID 注册的静态实例名称，请确保提供正确的实例索引和提供程序 ID。 如果的事件 GUID 注册的动态实例名称，请确保，将事件发送时，将包括实例名称。 如果使用**WNODE\_事件\_引用**结构指定事件时，请检查**Wnode.Guid**匹配**TargetGuid**。

5.  如果驱动程序使用[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)发送事件，请确保正确的值为传递*Guid*并*InstanceIndex*参数。

### <a name="changes-in-security-settings-for-wmi-requests-do-not-take-effect"></a>在 WMI 请求的安全设置的更改不会生效

-   卸载并重新加载 WMI WDM 提供程序。 WMI 数据块注册 WMIREG\_标志\_昂贵的标志，该提供程序使句柄打开到数据块，只要有该块的使用者。 提供程序关闭句柄，新的安全设置才会生效。 卸载并重新加载提供程序可确保在关闭此句柄。 (有关 WMIREG\_标志\_昂贵的标志，请参阅[ **WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)。)

 

 




