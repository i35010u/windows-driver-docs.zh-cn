---
title: 处理通知
description: 处理通知
ms.assetid: ace7f59d-fe9f-4810-91db-2cf20c9591cf
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
ms.openlocfilehash: b431cb06a25fc8841f81a4e3efc014917ec9c44c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836490"
---
# <a name="handling-notifications"></a>处理通知


[*RegistryCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)例程接收指向**REG\_*XXX*\_密钥\_信息**结构的指针，该信息结构包含有关所发生注册表操作的信息。

*RegistryCallback*例程可以监视、阻止或修改注册表操作。

### <a name="monitoring-registry-calls"></a>监视注册表调用

如果注册表筛选驱动程序监视注册表操作，其*RegistryCallback*例程可以更新计数器或执行其他簿记操作，然后返回状态\_SUCCESS。 每当*RegistryCallback*例程返回状态\_"成功" 时，配置管理器将继续执行注册表操作。

Windows XP 和更高版本的 Windows 支持监视注册表调用。

### <a name="blocking-registry-calls"></a>阻止注册表调用

如果注册表筛选驱动程序的*RegistryCallback*例程返回一个状态值，而[\_](using-ntstatus-values.md)该状态*值为（* 即，非成功的 NTSTATUS值），则它会阻止注册表操作。 当 configuration manager 收到非成功返回值时，它会立即返回到具有驱动程序指定状态值的调用线程。 因此，注册表筛选驱动程序可以使用前通知来阻止对注册表操作进行处理。

如果*RegistryCallback*例程为预先通知返回一个状态值，使 NT\_SUCCESS （*状态*）等于**FALSE** ，则不会发生该操作的后通知回调。

Windows XP 和更高版本的 Windows 支持阻止注册表调用。 对于 Windows Vista 和更高版本，驱动程序可以修改注册表操作返回到调用线程的值。 这些值包含在 Windows Vista 和更高版本的**REG\_*XXX*\_密钥\_信息**结构中。

### <a name="modifying-registry-calls"></a>修改注册表调用

注册表筛选驱动程序可以修改注册表操作的输出参数或返回值。 此外，驱动程序还可以完全处理注册表操作，而不是允许注册表处理操作。

注册表筛选驱动程序的*RegistryCallback*例程收到公告后，可以：

-   修改其**REG\_*XXX*\_密钥\_信息**结构包含的输出参数，然后返回\_状态 "成功"。 配置管理器将修改后的输出参数返回给调用线程。

    Windows Vista 和更高版本支持修改输出参数。

-   通过为[**REG\_POST\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)的**ReturnStatus**成员提供状态值来修改注册表操作的返回值\_信息结构，然后返回\_回叫状态\_开. 配置管理器将指定的返回值返回给调用线程。

    **注意** 如果驱动程序将状态代码从 success 更改为失败，则可能需要解除分配配置管理器分配的对象。 或者，如果驱动程序将状态代码从 "失败" 更改为 "成功"，则可能必须提供相应的输出参数。




Windows Vista 和更高版本支持修改返回值。


当注册表筛选驱动程序的*RegistryCallback*例程收到预先通知时，例程可以处理注册表操作本身，然后返回状态\_回调\_绕过。 当注册表接收到\_从驱动程序跳过的状态\_回调时，它只会将\_状态返回到调用线程，而不会处理操作。 驱动程序抢先于注册表操作并必须完全处理它，并且驱动程序必须小心地在**REG\_*XXX*\_密钥\_信息**结构中返回有效的输出值。

驱动程序可以在 Windows Vista 和更高版本中抢占注册表操作。

如果*RegistryCallback*例程为预先通知返回状态\_回调\_绕过，则不会发生操作的后通知回调。

**注意** 不会记录多个注册表系统调用，因为它们很少使用，使用这些调用时，通常会在注册表中实现一些非常规结果。 修改由这些调用执行的操作非常困难，而且容易出错。 不建议驱动程序开发人员尝试修改以下注册表系统调用：
-   **NtRestoreKey**
-   **NtSaveKey**
-   **NtSaveKeyEx**
-   **NtLoadKeyEx**
-   **NtUnloadKey2**
-   **NtUnloadKeyEx**
-   **NtReplaceKey**
-   **NtRenameKey**
-   **NtSetInformationKey**










