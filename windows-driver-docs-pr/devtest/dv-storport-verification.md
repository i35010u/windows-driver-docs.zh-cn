---
title: Storport 验证
description: Storport 验证
ms.assetid: 3731C877-1A69-447C-A5DB-0BDD1B753D3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5fac8f52b7bf6a74506b22334e5e5e3a2587088
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840274"
---
# <a name="storport-verification"></a>Storport 验证


## <span id="ddk_storport_verification_tools"></span><span id="DDK_STORPORT_VERIFICATION_TOOLS"></span>


Storport 验证功能监视 Storport 微型端口驱动程序与端口驱动程序之间的交互。 如果微型端口驱动程序误用了一个例程，响应来自端口驱动程序的请求，或者需要大量时间来响应请求，则会发出 bug 检查。

**请注意**  Storport 验证功能只能在 windows Vista 和更高版本的 windows 中使用。

 

### <a name="span-idviolations_detected_by_storport_verificationspanspan-idviolations_detected_by_storport_verificationspanviolations-detected-by-storport-verification"></a><span id="violations_detected_by_storport_verification"></span><span id="VIOLATIONS_DETECTED_BY_STORPORT_VERIFICATION"></span>Storport 验证检测到的冲突

Storport 验证功能可检测到 Storport 例程的几个误用了。 还可以单独禁用其中一些检查。

如果 Storport 微型端口驱动程序提交以下冲突之一，则 Storport 验证功能会发出 bug 检查0xF1 或 bug 检查0xC4：

-   微型端口驱动程序将错误的参数（空指针）传递到[**StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程。

-   微型端口驱动程序调用[**StorPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution) ，并指定延迟时间超过0.1 秒，停止处理器的时间过长。

-   只能从微型端口驱动程序的**HwStorFindAdapter**例程调用[**StorPortFreeDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreedevicebase) 。

-   [**StorPortGetUncachedExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension)只能从微型端口驱动程序的**HwStorFindAdapter**例程调用，只能为总线-主适配器调用。 在调用**StorPortGetUncachedExtension**之前，微型端口必须设置[**HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)（Storport）结构的**SrbExtensionSize** 。

-   [**StorPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)例程仅支持由 system 即插即用（PnP）管理器分配给驱动程序的地址。

-   微型端口驱动程序将一个无效的虚拟地址传递给一个 **StorPortRead * * * xxx*或 **StorPortWrite * * xxx*例程（例如[**StorPortReadRegisterUchar**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportreadregisteruchar)或[**StorPortWritePortBufferUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportwriteportbufferulong)）。 这通常意味着提供的地址不会映射到公共缓冲区区。 指定的*寄存器*或*端口*必须在[**StorPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)例程返回的映射的内存空间范围内。 仅在基于 x86 的系统上支持此项检查。

有关 Storport 验证使用的 bug 检查参数的列表，请参阅[**Bug 检查 0xF1**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation) （SCSI\_验证程序\_检测到\_违规）。 除 Bug 检查0xF1 以外，还可以使用[**Bug 检查 0xC4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （驱动程序\_验证程序\_检测到\_违规）。

**注意**  [**Bug 检查 0XF1**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation)用于 SCSI 验证和 Storport 验证。

 

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

用于激活 Storport 验证选项的过程不同于用于激活其他驱动程序验证程序选项的过程。

**激活 Storport 验证**

1.  使用驱动程序验证器管理器或*Verifier*命令行开始验证微型端口驱动程序。 由于 Storport 验证将不可用作选项，因此必须至少*选择一个 "* 驱动程序验证程序" 选项。 有关详细信息，请参阅[选择驱动程序验证程序选项](selecting-driver-verifier-options.md)和[选择要验证的驱动程序](selecting-drivers-to-be-verified.md)。

2.  使用*regedit.exe*打开注册表。 在**HKEY\_本地\_计算机\\SYSTEM\\CurrentControlSet\\控件\\StorPort**密钥中，添加一个名为**Verifier**的子项。 如果**StorPort**密钥不存在，则需要创建该密钥。 在**HKEY\_本地\_计算机\\SYSTEM\\CurrentControlSet\\控件\\STORPort\\Verifier**密钥中，添加一个名为**VerifyLevel**的**REG\_DWORD**项。 分配给此项的值将确定哪些 Storport 验证测试将处于活动状态。 值0x1 会获得最大验证。

3.  重新启动计算机。

如果**VerifyLevel**值不存在，或等于0xffffffff，则将禁用 Storport 验证。

### <a name="span-idactivating_without_rebootingspanspan-idactivating_without_rebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>激活而不重新启动

通常，在任何 Windows 操作系统上都不需要重新启动计算机（重新启动），就无法激活或停用 Storport 验证。 *StorPort*驱动程序只在加载时读取**VerifyLevel**注册表项，这通常是在启动时。 但是，如果在添加注册表项时未加载*StorPort*驱动程序，或者卸载并重新加载该驱动程序，则可以在 windows Vista 和更高版本的 windows 上启用 storport 验证，而无需重新启动计算机。

 

 





