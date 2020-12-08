---
title: 选择退出音量级别持久性
description: 选择退出音量级别持久性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a72a8e9d1eb33c36847986255c352cb101dff22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800971"
---
# <a name="opting-out-of-volume-level-persistence"></a>选择退出音量级别持久性


默认情况下，当你重新启动计算机时，会保留卷级别设置。 此默认系统行为称为 " *卷持久性*"。 如果你不希望系统在计算机重新启动之后维护卷级别，则可以在安装音频适配器时使用 INF 文件来选择不使用默认系统行为。

如果驱动程序有自己的注册表缓存，并在驱动程序加载时设置硬件本身的级别，则可能希望驱动程序选择退出卷暂留。

若要选择退出使用 INF 文件的卷暂留，请使用 [**AddProperty**](../install/inf-addproperty-directive.md) 注册表指令将 PKEY \_ AudioDevice DontPersistControls 注册表项的值设置 \_ 为 "1"。 默认值为 "0"。

以下 INF 文件片段显示了如何选择不保留卷持久性：

```inf
 
;; INF file fragment to show how to use AddProperty
;; to opt out of volume persistence
;;
[Version]
Signature = "$CHICAGO$"
Class = MEDIA
ClassGUID = {...}
...
[Manufacturer]
%MfgName% = CompanyName
...
[CompanyName]
%DeviceDescription% = HdAudModel, hw-id
;; ... other device models listed here

[HdAudModel]
Include=ks.inf, wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
CopyFiles = HdAudModel.CopyList, HdAudProp.CopyList, HdAudShortCut.CopyList
AddReg = HdAudModel.AddReg, HdAudProp.AddReg, HdAudShortCut.AddReg, HdAudBranding.AddReg
AddProperty = HdAudModel.AddProperty
...
[HdAudModel.AddProperty]
;; {F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},2,7,,0
{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},2,7,,1
...
[Strings]
MfgName = "My Company Name Inc"
DeviceDescription = "My WDM device driver"
```

**注意**  上述 INF 文件片段只显示 **版本** 部分以及与 [**AddProperty**](../install/inf-addproperty-directive.md) 指令相关的部分。

 

**制造商** 部分中的 **% MfgName% = 公司名称** 行条目引用了 "**公司名称**" 部分，其中提供了) 音频适配器的型号和硬件 id (。 此部分位于 INF 文件中，其中提供了模型和 hw id 信息，称为 "模型" *部分*。 部分的实际标题是用户定义的，在前面的示例中，它是 **公司名称**。 有关 INF 文件的型号部分的详细信息，请参阅 [**Inf 型号部分**](../install/inf-models-section.md)。

模型部分反过来引用设备驱动程序安装 (DDInstall) 部分，其中提供了有关安装程序必须复制的其他 INF 文件的信息。 本部分的实际标题是用户定义的，在前面的示例中，它是 **HdAudModel**。 **需求 = KS。注册 ...** 行条目提供有关 INF 文件中特定部分的信息，安装程序必须从这些部分中检索要安装的数据

**HdAudModel** 节还包含对 AddReg 和 AddProperty 部分的引用。 安装程序将从 AddReg 和 AddProperty 中检索数据，以便分别设置注册表项和设备属性。 此处引用的 AddProperty 节为 **HdAudModel. AddProperty** ，它使用以下格式来提供有关设备属性的信息：

{*property-category-guid*}，*属性-pid*， *type*， \[ *flags* \] ， *value*

**HdAudModel** 部分显示两个行条目，其中第一个条目已注释掉。注释掉的行条目会将设备属性的值设置为 "1"。 未注释掉的行项是安装程序读取的行项。 此行项使设备属性的值设置为 "0"。 如果此设备属性设置为 "0"，则音频设备将会退出卷暂留。

有关 AddProperty 指令的详细信息，请参阅 [**INF AddProperty 指令**](../install/inf-addproperty-directive.md)。

与前面 INF 文件片段中的属性类别 GUID 和属性 ID 相对应的属性名称为 PKEY \_ AudioDevice \_ DontPersistControls。

 

