---
title: 处理通知
description: 处理通知
keywords:
- 筛选注册表调用 WDK 内核，通知选项
- 注册表筛选驱动程序 WDK 内核，通知选项
- 通知 WDK 筛选器注册表调用
- 筛选注册表调用 WDK 内核，监视调用
- 注册表筛选驱动程序 WDK 内核，监视调用
- 筛选注册表调用 WDK 内核，阻止调用
- 注册表筛选驱动程序 WDK 内核，阻止调用
- 筛选注册表调用 WDK 内核，修改调用
- 注册表筛选驱动程序 WDK 内核，修改调用
- 阻止调用 WDK 筛选器注册表调用
- 监视注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25813fd1bf2ed7f4500fd264808cb5588e08e5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836387"
---
# <a name="handling-notifications"></a>处理通知


[*RegistryCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)例程接收指向 **REG \_ *XXX* \_ 密钥 \_ 信息** 结构的指针，该结构包含有关所发生注册表操作的信息。

*RegistryCallback* 例程可以监视、阻止或修改注册表操作。

### <a name="monitoring-registry-calls"></a>监视注册表调用

如果注册表筛选驱动程序正在监视注册表操作，则其 *RegistryCallback* 例程可以更新计数器或执行其他簿记操作，然后返回状态 " \_ 成功"。 每当 *RegistryCallback* 例程返回状态 \_ "成功" 时，配置管理器将继续执行注册表操作。

Windows XP 和更高版本的 Windows 支持监视注册表调用。

### <a name="blocking-registry-calls"></a>阻止注册表调用

注册表筛选驱动程序可以在注册表操作返回 (*RegistryCallback* 状态值（ [NT \_ success](using-ntstatus-values.md) *状态*) 等于 **FALSE** (即) 的非成功 NTSTATUS 值）时阻止注册表操作。 当 configuration manager 收到非成功返回值时，它会立即返回到具有驱动程序指定状态值的调用线程。 因此，注册表筛选驱动程序可以使用前通知来阻止对注册表操作进行处理。

如果 *RegistryCallback* 例程返回一个状态值，使其 NT \_ SUCCESS (*状态*) 等于 **FALSE** （对于预通知），则不会发生操作的后通知回调。

Windows XP 和更高版本的 Windows 支持阻止注册表调用。 对于 Windows Vista 和更高版本，驱动程序可以修改注册表操作返回到调用线程的值。 这些值包含在 Windows Vista 和更高版本的 **REG \_ *XXX* \_ 密钥 \_ 信息** 结构中。

### <a name="modifying-registry-calls"></a>修改注册表调用

注册表筛选驱动程序可以修改注册表操作的输出参数或返回值。 此外，驱动程序还可以完全处理注册表操作，而不是允许注册表处理操作。

注册表筛选驱动程序的 *RegistryCallback* 例程收到公告后，可以：

-   修改其 **REG \_ *XXX* \_ 密钥 \_ 信息** 结构包含的输出参数，然后返回状态 " \_ 成功"。 配置管理器将修改后的输出参数返回给调用线程。

    Windows Vista 和更高版本支持修改输出参数。

-   通过为 [**REG \_ POST \_ 操作 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)结构的 **ReturnStatus** 成员提供状态值，然后返回状态回调旁路来修改注册表操作的返回值 \_ \_ 。 配置管理器将指定的返回值返回给调用线程。

    **注意**  如果驱动程序将状态代码从 success 更改为失败，则可能需要解除分配配置管理器分配的对象。 或者，如果驱动程序将状态代码从 "失败" 更改为 "成功"，则可能必须提供相应的输出参数。




Windows Vista 和更高版本支持修改返回值。


当注册表筛选驱动程序的 *RegistryCallback* 例程收到预先通知时，例程可以自行处理注册表操作，然后返回状态 \_ 回调 \_ 绕过。 当注册表接收 \_ \_ 到从驱动程序绕过的状态回调时，它只会将状态 \_ 成功返回给调用线程，并且不会处理该操作。 驱动程序抢先于注册表操作，并且必须完全处理该驱动程序，并且该驱动程序必须小心地返回 **REG \_ *XXX* \_ 密钥 \_ 信息** 结构中的有效输出值。

驱动程序可以在 Windows Vista 和更高版本中抢占注册表操作。

如果 *RegistryCallback* 例程 \_ \_ 为预先通知返回状态回调旁路，则不会发生操作的通知后回调。

**注意**  不会记录多个注册表系统调用，因为它们很少使用，使用这些调用时，通常会在注册表中实现一些非常规结果。 修改由这些调用执行的操作非常困难，而且容易出错。 不建议驱动程序开发人员尝试修改以下注册表系统调用：
-   **NtRestoreKey**
-   **NtSaveKey**
-   **NtSaveKeyEx**
-   **NtLoadKeyEx**
-   **NtUnloadKey2**
-   **NtUnloadKeyEx**
-   **NtReplaceKey**
-   **NtRenameKey**
-   **NtSetInformationKey**
