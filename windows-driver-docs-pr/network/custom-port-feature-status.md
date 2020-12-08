---
title: 自定义端口功能状态
description: 自定义端口功能状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4d48448eff7e7d17a2cac780b0025546a7d2e21
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794653"
---
# <a name="custom-port-feature-status"></a>自定义端口功能状态


Hyper-v 平台和 Hyper-v 可扩展交换机接口提供了基础结构，用于获取可扩展交换机端口的自定义状态信息。 此信息称为 *端口功能状态* 信息。

Hyper-v 可扩展交换机端口属性的自定义功能状态定义通过使用 (MOF) 类定义的托管对象格式注册到 WMI 管理层。 除了定义自定义端口功能状态定义的属性的结构成员以外，MOF 类还必须包含以下内容：

-   用于唯一标识自定义端口功能状态定义的 UUID。

-   唯一标识可扩展交换机扩展的 GUID。 此 GUID 声明为 MOF 类的 **ExtensionId** 限定符，并且必须与扩展的 INF 文件中声明的 **NetCfgInstanceId** 条目的值匹配。

-   描述性类名字符串。 供应商的名称必须包括在字符串中。

下面显示了 MOF 类的一个示例，用于扩展交换机端口的自定义功能状态定义。

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

端口的自定义功能状态定义的 MOF 类通过使用 MOF 编译器 ( # A0) 在通用信息模型中注册 (CIM) 存储库。 注册后，MOF 类可通过 PowerShell cmdlet 和基于 WMI 的应用程序进行配置。

下面的示例演示为注册一个文件 (Fabrikam CustomPortData) ，这些命令必须 \_ 包含自定义端口功能状态定义的 mof 类。

```PowerShell
net stop vmms
mofcomp -N:root\virtualization\v2 Fabrikam_CustomPortData.mof
net start vmms
```

有关如何使用 MOF 编译器的详细信息，请参阅 [编译驱动程序的 MOF 文件](../kernel/compiling-a-driver-s-mof-file.md)。

下面的示例演示如何使用自定义端口功能状态定义来获取端口数据。 在此示例中，Fabrikam \_ CUSTOMPORTDATA MOF 类用于从名为 "TestVm" 的 hyper-v 分区获取端口状态。 Fabrikam "TestSwitch" 上已启用 Fabrikam，Inc. 扩展，返回的状态为123。

```PowerShell
PS C:\> $portData = Get-VMSwitchExtensionPortData -VmName TestVm -FeatureId DAA0B7CC-74DB-41ef-8354-7002F9FA463E
# Output the current value
PS C:\> $portData.Data.CurrentStatus
123
```

有关可扩展交换机扩展如何管理端口功能状态信息的详细信息，请参阅 [管理自定义端口功能状态信息](managing-custom-port-feature-status-information.md)。

 

