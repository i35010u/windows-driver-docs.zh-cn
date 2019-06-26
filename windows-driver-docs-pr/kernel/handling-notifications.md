---
title: 处理通知
description: 处理通知
ms.assetid: ace7f59d-fe9f-4810-91db-2cf20c9591cf
keywords:
- 筛选注册表调用 WDK 内核，通知选项
- 注册表筛选驱动程序 WDK 内核，通知选项
- 通知 WDK 筛选注册表调用
- 筛选注册表调用 WDK 内核，监视的调用
- 注册表筛选驱动程序 WDK 内核，监视的调用
- 筛选注册表调用 WDK 内核，阻止调用
- 注册表筛选驱动程序 WDK 内核、 阻止调用
- 筛选注册表调用 WDK 内核，修改调用
- 筛选驱动程序 WDK 内核，修改调用注册表
- 阻止调用 WDK 筛选注册表调用
- 监视注册表调用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e98ef23feda0dfffa68483d511bcbca3569c7de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385621"
---
# <a name="handling-notifications"></a>处理通知


[ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)例程接收指向**REG\_*XXX*\_键\_信息**结构，其中包含有关正在进行的注册表操作的信息。

*RegistryCallback*例程可以监视、 阻止或修改注册表操作。

### <a name="monitoring-registry-calls"></a>监视注册表调用

如果注册表筛选，则驱动程序正在监视注册表操作，其*RegistryCallback*例程可以更新计数器或执行其他簿记操作并返回状态\_成功。 每当*RegistryCallback*例程将返回状态\_成功后，配置管理器仍会执行注册表操作。

在 Windows XP 和更高版本的 Windows 支持监视注册表调用。

### <a name="blocking-registry-calls"></a>阻止注册表调用

筛选驱动程序的注册表可以阻止注册表操作，如果其*RegistryCallback*例程为其返回状态值[NT\_成功](using-ntstatus-values.md)(*状态*) 等于**FALSE** （即，非成功 NTSTATUS 值）。 当配置管理器收到非成功的返回值时，它将立即返回对调用线程具有驱动程序指定的状态值。 因此，注册表筛选驱动程序可以使用预先通知以防止从正在处理的注册表操作。

如果*RegistryCallback*例程返回状态值的 NT\_成功 (*状态*) 等于**FALSE**对于预先通知，该操作的后通知回调不会发生。

阻止注册表调用在 Windows XP 和更高版本的 Windows 支持。 适用于 Windows Vista 及更高版本，该驱动程序可以修改注册表操作将返回到调用线程的值。 这些值包含在**REG\_*XXX*\_密钥\_信息**结构适用于 Windows Vista 及更高版本。

### <a name="modifying-registry-calls"></a>修改注册表调用

筛选驱动程序的注册表可以修改注册表操作的输出参数或返回值。 此外，驱动程序可以完全处理而不是允许注册表来处理操作的注册表操作。

当筛选驱动程序的注册表*RegistryCallback*例程收到通知后，它可以：

-   修改输出参数，其**REG\_*XXX*\_密钥\_信息**结构包含，并返回状态\_成功。 配置管理器返回到调用线程的修改后的输出参数。

    在 Windows Vista 及更高版本，支持修改输出参数。

-   修改注册表操作的返回值，通过提供有关状态值**ReturnStatus**的成员[ **REG\_POST\_操作\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_post_operation_information)结构并返回状态\_回调\_绕过。 配置管理器将返回指定值返回给调用线程。

    **请注意**如果驱动程序故障，从成功更改状态代码，它可能需要解除分配的配置管理器分配的对象。 或者，如果该驱动程序为成功从失败更改状态代码，它可能需要提供相应的输出参数。




在 Windows Vista 及更高版本，支持修改返回值。


当筛选驱动程序的注册表*RegistryCallback*例程收到前通知后，该例程可以处理注册表操作本身，然后返回状态\_回调\_绕过。 当注册表收到状态\_回调\_跳过从驱动程序，它只是返回状态\_对调用线程的成功和不会处理该操作。 该驱动程序会抢占注册表操作和完全处理，以及驱动程序必须非常谨慎才能返回有效的输出值中**REG\_*XXX*\_密钥\_信息**结构。

驱动程序可抢占注册表操作 Windows Vista 及更高版本。

如果*RegistryCallback*例程将返回状态\_回调\_绕过预通知，该操作后通知回调不会发生。

**请注意**不讨论几个注册表系统调用，因为它们很少使用，并使用它们时，通常以获得在注册表中的一些非常规结果。 修改这些调用执行的操作是非常困难且容易出错。 驱动程序开发人员我们建议您不要尝试修改以下注册表系统调用：
-   **NtRestoreKey**
-   **NtSaveKey**
-   **NtSaveKeyEx**
-   **NtLoadKeyEx**
-   **NtUnloadKey2**
-   **NtUnloadKeyEx**
-   **NtReplaceKey**
-   **NtRenameKey**
-   **NtSetInformationKey**










