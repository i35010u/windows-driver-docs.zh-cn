---
title: 打开 Enclave 调试
description: 打开 Enclave 调试
ms.date: 08/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: fbefd760dc8f77ed8d5dff1a936aad6e07438a70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833631"
---
# <a name="open-enclave-debugging"></a>打开 Enclave 调试

WinDbg Preview 版本1.0.1908.30002 和更高版本支持 Open Enclave 调试。 开放式 Enclave 应用程序使用基于硬件的受信任执行环境，也称为 enclaves。 Enclave 是受保护的内存区域，为数据和代码执行提供机密性。 它是受信任的执行环境的实例 (t) 通常由硬件保护，例如， [Intel Software Guard 扩展 (SGX) ](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions.html)。

Open Enclave SDK 是一个硬件无关的开源库，用于开发利用 enclaves 的应用程序。 有关详细信息，请参阅中的项目 GitHub https://github.com/openenclave/openenclave 。

有关如何使用 WinDbg Preview 调试 Open Enclave 应用程序的信息，请参阅 [使用 Windbg Preview 调试 ELF Enclaves](https://github.com/openenclave/openenclave/blob/master/docs/GettingStartedDocs/Windows_windbg.md)。

## <a name="debugrt-dll"></a>debugrt DLL

Open Enclave 的一些调试功能由作为 Enclave 调试目标的一部分加载的 debugrt DLL 提供。 有关详细信息和源代码，请参阅 debugrt 项目 GitHub https://aka.ms/debugrt 。
