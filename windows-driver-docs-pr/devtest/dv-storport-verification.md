---
title: Storport 验证
description: Storport 验证
ms.assetid: 3731C877-1A69-447C-A5DB-0BDD1B753D3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63af5c2ae009a36a03791fb85d7818008c23dc6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371389"
---
# <a name="storport-verification"></a>Storport 验证


## <span id="ddk_storport_verification_tools"></span><span id="DDK_STORPORT_VERIFICATION_TOOLS"></span>


Storport 验证功能监视 Storport 微型端口驱动程序和端口驱动程序之间的交互。 如果一个例程的微型端口驱动程序误用了不正确的请求响应来自端口驱动程序，或很长的时间来响应请求，则会发出错误检查。

**请注意**  Storport 验证功能只是在 Windows Vista 和更高版本的 Windows 中可用。

 

### <a name="span-idviolationsdetectedbystorportverificationspanspan-idviolationsdetectedbystorportverificationspanviolations-detected-by-storport-verification"></a><span id="violations_detected_by_storport_verification"></span><span id="VIOLATIONS_DETECTED_BY_STORPORT_VERIFICATION"></span>Storport 验证检测到冲突

Storport 验证功能可以检测到多个误用了 Storport 例程。 还有可能要单独禁用其中一些检查。

Storport 验证功能将发出 bug 检查 0xF1 或 bug 检查 0xC4 Storport 微型端口驱动程序提交一个以下冲突：

-   微型端口驱动程序将错误参数 （NULL 指针） 传递给[ **StorPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)例程。

-   微型端口驱动程序调用[ **StorPortStallExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportstallexecution) ，并指定延迟时间超过 0.1 秒，拖延症的处理器的时间过多的时间。

-   [**StorPortFreeDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreedevicebase)仅从微型端口驱动程序可以调用**HwStorFindAdapter**例程。

-   [**StorPortGetUncachedExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetuncachedextension)仅从微型端口驱动程序可以调用**HwStorFindAdapter**例程和可以调用仅为主机总线适配器。 微型端口必须设置**SrbExtensionSize**的[ **HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data) (Storport) 结构，然后再调用**StorPortGetUncachedExtension**。

-   [ **StorPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase)例程支持分配给驱动程序的系统插即用 (PnP) 管理器的地址。

-   微型端口驱动程序将无效的虚拟地址传递给其中一个 **StorPortRead * * * xxx*或 **StorPortWrite * * * xxx*例程 (例如， [ **StorPortReadRegisterUchar** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportreadregisteruchar)或[ **StorPortWritePortBufferUlong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportwriteportbufferulong))。 这通常意味着提供的地址不会映射到常见的缓冲区区域。 指定*注册*或*端口*必须在映射的内存空间范围内返回[ **StorPortGetDeviceBase** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase)例程。 此检查仅支持基于 x86 的系统。

Storport 验证使用的 bug 检查参数的列表，请参阅[ **Bug 检查 0xF1** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation) (SCSI\_VERIFIER\_检测到\_冲突)。 除了 Bug 检查 0xF1，还使用了 Storport 验证[ **Bug 检查 0xC4** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (驱动程序\_VERIFIER\_检测到\_冲突)。

**请注意**  [**Bug 检查 0xF1** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xf1--scsi-verifier-detected-violation)用于 SCSI 验证和 Storport 验证。

 

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

激活 Storport 验证选项的过程是不同于激活其他驱动程序验证程序选项的过程。

**若要激活 Storport 验证**

1.  使用驱动程序验证程序管理器或*Verifier.exe*命令行，请启动的微型端口驱动程序验证。 因为 Storport 验证不会作为一个选项可用，则必须选择至少一个*其他*Driver Verifier 选项。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)并[选择驱动程序，以验证](selecting-drivers-to-be-verified.md)。

2.  打开注册表使用*regedit.exe*。 在中**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\StorPort**密钥，请添加名为一个子项**验证工具**. 如果**StorPort**项不存在，则需要创建它。 内**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\STORPort\\Verifier**密钥，请添加**REG\_DWORD**名为条目**VerifyLevel**。 分配给此条目的值将确定哪些 Storport 验证测试会处于活动状态。 0x1 值将为最大的验证。

3.  重新启动计算机。

如果**VerifyLevel**值不存在，或等于 0xFFFFFFFF，Storport 验证将被禁用。

### <a name="span-idactivatingwithoutrebootingspanspan-idactivatingwithoutrebootingspanactivating-without-rebooting"></a><span id="activating_without_rebooting"></span><span id="ACTIVATING_WITHOUT_REBOOTING"></span>激活时避免重新启动

一般情况下，您不能激活或停 Storport 验证用无需重新启动 （重新启动） 在任何 Windows 操作系统上的计算机。 *StorPort.sys*驱动程序读取**VerifyLevel**注册表项仅当它加载时，这通常是在启动时。 但是，如果*StorPort.sys*添加注册表项，或如果它是卸载并重新加载，可以自己启用 Storport 验证在 Windows Vista 和更高版本的 Windows 上，而无需重新启动计算机时不加载驱动程序。

 

 





