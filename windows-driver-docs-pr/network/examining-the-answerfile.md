---
title: 检查应答文件
description: 检查应答文件
ms.assetid: 42d58786-e50c-43c2-b673-5f23c9930ee7
keywords:
- 测试网络组件升级 WDK
- 应答文件 WDK 网络
- 升级测试 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 672e95f384b9ddce84889598996da366ba132e9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542142"
---
# <a name="examining-the-answerfile"></a>检查应答文件





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

正在升级的系统上将立即显示"安装程序是复制文件"进度栏之前，创建应答文件。 NetSetup 和供应商提供的网络迁移 Dll 在应答文件中创建的节，然后编写对这些部分期间 Winnt32 条目升级阶段。

可以通过复制 c： 检查 AnswerFile\\$win\_nt$。 ~ bt\\winnt.sif 到 %TEMP%。 在复制应答文件后，可以单击**取消**取消文件复制。 无需等待，直到文件复制完成。

下表列出了应答文件和每个部分包含与网络组件相关的相应条目中的顶级部分：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">部分</th>
<th align="left">包含的条目</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NetAdapters</strong></p></td>
<td align="left"><p>网络适配器，包括 ISDN 适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AsyncAdapters</strong></p></td>
<td align="left"><p>异步适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NetProtocols</strong></p></td>
<td align="left"><p>网络协议</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NetServices</strong></p></td>
<td align="left"><p>网络服务</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NetClients</strong></p></td>
<td align="left"><p>网络客户端</p></td>
</tr>
</tbody>
</table>

 

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

有关在 Winnt32 阶段过程中发现每个网络组件，NetSetup 到应答文件的适当顶级部分写入一个条目。 每个条目具有以下格式：

params.*postupgrade-ID*

*Postupgrade ID*条目是 Windows 2000 或更高版本 NetSetup 从组件 netmap.inf 文件中获取的设备 ID。

每个条目应答文件中指定该组件的参数部分的名称。 例如，如果组件的 Windows 2000 或更高版本的设备 ID 是 netadapter2 中的项**NetAdapters**部分**params.netadapter2**。 顶级部分和应答文件中的参数部分不可见的网络迁移 DLL。

NetSetup 将扩展添加到组件的参数部分名称， **OemSection**来创建*OEM 部分*组件名称。 例如，如果参数部分的一个组件是 params.netadapter2， *OEM 部分*名称的组件是 params.netadapter2.OemSection。 将传递 NetSetup *OEM 部分*名称用作*szSectionName*参数[ **DoPreUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545634)函数提供的网络迁移 DLL 组件。 **DoPreUpgradeProcessing**函数调用[ **NetUpgradeAddSection** ](https://msdn.microsoft.com/library/windows/hardware/ff559063)函数来创建*OEM 部分*组件在应答文件。 **DoPreUpgradeProcessing**函数然后调用[ **NetUpgradeAddLineToSection** ](https://msdn.microsoft.com/library/windows/hardware/ff559059)添加到特定于组件的信息*OEM 部分*.

应答文件的以下部分显示的部分和条目的网络适配器的 Windows 2000 或更高版本的设备 ID 是**adapter2**:

```INF
[NetAdapter]              ;top-level adapters section
adapter2=params.adapter2      ;entry for adapter2
[params.adapter2]          ;parameters section for adapter2
InfID=adapter2            ;Windows 2000 or later device ID
OemSection=params.adapter2.OemSection  ;Identifies the OemSection

[params.adapter2.OemSection]  ;OemSection created by migration DLL
InfToRunAfterInstall="", adapter2.SectionToRun ;Written by DLL

[adapter2.SectionToRun]      ;Section created by migration DLL
AddReg=adapter2.SectionToRun.AddReg ;AddReg directive

[adapter2.SectionToRun.AddReg] ;AddReg section created by DLL
HKR,0\0,IsdnPhoneNumber,0,"111-1111" ;AddReg entries written by DLL
HKR,0\1,IsdnPhoneNumber,0,"222-2222"
HKR,0\0,IsdnSpid,0,"111"
HKR,0\1,IsdnSpid,0,"222"
HKR,0,IsdnSwitchType,0x00010001,1
```

在 GUI 模式阶段，NetSetup 检测[ **InfToRunAfterInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff559059)密钥编写的 DLL 在迁移到**params.adapter2.OemSection**的示例应答文件。 按此键的指引，处理 NetSetup **adapter2。SectionToRun.AddReg**部分。 **Adapter2。SectionToRun.AddReg**部分指导 NetSetup 将参数值添加到在 Windows 2000 或更高版本的注册表中 adapater2 的实例键。 DLL 读取 adapter2 迁移升级的 Winnt32 阶段的注册表的升级前的参数值应匹配这些参数值。

如果网络迁移 DLL 是要在 GUI 模式阶段，加载其[ **DoPreUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545634)函数设置 NUA\_负载\_POST\_升级标志。 此标志会导致 NetSetup 编写**OemDllToLoad**进入到应答文件中的组件的参数部分。 **OemDllToLoad**条目会导致 NetSetup 加载组件迁移 DLL 在 GUI 模式阶段。

下面的示例演示的应答文件部分和条目的组件的网络在 GUI 模式阶段期间加载 DLL 的迁移：

```INF
[NetAdapter]              ;top-level adapters section
adapter2=params.adapter2      ;entry for adapter2
[params.adapter2]          ;parameters section for adapter2
InfID=adapter2            ;postupgrade device ID
OemSection=params.adapter2.OemSection;Identifies the OemSection
OemDllToLoad=c:\temp\oem0001\migration.dll
```

请注意**OemDllToLoad**中的条目**params.adapter2**部分。 另请注意，迁移 DLL 未创建**params.adapter2.OemSection**。 当迁移 DLL 要在 GUI 模式阶段期间加载时，它通常不会写入**InfToRunAfterInstall**密钥应答文件。 DLL 执行安装后升级报告中。因此，它不需要创建*Oem 部分*包含 NetSetup 在 GUI 模式阶段期间执行的指令的名称。

 

 





