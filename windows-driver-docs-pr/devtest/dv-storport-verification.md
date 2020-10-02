---
title: Storport 验证
description: Storport 验证
ms.assetid: 3731C877-1A69-447C-A5DB-0BDD1B753D3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ff90ddf313143c7f77d92317320789fd23e993a
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646013"
---
# <a name="storport-verification"></a>Storport 验证

Storport 验证功能监视 Storport 微型端口驱动程序与端口驱动程序之间的交互。 如果微型端口驱动程序误用了一个例程，响应来自端口驱动程序的请求，或者需要大量时间来响应请求，则会发出 bug 检查。

>[!NOTE]
>Storport 验证功能只能在 Windows Vista 和更高版本的 Windows 中使用。

## <a name="violations-detected-by-storport-verification"></a>Storport 验证检测到的冲突

Storport 验证功能可检测到 Storport 例程的几个误用了。 还可以单独禁用其中一些检查。

如果 Storport 微型端口驱动程序提交以下冲突之一，则 Storport 验证功能会发出 bug 检查0xF1 或 bug 检查0xC4：

- 微型端口驱动程序将错误的参数传递 () 到 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize) 例程的 NULL 指针。

- 微型端口驱动程序调用 [**StorPortStallExecution**](/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution) ，并指定延迟时间超过0.1 秒，停止处理器的时间过长。

- 只能从微型端口驱动程序的**HwStorFindAdapter**例程调用[**StorPortFreeDeviceBase**](/windows-hardware/drivers/ddi/storport/nf-storport-storportfreedevicebase) 。

- [**StorPortGetUncachedExtension**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension) 只能从微型端口驱动程序的 **HwStorFindAdapter** 例程调用，只能为总线-主适配器调用。 在调用**StorPortGetUncachedExtension**之前，微型端口必须将[**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data-r1)的**SrbExtensionSize**设置 (Storport) 结构。

- [**StorPortGetDeviceBase**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)例程仅支持由 system 即插即用 (PnP) manager 分配给驱动程序的地址。

- 微型端口驱动程序将一个无效的虚拟地址传递给一个 **StorPortRead * * * xxx* 或 **StorPortWrite ** * (Xxx 例程，例如 [**StorPortReadRegisterUchar**](/windows-hardware/drivers/ddi/storport/nf-storport-storportreadregisteruchar) 或 [**StorPortWritePortBufferUlong**](/windows-hardware/drivers/ddi/storport/nf-storport-storportwriteportbufferulong)) 。 这通常意味着提供的地址不会映射到公共缓冲区区。 指定的 *寄存器* 或 *端口* 必须在 [**StorPortGetDeviceBase**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase) 例程返回的映射的内存空间范围内。 仅在基于 x86 的系统上支持此项检查。

有关 Storport 验证使用的 bug 检查参数的列表，请参阅 [**Bug 检查 0xF1**](../debugger/bug-check-0xf1--scsi-verifier-detected-violation.md) (SCSI \_ 验证程序 \_ 检测到 \_ 冲突) 。 除 Bug 检查0xF1 外，Storport 验证还利用 [**Bug 检查 0xC4**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (驱动程序验证程序 \_ \_ 检测到 \_ 冲突) 。

>[!NOTE]
>[**Bug 检查 0xF1**](../debugger/bug-check-0xf1--scsi-verifier-detected-violation.md) 用于 SCSI 验证和 Storport 验证。

### <a name="activating-the-storport-verification-option"></a>激活 Storport 验证选项

用于激活 Storport 验证选项的过程不同于用于激活其他驱动程序验证程序选项的过程。

1. 使用驱动程序验证器管理器或 *Verifier.exe* 命令行开始验证微型端口驱动程序。 由于 Storport 验证将不可用作选项，因此必须至少 *选择一个 "* 驱动程序验证程序" 选项。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md) 和 [选择要验证的驱动程序](selecting-drivers-to-be-verified.md)。

2. 使用 *regedit.exe*打开注册表。 在 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ StorPort** 密钥中，添加一个名为 **Verifier**的子项。 如果 **StorPort** 密钥不存在，则需要创建该密钥。 在**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ STORPort \\ 验证**程序密钥中，添加一个名为**VerifyLevel**的**REG \_ DWORD**条目。 分配给此项的值将确定哪些 Storport 验证测试将处于活动状态。 值0x1 会获得最大验证。

3. 重新启动计算机。

如果 **VerifyLevel** 值不存在，或等于0xffffffff，则将禁用 Storport 验证。

### <a name="activating-without-rebooting"></a>激活而不重新启动

通常，在任何 Windows 操作系统上，如果不重新启动 (重新启动) 计算机，则无法激活或停用 Storport 验证。 *StorPort.sys*驱动程序只在加载（通常在启动时）读取**VerifyLevel**注册表项。 但是，如果在添加注册表项时未加载 *StorPort.sys* 的驱动程序，或者卸载并重新加载了该驱动程序，则可以在 windows Vista 和更高版本的 windows 上启用 Storport 验证，而无需重新启动计算机。
