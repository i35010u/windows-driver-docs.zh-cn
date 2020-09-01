---
title: 自定义交换机功能状态
description: 自定义交换机功能状态
ms.assetid: 2362EE05-9CC9-451D-80D1-C18CC9274BAB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc257264de40b0346f79a4f396834a362a28811
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207605"
---
# <a name="custom-switch-feature-status"></a>自定义交换机功能状态


Hyper-v 平台和 Hyper-v 可扩展交换机接口提供了基础结构，用于获取可扩展交换机的自定义状态信息。 此信息称为 *交换机功能状态* 信息。

通过使用托管对象格式 (MOF) 类定义，将自定义切换功能状态定义注册到 WMI 管理层。 除了定义自定义交换机功能状态定义的属性的结构成员以外，MOF 类还必须包含以下内容：

-   唯一标识自定义交换机功能状态定义的 UUID。

-   唯一标识可扩展交换机扩展的 GUID。 此 GUID 声明为 MOF 类的 **ExtensionId** 限定符，并且必须与扩展的 INF 文件中声明的 **NetCfgInstanceId** 条目的值匹配。

-   描述性类名字符串。 供应商的名称必须包括在字符串中。

下面显示了 MOF 类的一个示例，用于扩展交换机的自定义功能状态定义。

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

可扩展交换机的 MOF 类自定义功能状态定义通过使用 MOF 编译器 ( # A0) 在通用信息模型中注册 (CIM) 存储库。 注册后，MOF 类可通过 PowerShell cmdlet 和基于 WMI 的应用程序进行配置。

下面的示例演示为注册文件 (Fabrikam CustomSwitchData) 的命令，这些命令 \_ 包含用于自定义交换机功能状态定义的 mof 类。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_CustomSwitchData.mof
net start vmms
```

有关如何使用 MOF 编译器的详细信息，请参阅 [编译驱动程序的 MOF 文件](../kernel/compiling-a-driver-s-mof-file.md)。

下面的示例演示如何使用自定义交换机功能状态定义来获取交换机数据。 在此示例中，Fabrikam \_ CUSTOMSWITCHDATA MOF 类用于从名为 "TestSwitch" 的开关获取交换机状态。 Fabrikam "TestSwitch" 上已启用 Fabrikam，Inc. 扩展，返回的状态为123。

```PowerShell
PS C:\> $switchData = Get-VMSwitchExtensionSwitchData -SwitchName TestSwitch -FeatureId B3E57D77-8E95-4977-97DE-524F8DAF03E4
# Output the current value
PS C:\> $switchData$customSwitchData.Data.CurrentStatus
123
```

有关可扩展交换机扩展如何管理交换机功能状态信息的详细信息，请参阅 [管理自定义交换机功能状态信息](managing-custom-switch-feature-status-information.md)。

 

