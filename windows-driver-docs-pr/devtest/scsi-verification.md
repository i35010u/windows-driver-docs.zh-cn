---
title: SCSI 验证
description: SCSI 验证
ms.assetid: dba63137-ff92-480a-bca4-ab651a6bda85
keywords:
- SCSI 验证功能 WDK 驱动程序验证程序
- 微型端口驱动程序 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764b7004e21a30b0b9a094a7299ed10b131fb144
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384437"
---
# <a name="scsi-verification"></a>SCSI 验证


## <span id="ddk_scsi_verification_tools"></span><span id="DDK_SCSI_VERIFICATION_TOOLS"></span>


驱动程序验证程序的 SCSI 验证功能监视 SCSI 微型端口驱动程序与端口驱动程序之间的交互。 如果微型端口驱动程序误用了一个例程，响应来自端口驱动程序的请求，或者需要大量时间来响应请求，则会发出 bug 检查。

此驱动程序验证程序选项仅在 Windows XP 和更高版本中可用。

### <a name="span-idviolations_detected_by_scsi_verificationspanspan-idviolations_detected_by_scsi_verificationspanviolations-detected-by-scsi-verification"></a><span id="violations_detected_by_scsi_verification"></span><span id="VIOLATIONS_DETECTED_BY_SCSI_VERIFICATION"></span>SCSI 验证检测到的冲突

SCSI 验证选项可以检测到多个误用了的 SCSI 例程。 还可以单独禁用某些检查。

当 SCSI 微型端口驱动程序提交以下冲突之一时，驱动程序验证程序将发出 bug 检查0xF1。

-   微型端口驱动程序将错误的参数传递给 **ScsiPortInitialize**。

-   微型端口驱动程序调用 **ScsiPortStallExecution** ，并指定延迟时间超过0.1 秒，停止处理器的时间过长。

-   端口驱动程序调用微型端口驱动程序例程，微型端口驱动程序的执行时间超过0.5 秒。  (**FindAdapter** 例程为豁免，则允许 **HwInitialize** 例程5秒。 ) 

-   微型端口驱动程序多次完成一个请求。

-   微型端口驱动程序完成具有无效 SRB 状态的例程。

-   微型端口驱动程序调用 **ScsiPortNotification** 来请求 **NextLuRequest**，但未标记的请求仍处于活动状态。

-   微型端口驱动程序将无效的虚拟地址传递给 **ScsiPortGetPhysicalAddress**。  (这通常意味着提供的地址不会映射到通用缓冲区区域。 ) 

-   总线重置保持期结束，但微型端口驱动程序仍有未处理的请求。

有关错误检查参数的完整列表，请参阅 [**Bug 检查 0xF1**](../debugger/bug-check-0xf1--scsi-verifier-detected-violation.md) (SCSI \_ 验证器 \_ 检测到 \_ 冲突) 。

除了这些违规情况外，SCSI 验证还会监视微型端口驱动程序的内存访问，以不正确地使用。 在请求完成后，小型端口驱动程序所做的两个常见内存冲突将在访问 SRB 扩展，并在**未指定微型**端口驱动程序时访问 SRB 的**DataBuffer** 。

此排序的内存冲突通常会导致 [**Bug 检查 0xD1**](../debugger/bug-check-0xd1--driver-irql-not-less-or-equal.md) (驱动程序 \_ IRQL \_ 不 \_ 小于 \_ 或 \_ 等于发出) 。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

用于激活 SCSI 验证选项的过程不同于用于激活其他驱动程序验证程序选项的过程。

**激活 SCSI 验证**

1.  使用驱动程序验证器管理器或 Verifier.exe 命令行开始验证微型端口驱动程序。 由于 SCSI 验证将不可用作选项，因此必须至少选择一个 "驱动程序验证程序" 选项。 请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md) 和 [选择要验证的驱动程序](selecting-drivers-to-be-verified.md) 以获取详细信息。

2.  使用 regedit.exe 打开注册表。 在 **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ ScsiPort** 项中，添加一个名为 **Verifier**的子项。 在该密钥中，添加一个 \_ 名为 **VERIFYLEVEL**的 REG DWORD 条目。 分配给此项的值将确定哪些 SCSI 验证测试将处于活动状态。 值0x1 会获得最大验证。

3.  重新启动计算机。

如果 **VerifyLevel** 值不存在，或等于0xffffffff，则将禁用 SCSI 验证。

可以使用 **VerifyLevel** 值中的单个位来精确控制要执行的测试。 位零 (0x1) 启用某些测试;位28、29、30和31禁用某些测试。 因此，可以使用值0x00000001 获得最大验证。

每位的效果如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit</th>
<th align="left">值</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>驱动程序验证程序将监视微型端口驱动程序的内存访问，并检查是否不正确使用内存缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>如果 <strong>HwAdapterControl</strong> 例程完成时间超过0.5 秒，驱动程序验证程序将不会发出 bug 检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>29</p></td>
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>如果重置的保持期结束，并且逻辑单元上仍有未完成的请求，则驱动程序验证程序不会发出 bug 检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p>30</p></td>
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>如果无标记的请求仍处于活动状态，则当微型端口驱动程序使用<strong>NextLuRequest</strong>调用<strong>ScsiPortNotification</strong>时，驱动程序验证程序不会发出 bug 检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>31</p></td>
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>如果 <strong>HwInitialize</strong> 例程完成时间超过5秒，驱动程序验证程序将不会发出 bug 检查。</p></td>
</tr>
</tbody>
</table>

 

在大多数情况下，建议的设置为0xD0000001。 这将启用除**HwAdapterControl**上的时间限制之外的所有**SCSI 验证**程序测试、对**HwInitialize**的时间限制以及对逻辑单元的多个请求上的 "禁止"。 这三项测试通常过于严格。

如果附加了内核调试程序，则可以在启动周期后更改 SCSI 验证级别。 为此，请使用调试器命令：

```
kd> ed scsiport!SpVrfyLevel Level 
```

使用此命令可以为 *级别*设置新值。 使用此方法，你可以随时更改0x10000000 到 0x8000000) 的高位 (。 但是，如果你想要更改低位 (0x1) ，则必须在启动过程中 (，在内核调试器的初始断点) 执行此操作。

同样，如果要完全停用 SCSI 验证，则需要在初始断点处将 *Level* 设置为0xffffffff。

**注意**   值0xF0000000 将禁用所有测试，但仍会加载 SCSI 验证模块。 如果希望禁用验证，但要在以后启用高位测试，请使用此值。 另一方面，值0xFFFFFFFF 会阻止完全加载模块;如果在启动过程中使用此值，则不能在不重启的情况下启用 SCSI 验证。

 

### <a name="span-idactivating_without_rebootingspanspan-idactivating_without_rebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>激活而不重新启动

通常，在任何 Windows 操作系统上都 ) 计算机上 ( "重新启动"，不能激活或停用 SCSI 验证。 ScsiPort.sys 驱动程序只在加载（通常在启动时）读取 **VerifyLevel** 注册表项。 但是，如果在添加注册表项时未加载 ScsiPort.sys 的驱动程序，或者卸载并重新加载了该驱动程序，则可以在 Windows XP 和更高版本的 Windows 上启用 SCSI 验证，而无需重新启动计算机。

 

