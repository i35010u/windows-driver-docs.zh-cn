---
title: 检查应答文件
description: 检查应答文件
ms.assetid: 42d58786-e50c-43c2-b673-5f23c9930ee7
keywords:
- 测试网络组件升级 WDK
- AnswerFile WDK 网络
- 升级测试 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7940952c04e9c61c163d5bf53bdbb9a399244613
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209333"
---
# <a name="examining-the-answerfile"></a>检查应答文件





**注意**   Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

紧跟在要升级的系统上显示 "安装程序正在复制文件" 进度栏之前，会创建 AnswerFile。 NetSetup 和供应商提供的网络迁移 Dll 会在 AnswerFile 中创建节，然后在 Winnt32.exe 升级阶段向这些部分写入条目。

可以通过将 c： \\ $win \_ nt $. ~ bt \\ winnt.sif 复制到% TEMP% 来检查 AnswerFile。 复制 AnswerFile 后，可以单击 " **取消** " 以取消文件复制。 无需等到文件复制完成。

下表列出了 AnswerFile 中的顶级部分，并列出了与网络组件相关的每个部分中的相应条目：

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

 

**请注意**，  **NetClient**组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。

 

对于它在 Winnt32.exe 阶段找到的每个网络组件，NetSetup 将向 AnswerFile 的适当顶级部分写入一个条目。 每个条目均具有以下格式：

化.*postupgrade-ID*

*Postupgrade*条目是从组件的 netmap 文件中 NetSetup 获取的 Windows 2000 或更高版本的设备 ID。

每个条目指定 AnswerFile 中该组件的参数部分的名称。 例如，如果组件的 Windows 2000 或更高版本的设备 ID 为 netadapter2，则 **NetAdapters** 节中的条目为 **netadapter2**。 AnswerFile 中的顶级部分和参数部分对网络迁移 DLL 不可见。

对于组件的参数部分名称，NetSetup 添加了 extension **OemSection** ，以创建组件的 *OEM 部分* 名称。 例如，如果组件的参数部分是 netadapter2，则该组件的 *OEM 节* 名称为 Netadapter2. OemSection。 NetSetup 将 *OEM 节* 名称作为 *szSectionName* 参数传递给组件的网络迁移 DLL 提供的 [**DoPreUpgradeProcessing**](/previous-versions/windows/hardware/network/ff545634(v=vs.85)) 函数。 **DoPreUpgradeProcessing**函数调用[**NetUpgradeAddSection**](/previous-versions/windows/hardware/network/ff559063(v=vs.85))函数来创建 AnswerFile 中组件的*OEM 部分*。 然后， **DoPreUpgradeProcessing** 函数调用 [**NetUpgradeAddLineToSection**](/previous-versions/windows/hardware/network/ff559059(v=vs.85)) ，将特定于组件的信息添加到 *OEM 部分*。

AnswerFile 的以下部分显示了其 Windows 2000 或更高版本的设备 ID 为 **adapter2**的网络适配器的部分和条目：

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

在 GUI 模式阶段，NetSetup 将迁移 DLL 写入的 [**InfToRunAfterInstall**](/previous-versions/windows/hardware/network/ff559059(v=vs.85)) 密钥检测到示例 AnswerFile 的 **adapter2. OemSection** 。 按照此键的指示，NetSetup 将处理 **adapter2。SectionToRun. AddReg** 部分。 **Adapter2。SectionToRun AddReg**部分指导 NetSetup 将参数值添加到 Windows 2000 或更高版本的注册表中的 adapater2's 实例键。 在升级 Winnt32.exe 阶段，这些参数值应与迁移 DLL 从中读取注册表的 preupgrade 参数值匹配。

如果在 GUI 模式阶段要加载网络迁移 DLL，则其 [**DoPreUpgradeProcessing**](/previous-versions/windows/hardware/network/ff545634(v=vs.85)) 函数将设置 NUA \_ 负载 \_ \_ 升级后标志。 此标志会导致 NetSetup 将 **OemDllToLoad** 条目写入 AnswerFile 中的组件 parameters 节。 **OemDllToLoad**条目导致 NETSETUP 在 GUI 模式阶段加载组件的迁移 DLL。

以下示例显示了在 GUI 模式阶段，为其网络迁移 DLL 加载的组件的 AnswerFile 部分和条目：

```INF
[NetAdapter]              ;top-level adapters section
adapter2=params.adapter2      ;entry for adapter2
[params.adapter2]          ;parameters section for adapter2
InfID=adapter2            ;postupgrade device ID
OemSection=params.adapter2.OemSection;Identifies the OemSection
OemDllToLoad=c:\temp\oem0001\migration.dll
```

请注意**adapter2**节中的**OemDllToLoad**条目。 另请注意，迁移 DLL 未创建 **adapter2. OemSection**。 在 GUI 模式阶段加载迁移 DLL 时，通常不会将 **InfToRunAfterInstall** 键写入 AnswerFile。 DLL 执行安装后升级;因此，它不需要创建一个 *Oem 节* 名称，其中包含在 GUI 模式阶段中 NetSetup 要执行的指令。

 

