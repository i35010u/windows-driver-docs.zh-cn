---
title: 筛选针对应用程序配置单元执行的注册表操作
description: Windows Vista 中引入了对应用程序配置单元的初始支持。
ms.assetid: A8D06E25-7CC6-476A-AB55-DAFE19954347
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ce08bbe206c7cda4125e0a1c8f97f469172e4dc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359959"
---
# <a name="filtering-registry-operations-on-application-hives"></a>筛选针对应用程序配置单元执行的注册表操作


Windows Vista 中引入了对应用程序配置单元的初始支持。 从 Windows 8 开始，改进了对应用程序配置单元支持，并且可预期得到更广泛使用的应用程序配置单元。 因此，注册表筛选器驱动程序开发的这些版本的 Windows，并且特别适用于 Windows 8 和更高版本，必须了解应用程序配置单元中的注册表操作。 这些驱动程序应处理此类操作有效地以避免对用户体验造成负面影响。

应用程序配置单元是用户模式应用程序来存储特定于应用程序的状态数据加载的注册表配置单元。 应用程序调用[ **RegLoadAppKey** ](https://msdn.microsoft.com/library/windows/desktop/ms724886)函数以加载应用程序配置单元。

相比其他类型的注册表配置单元中，应用程序配置单元下加载\\注册表\\下的注册表路径名称而不是\\注册表\\计算机或\\注册表\\用户。 \\注册表\\路径名称很特殊，因为没有方法来遍历此路径，并尝试打开下的项\\注册表\\A 将因错误状态 STATUS\_访问\_被拒绝。 应用程序可以访问应用程序配置单元中的键的唯一方法是使用的句柄的应用程序配置单元的根密钥。 应用程序获取来自此句柄**RegLoadAppKey**加载配置单元的调用。

应用程序不必显式卸载应用程序配置单元。 所有配置单元的句柄关闭后，操作系统会自动卸载的应用程序配置单元。

应用程序配置单元不支持该配置单元中的键上设置安全描述符。 相反，是适用于整个 hive 的一个安全描述符。 尝试在应用程序配置单元中的键上设置安全描述符将因错误状态 STATUS\_访问\_被拒绝。 相比其他类型的注册表配置单元，为其每个密钥保护具有其自己的安全描述符，应用程序配置单元的安全性基于 hive 文件的安全描述符。 因此，成功加载配置单元中的实体可以修改的整个配置单元。

注册表筛选器驱动程序接收到调用其[ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)例程的注册表操作的应用程序配置单元。 这些调用不区分应用程序配置单元上的注册表操作和其他类型的注册表配置单元上的操作。 注册表筛选器驱动程序处理创建密钥和打开密钥的操作 (所指示的**RegNtPreOpenKey**， **RegNtPreOpenKeyEx**， **RegNtPreCreateKey**，并**RegNtPreCreateKeyEx**通知值) 必须正确地处理以下特殊情况。 加载应用程序配置单元时，加载过程的最后一步是通过注册表管理器配置单元的根项开始。 注册表管理器发出注册表项，这意味着中的路径名称字符串的绝对路径与此打开密钥操作**CompleteName**的成员[ **REG\_创建\_密钥\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560920)， [ **REG\_创建\_键\_信息\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff560922)， [ **REG\_打开\_密钥\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560957)，或[ **REG\_打开\_密钥\_信息\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff560959)结构将启动与"\\注册表\\一个\\"。 仅注册表管理器可以使用绝对路径来打开应用程序配置单元。 如果尝试以这种方式打开应用程序配置单元注册表筛选器驱动程序 (例如，通过调用[ **ZwOpenKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567014)例程)，则操作将失败，错误状态状态\_访问\_被拒绝。

 

 




