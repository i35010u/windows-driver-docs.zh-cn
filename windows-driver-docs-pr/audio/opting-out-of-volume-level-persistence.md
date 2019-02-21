---
title: 选择退出卷级持久性
description: 选择退出卷级持久性
ms.assetid: e96533be-25e8-49ae-8e56-7105dfa92b5a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d5742006ae28e4a5db2166e674197e4f4ab0f29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541444"
---
# <a name="opting-out-of-volume-level-persistence"></a>选择退出卷级持久性


默认情况下重新启动计算机时保留卷级别设置。 此默认的系统行为被称为*卷持久性*。 如果不想要在计算机重启后由系统维护的卷级别，可以在音频的适配器，安装时使用 INF 文件，可以选择不使用默认的系统行为。

您可能希望您的驱动程序可以选择不使用卷暂留，如果您的驱动程序必须在其自己的注册表缓存并且在驱动程序加载硬件本身上设置的级别。

若要选择退出使用 INF 文件的卷暂留，请使用[ **AddProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff546318)注册表指令设置主键的值\_AudioDevice\_DontPersistControls 注册表为"1"的键。 默认值为"0"。

下面的 INF 文件片断演示如何选择退出卷持久性：

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

**请注意**  前面的 INF 文件片段中，仅显示**版本**部分以及与相关的各部分[ **AddProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff546318)指令。

 

**%Mfgname%= CompanyName**行中的条目**制造商**部分引用**CompanyName**部分的位置的模型和硬件 ID (hw id) 的音频的适配器提供了。 本部分中的 INF 文件，其中提供模型和硬件 id 信息，称为*模型部分*。 部分的实际标题是用户定义和在前面的示例很**CompanyName**。 INF 文件的模型部分的详细信息，请参阅[ **INF 模型部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)。

模型部分中，引用有关其他安装程序必须将复制的 INF 文件提供了信息的设备驱动程序安装 (DDInstall) 部分。 本部分中的实际标题是用户定义和在前面的示例很**HdAudModel**。 **需求 = KS。注册...** 行条目提供有关安装程序必须从其检索的 INF 文件内的特定部分数据的信息安装

**HdAudModel**部分还包含对 AddReg 和 AddProperty 部分的引用。 安装程序从 AddReg 以及 AddProperty 分别设置注册表项和设备属性中检索数据。 此处引用的 AddProperty 部分是**HdAudModel.AddProperty**并使用以下格式提供有关设备属性的信息：

{*属性类别 guid*}，*属性 pid*，*类型*， \[*标志*\]， *值*

**HdAudModel**部分显示了第一个注释掉的两个行项。已被注释掉的行项设置的值将设备属性设为"1。 未被注释掉的行项是安装程序读取。 此行条目会导致值的设备属性设置为"0。 当此设备属性设置为"0"时，选择弃用卷持久性的音频设备。

有关 AddProperty 指令的详细信息，请参阅[ **INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)。

在前面的 INF 文件片段中的属性类别 GUID 和属性 ID 对应的属性名称是主键\_AudioDevice\_DontPersistControls。

 

 




