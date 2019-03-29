---
title: SCSI 验证
description: SCSI 验证
ms.assetid: dba63137-ff92-480a-bca4-ab651a6bda85
keywords:
- SCSI 验证功能 WDK Driver Verifier
- 微型端口驱动程序 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e0ccbd2ee301100b75b3fc4428067c7e47e8ae
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349352"
---
# <a name="scsi-verification"></a>SCSI 验证


## <span id="ddk_scsi_verification_tools"></span><span id="DDK_SCSI_VERIFICATION_TOOLS"></span>


Driver Verifier 的 SCSI 验证功能监视 SCSI 微型端口驱动程序和端口驱动程序之间的交互。 如果一个例程的微型端口驱动程序误用了不正确的请求响应来自端口驱动程序，或很长的时间来响应请求，则会发出错误检查。

此驱动程序验证程序选项才可用在 Windows XP 及更高版本。

### <a name="span-idviolationsdetectedbyscsiverificationspanspan-idviolationsdetectedbyscsiverificationspanviolations-detected-by-scsi-verification"></a><span id="violations_detected_by_scsi_verification"></span><span id="VIOLATIONS_DETECTED_BY_SCSI_VERIFICATION"></span>通过 SCSI 验证检测到冲突

SCSI 验证选项可检测到 SCSI 例程的几个的误用。 还有可能单独禁用某些这些检查。

时 SCSI 微型端口驱动程序提交一个以下冲突时，驱动程序验证程序将发出错误检查 0xF1。

-   微型端口驱动程序将传递到错误的参数**ScsiPortInitialize**。

-   微型端口驱动程序调用**ScsiPortStallExecution** ，并指定延迟时间超过 0.1 秒，拖延症的处理器的时间过多的时间。

-   端口驱动程序调用的微型端口驱动程序例程，并花费的时间超过 0.5 秒的时间来执行该微型端口驱动程序。 ( **FindAdapter**例程不受限制，并**HwInitialize**例程允许 5 秒。)

-   微型端口驱动程序不止一次完成一个请求。

-   微型端口驱动程序完成无效 SRB 状态的例程。

-   微型端口驱动程序调用**ScsiPortNotification**寻求**NextLuRequest**，但未标记的请求仍处于活动状态。

-   微型端口驱动程序将传递到的虚拟地址无效**ScsiPortGetPhysicalAddress**。 （这通常意味着提供的地址不会映射到常见的缓冲区区域。）

-   总线重置保存期结束，但微型端口驱动程序仍有未完成的请求。

请参阅[ **Bug 检查 0xF1** ](https://msdn.microsoft.com/library/windows/hardware/ff560365) (SCSI\_VERIFIER\_检测到\_冲突) 的 bug 的完整列表检查参数。

除了这些冲突 SCSI 验证还可监视使用不当的微型端口驱动程序的内存的访问。 所做的微型端口驱动程序的两个常见内存冲突后请求完成后，访问 SRB 扩展和访问 SRB **DataBuffer**微型端口驱动程序时未指定**MapBuffers**.

这种内存冲突通常会导致[ **Bug 检查 0xD1** ](https://msdn.microsoft.com/library/windows/hardware/ff560244) (驱动程序\_IRQL\_不\_较少\_或\_等于)其颁发。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

激活 SCSI 验证选项的过程是不同于激活其他驱动程序验证程序选项的过程。

**若要激活 SCSI 验证**

1.  使用驱动程序验证程序管理器或 Verifier.exe 命令行启动微型端口驱动程序的验证。 因为 SCSI 验证不会作为一个选项可用，必须选择至少一个其他驱动程序验证程序选项。 请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)并[选择驱动程序，以验证](selecting-drivers-to-be-verified.md)有关详细信息。

2.  打开注册表使用 regedit.exe。 在中**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\ScsiPort**密钥，请添加名为一个子项**验证工具**. 在该注册表项，添加 REG\_DWORD 项名为**VerifyLevel**。 分配给此条目的值将确定哪些 SCSI 验证测试会处于活动状态。 0x1 值将为最大的验证。

3.  重新启动计算机。

如果**VerifyLevel**值不存在，或等于 0xFFFFFFFF，SCSI 验证将被禁用。

中的单个位**VerifyLevel**值可用于的控制将执行完全的测试。 位零 (0x1) 使某些测试;位 28、 29、 30 和 31 禁用某些测试。 因此，可以通过使用值 0x00000001 获取最大的验证。

每一位的影响是，如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">ReplTest1</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>驱动程序验证程序将监视微型端口驱动程序的内存访问，并检查错误地使用内存缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>28</p></td>
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>驱动程序验证工具将问题 bug 检查何时<strong>HwAdapterControl</strong>例程需要多个 0.5 秒才能完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>29</p></td>
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>重置保留期结束和逻辑单元上有仍未完成的请求时，驱动程序验证程序不会发出错误检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p>30</p></td>
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>微型端口驱动程序调用时，驱动程序验证程序不会发出的 bug 检查<strong>ScsiPortNotification</strong>与<strong>NextLuRequest</strong>未标记的请求时仍处于活动状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>31</p></td>
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>驱动程序验证工具将问题 bug 检查何时<strong>HwInitialize</strong>例程需要超过 5 秒钟才能完成。</p></td>
</tr>
</tbody>
</table>

 

在大多数情况下，建议的设置为 0xD0000001。 这样，所有**SCSI Verifier**上的测试时间限制除外**HwAdapterControl**，在时间限制**HwInitialize**，和多个请求为逻辑上的禁止单位。 这三项测试通常是太严格的。

如果内核调试器已附加，就可以启动周期后更改 SCSI 验证级别。 若要执行此操作，使用调试器命令：

```
kd> ed scsiport!SpVrfyLevel Level 
```

此命令允许您设置的新值*级别*。 使用此方法，可以在任何时候更改高位 （通过 0x8000000 0x10000000 处）。 但是，如果你想要更改的低位 (0x1)，您必须执行在启动过程中 （在内核调试程序的初始断点）。

同样，如果你想要完全停用 SCSI 验证，则需要设置*级别*为 0xFFFFFFFF 初始断点处。

**请注意**   0xF0000000 的值将禁用所有的测试，但仍会加载 SCSI 验证模块。 如果你想要禁用验证，但想要启用高位测试在更高版本时，请使用此值。 但是，值 0xFFFFFFFF 可防止模块加载完全;如果在启动过程中使用此值，它不会无法启用 SCSI 验证而无需重新启动。

 

### <a name="span-idactivatingwithoutrebootingspanspan-idactivatingwithoutrebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>激活时避免重新启动

一般情况下，您不能激活或停用无需重新启动 （"重新启动"） 的 SCSI 验证任何 Windows 操作系统的计算机。 ScsiPort.sys 驱动程序读取**VerifyLevel**注册表项仅当它加载时，这通常是在启动时。 但是，如果添加的注册表项时不会加载 ScsiPort.sys 驱动程序或者卸载并重新加载，您可以启用在 Windows XP 和更高版本的 Windows 上的 SCSI 验证而无需重新启动计算机。

 

 





