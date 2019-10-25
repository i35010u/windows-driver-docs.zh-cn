---
title: 排查具体的 WMI 问题
description: 排查具体的 WMI 问题
ms.assetid: 966191e7-aec4-4eff-b975-99a6d3eb8d02
keywords:
- WMI WDK 内核，故障排除
- 排查 WMI 问题 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cef8bff1b2760391403a40c5999735fd8f79d74
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836112"
---
# <a name="troubleshooting-specific-wmi-problems"></a>排查具体的 WMI 问题





### <a href="" id="driver-s-wmi-classes-do-not-appear-in-the--root-wmi-namespace"></a>驱动程序的 WMI 类不显示在 \\根\\WMI 命名空间中

1.  使用[wmimofck](using-wmimofck-exe.md)bmf 检查二进制 MOF 文件格式是否正确。 可以在 mofcomp.exe 中找到其他错误消息。

2.  检查[系统事件日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)，以查看驱动程序是否返回了格式不正确的[**WMIREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)数据结构以响应注册请求。

3.  检查驱动程序是否正在返回**WMIREGINFO**结构内的**RegistryPath**和**MofResourceName**的正确值。

4.  如果驱动程序在单独的文件中提供了 MOF 数据，请检查是否正确设置了驱动程序的[MofImagePath](setting-the-mofimagepath-registry-value.md)注册表值。

5.  检查[WMI WDM 提供程序日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)中是否存在错误。

6.  使用[mofcomp.exe](compiling-a-driver-s-mof-file.md)重新编译和重新加载 MOF 文本文件。 例如，命令**mofcomp.exe-N： root/wmi 驱动程序。 mof**将尝试在驱动程序的 mof 文件中重新编译和重新加载任何 mof 数据。 查看 Mofcomp.exe 在 mofcomp.exe 中生成的错误消息。 （请注意，如果 MOF 文件使用预处理器指令（如 **\#定义**），则需要使用已预处理的 MOF 文件，而不是原始源文件。

    **警告**  如果此操作成功，则实际上会向系统注册新的 WMI 类数据。 你将需要删除这些类（例如，通过使用 Wbemtest）来测试是否正确读取了驱动程序的 MOF 数据。

     

7.  如果上一步骤成功，则最可能的问题是**WMIREGINFO**的成员（例如**MofResourceName**）未正确指定。 或者，问题可能是 MOF 文件指定了从不存在的基类派生的类。

8.  如果驱动程序使用动态 MOF 数据（请参阅[实现动态 Mof 数据](implementing-dynamic-mof-data.md)），请检查驱动程序是否正在接收针对 MSWmi\_MOFDATA\_guid GUID 的 WMI IRP 请求，以及是否已成功完成 IRP 并且未记录任何错误。

### <a name="drivers-wmi-properties-or-methods-cannot-be-accessed"></a>无法访问驱动程序的 WMI 属性或方法

1. 使用**wmimofck bmf**检查二进制 MOF 文件格式是否正确。 有关详细信息，请参阅[Using wmimofck](using-wmimofck-exe.md)。

2. 检查系统事件日志中是否有错误。 有关详细信息，请参阅[WMI irp 和系统事件日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)。

3. 检查[WMI WDM 提供程序日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)中是否存在错误。

4. 请确保每次使用 Wbemtest 查询驱动程序的类时，驱动程序都会收到 WMI IRP。 如果不是，则检查 MOF 文件中的指定 GUID 是否与驱动程序所需的 GUID 匹配。 另外，请检查该驱动程序是否正在接收 WMI 注册请求，该请求是否成功，以及驱动程序是否注册了正确的 Guid。

5. 如果驱动程序收到 IRP，请确保 IRP 已成功完成，并且驱动程序返回了正确的**WNODE\_* XXX*** 结构类型。

6. 如果 Wbemtest 返回错误，请单击 "**详细信息**" 按钮，然后查看 "**说明**" 属性以获取错误说明。

7. 对于方法，请检查你的驱动程序是否支持处理[**IRP\_MN\_query\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)和 IRP\_\_\_查询\_[**实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)请求方法的 GUID。 在执行方法之前，WMI 始终会执行这两个请求中的一个。

### <a name="drivers-wmi-events-are-not-being-received"></a>未收到驱动程序的 WMI 事件

1.  检查[系统事件日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)中是否有错误。 例如，如果驱动程序在调用[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)时指定了静态事件名称，但驱动程序未注册任何静态事件名称，则会在系统事件日志中生成一个条目。

2.  检查[WMI WDM 提供程序日志](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)中是否存在错误。

3.  如果驱动程序正在发送事件引用，则在发送事件引用后，驱动程序应立即收到[**IRP\_MN\_QUERY\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)请求。 如果驱动程序没有收到 IRP，则[**WNODE\_事件\_引用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)结构的格式可能不正确。 如果驱动程序收到 IRP，它应以状态状态\_成功完成。

4.  如果驱动程序使用[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)来发送事件或事件引用，请确保正确填写事件结构（ [**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)或**WNODE\_事件\_引用**）。 特别是，如果为静态实例名称注册了事件 GUID，请确保提供正确的实例索引和提供程序 ID。 如果为动态实例名称注册了事件 GUID，请确保在发送事件时包括实例名称。 如果使用**WNODE\_事件\_引用**结构来指定事件，请检查**WNODE**是否与**TargetGuid**匹配。

5.  如果驱动程序使用[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)来发送事件，请确保为*Guid*和*InstanceIndex*参数传递正确的值。

### <a name="changes-in-security-settings-for-wmi-requests-do-not-take-effect"></a>WMI 请求的安全设置更改不会生效

-   卸载并重新加载 WMI WDM 提供程序。 对于使用 WMIREG\_标志注册的 WMI 数据块\_开销较高的标志，只要存在用于该块的使用者，提供程序就会将句柄保持打开状态。 在提供程序关闭句柄之前，新的安全设置将不会生效。 卸载和重新加载提供程序可确保句柄已关闭。 （有关 WMIREG\_标志的详细信息\_昂贵标志，请参阅[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)。）

 

 




