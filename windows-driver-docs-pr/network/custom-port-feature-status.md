---
title: 自定义端口功能状态
description: 自定义端口功能状态
ms.assetid: 87E88302-6FEA-4D71-A80D-E7AD6D42C0BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6b3f0c646bf3080e0bdc11b7af398513eba72c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374874"
---
# <a name="custom-port-feature-status"></a>自定义端口功能状态


HYPER-V 平台和 HYPER-V 可扩展交换机接口提供了基础结构，以获取有关可扩展交换机端口的自定义状态信息。 此信息被称为*端口功能状态*信息。

自定义功能的 HYPER-V 可扩展交换机端口属性的状态定义使用 WMI 管理层使用注册的托管的对象格式 (MOF) 的类定义。 除了定义自定义端口功能状态定义的属性的结构成员、 MOF 类还必须包含以下：

-   一个唯一标识的自定义端口功能状态定义的 UUID。

-   用于唯一标识此可扩展交换机扩展的 GUID。 此 GUID 声明为**ExtensionId**限定符 MOF 的类，并且必须匹配的值**NetCfgInstanceId**扩展的 INF 文件中声明的项。

-   描述性类名称字符串。 必须在字符串中包含的供应商的名称。

下面显示了一个可扩展交换机端口的自定义功能状态定义 MOF 类的一个示例。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic,
  UUID("DAA0B7CC-74DB-41ef-8354-7002F9FA463E"),
  ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
  Provider("VmmsWmiInstanceAndMethodProvider"), 
  InterfaceVersion("1"),
  InterfaceRevison("0"),
  Locale(0x409),
  Description("Fabricam, Inc. port custom feature status description.") : Amended,
  DisplayName("Fabricam, Inc.port custom feature status friendly name.") : Amended]
class Fabrikam_CustomPortData  : Msvm_EthernetPortData {
    [ Read,
       Write,
       WmiDataId(1),
      InterfaceVersion("1"),
      InterfaceRevision("0"),
       Description(
         "The current status of custom feature on this port.") : Amended]
     uint32 CurrentStatus = 0 ;
};
```

使用 MOF 编译器 (Mofcomp.exe)，可将端口的自定义功能状态定义的 MOF 类注册公共信息模型 (CIM) 存储库中。 在注册后，可以通过 PowerShell cmdlet 和基于 WMI 的应用程序配置 MOF 类。

下面的示例演示必须输入要注册文件的命令 (Fabrikam\_CustomPortData.mof)，其中包含自定义端口功能状态定义 MOF 类。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_CustomPortData.mof
net start vmms
```

有关如何使用 MOF 编译器的详细信息，请参阅[编译的驱动程序的 MOF 文件](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)。

下面的示例演示如何使用自定义端口功能状态定义来获取端口的数据。 在此示例中，Fabrikam\_CustomPortData MOF 类用于从 HYPER-V 分区名为"TestVm"获取端口状态。 Fabrikam，Inc.扩展 vSwitch"TestSwitch"上已启用且正在返回 123 的状态。

```PowerShell
PS C:\> $portData = Get-VMSwitchExtensionPortData -VmName TestVm -FeatureId DAA0B7CC-74DB-41ef-8354-7002F9FA463E
# Output the current value
PS C:\> $portData.Data.CurrentStatus
123
```

有关详细信息如何可扩展交换机扩展管理端口功能的状态信息，请参阅[管理自定义端口功能状态信息](managing-custom-port-feature-status-information.md)。

 

 





