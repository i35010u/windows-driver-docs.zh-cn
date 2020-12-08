---
title: 筛选针对应用程序配置单元执行的注册表操作
description: Windows Vista 中引入了对应用程序配置单元的初始支持。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b1f98ed7f80de129b3ca4d0a841bb785c493fa85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788671"
---
# <a name="filtering-registry-operations-on-application-hives"></a>筛选针对应用程序配置单元执行的注册表操作


Windows Vista 中引入了对应用程序配置单元的初始支持。 从 Windows 8 开始，为应用程序配置单元提供改进的支持，需要更广泛地使用应用程序配置单元。 因此，为这些版本的 Windows 开发的注册表筛选器驱动程序，特别是对于 Windows 8 及更高版本，必须注意应用程序配置单元上的注册表操作。 这些驱动程序应该有效地处理此类操作，以避免对用户体验产生负面影响。

应用程序配置单元是用户模式应用程序加载的注册表配置单元，用于存储特定于应用程序的状态数据。 应用程序调用 [**RegLoadAppKey**](/windows/win32/api/winreg/nf-winreg-regloadappkeya) 函数以加载应用程序配置单元。

与其他类型的注册表配置单元不同，应用程序配置单元会在注册表中加载 \\ \\ 注册表路径名称，而不是 \\ 注册表的 \\ 计算机或 \\ 注册表 \\ 用户。 \\注册表 \\ 路径名称是特别的，因为没有办法遍历此路径，尝试在注册表 A 下打开密钥会失败，并出现 \\ \\ 错误状态 " \_ 拒绝访问" 错误 \_ 。 应用程序访问应用程序 hive 中的密钥的唯一方式是使用应用程序配置单元的根密钥的句柄。 应用程序从加载 hive 的 **RegLoadAppKey** 调用获取此句柄。

应用程序无需显式卸载应用程序配置单元。 在关闭对 hive 的所有句柄之后，操作系统会自动卸载应用程序配置单元。

应用程序配置单元不支持在 hive 中的密钥上设置安全描述符。 相反，整个 hive 都有一个安全描述符。 尝试在应用程序配置单元中的某个密钥上设置安全描述符将失败，并出现错误状态 " \_ 拒绝访问" \_ 。 与其他类型的注册表配置单元不同，每个密钥都使用其自己的安全描述符来保护，而应用程序配置单元的安全性则基于 hive 文件的安全描述符。 因此，加载 hive 成功的实体可以修改整个 hive。

注册表筛选器驱动程序接收对应用程序配置单元上的注册表操作的 [*RegistryCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function) 例程的调用。 这些调用不区分应用程序配置单元上的注册表操作和其他类型的注册表配置单元上的操作。 用于处理 RegNtPreOpenKey、RegNtPreOpenKeyEx、RegNtPreCreateKey 和 RegNtPreCreateKeyEx 通知值所指示的 **RegNtPreOpenKey**、 **RegNtPreOpenKeyEx**、 **RegNtPreCreateKey** 和 **RegNtPreCreateKeyEx** 通知值 (的注册表筛选器驱动程序) 必须正确处理以下特殊情况。 加载应用程序配置单元时，加载过程的最后一步是由注册表管理器打开 hive 的根密钥。 注册表管理器会发出此带有密钥绝对路径的打开键操作，这意味着 [**注册 \_ 创建密钥 \_ \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_create_key_information)的 **CompleteName** 成员中的路径名字符串、 [**reg \_ create \_ key \_ information \_ v1**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_create_key_information_v1)、 [**reg \_ open \_ key \_ 信息**](https://msdn.microsoft.com/library/windows/hardware/ff560957)或 [**reg \_ open \_ key \_ information \_ v1**](https://msdn.microsoft.com/library/windows/hardware/ff560959)结构将以 " \\ registry \\ A" 开头 \\ 。 只有注册表管理器可以使用绝对路径来打开应用程序配置单元。 如果注册表筛选器驱动程序尝试以这种方式打开应用程序配置单元 (例如，通过调用 [**ZwOpenKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey) 例程) ，操作将失败，并出现错误状态 " \_ 拒绝访问" 状态 \_ 。

 

