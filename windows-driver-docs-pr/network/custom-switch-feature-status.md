---
title: 自定义开关功能状态
description: 自定义开关功能状态
ms.assetid: 2362EE05-9CC9-451D-80D1-C18CC9274BAB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5efba9e9f5e2dbb0c7731998a1164bdc74feaa34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522967"
---
# <a name="custom-switch-feature-status"></a>自定义开关功能状态


HYPER-V 平台和 HYPER-V 可扩展交换机接口提供了基础结构，以获取有关可扩展交换机的自定义状态信息。 此信息被称为*切换功能状态*信息。

通过使用托管的对象格式 (MOF) 的类定义，可将自定义开关功能状态定义注册与 WMI 管理层。 除了定义自定义开关功能状态定义的属性的结构成员、 MOF 类还必须包含以下：

-   一个唯一标识的自定义开关功能状态定义的 UUID。

-   用于唯一标识此可扩展交换机扩展的 GUID。 此 GUID 声明为**ExtensionId**限定符 MOF 的类，并且必须匹配的值**NetCfgInstanceId**扩展的 INF 文件中声明的项。

-   描述性类名称字符串。 必须在字符串中包含的供应商的名称。

下面演示的可扩展交换机的自定义功能状态定义 MOF 类的一个示例。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic,
  UUID("B3E57D77-8E95-4977-97DE-524F8DAF03E4"),
  ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
  Provider("VmmsWmiInstanceAndMethodProvider"), 
  InterfaceVersion("1"),
  InterfaceRevison("0"),
  Locale(0x409),
  Description(
   "Fabricam, Inc. Switch custom feature status description.") : Amended,
  DisplayName("Fabricam, Inc. Switch custom feature status friendly name.") : Amended]
class Fabrikam_CustomSwitchData  : Msvm_EthernetSwitchFeatureSettingData{
    [ Read,
       Write,
       WmiDataId(1),
       InterfaceVersion("1"),
       InterfaceRevision("0"),
       Description(
         "The current status of custom feature on this switch.") : Amended]
     uint32 CurrentStatus = 0 ;
};
```

使用 MOF 编译器 (Mofcomp.exe) 的通用信息模型 (CIM) 存储库中注册的可扩展交换机的自定义功能状态定义的 MOF 类。 在注册后，可以通过 PowerShell cmdlet 和基于 WMI 的应用程序配置 MOF 类。

下面的示例演示必须输入要注册文件的命令 (Fabrikam\_CustomSwitchData.mof)，其中包含自定义开关功能状态定义 MOF 类。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_CustomSwitchData.mof
net start vmms
```

有关如何使用 MOF 编译器的详细信息，请参阅[编译的驱动程序的 MOF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542012)。

下面的示例演示如何使用自定义开关功能状态定义来获取开关的数据。 在此示例中，Fabrikam\_CustomSwitchData MOF 类用于从名为"TestSwitch"的交换机获取切换状态。 Fabrikam，Inc.扩展 vSwitch"TestSwitch"上已启用且正在返回 123 的状态。

```PowerShell
PS C:\> $switchData = Get-VMSwitchExtensionSwitchData -SwitchName TestSwitch -FeatureId B3E57D77-8E95-4977-97DE-524F8DAF03E4
# Output the current value
PS C:\> $switchData$customSwitchData.Data.CurrentStatus
123
```

有关详细信息如何可扩展交换机扩展管理交换机功能的状态信息，请参阅[管理自定义切换功能的状态信息](managing-custom-switch-feature-status-information.md)。

 

 





