---
title: 调试 OCA 小型转储文件
description: 联机崩溃分析 (OCA) 是适用于 Windows 错误报告 (WER) 信息的报告机构。 贵公司可以使用 OCA 崩溃转储来分析客户问题。
ms.assetid: 56F4202D-6A5F-4177-BBFD-70DA717FF24A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f495725448e1631bf794d9b6635384f97e080014
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213469"
---
# <a name="debugging-oca-minidump-files"></a>调试 OCA 小型转储文件

 (OCA) 的联机崩溃分析是 [Windows 错误报告 (WER) ](/windows/desktop/wer/windows-error-reporting) 信息的报告工具。 贵公司可以使用 OCA 崩溃转储来分析客户问题。

## <a name="analyze-dump-files"></a>分析转储文件

转储文件是发生崩溃时计算机（或进程）状态的快照。

若要分析此数据，开发人员必须使用可以读取用户小型转储文件的调试程序。 调试程序还必须能够同时访问与转储文件内容匹配的映像和符号。 大多数开发人员都知道在调试实时崩溃时，需要使用匹配的符号。 但是，在调试小型转储时，匹配图像还必须可用于调试器。

由于小型转储文件存储的信息非常少，而且它们只存储发生崩溃时的一些不稳定信息，因此匹配的映像必须处于可用状态。 它们不存储计算机加载到内存的基本代码流。 为了节省空间，小型转储文件仅存储在发生崩溃的计算机上加载的映像的名称和时间戳。

若要检查在发生崩溃的计算机上运行的代码，调试程序必须能够访问发生崩溃的计算机上运行的相同二进制文件。 当开发人员需要调试崩溃时，调试程序使用存储在小型转储文件中的名称和时间戳对二进制文件进行独特地匹配和加载。

在调试程序中加载了映像和符号后，你可以分析发生崩溃时系统的状态，其中包括崩溃发生后保存的数据。 然而，小型转储无法重现导致特定故障的步骤。 要查找根本原因，需要分析驱动程序的源代码，以确定可能会导致故障的代码路径。 经验表明，分析转储文件和源代码可以了解和处理大多数故障。

## <a name="use-symbols-to-match-executable-code-with-source-code"></a>使用符号将可执行代码与源代码匹配

访问匹配的映像和符号的最佳方式是使用 Microsoft 符号服务器。 符号是使调试程序能够将可执行代码映射回源代码的数据。 构建程序时，通常将程序的符号存储在符号文件中。 当调试程序分析某个程序时，它需要访问程序的符号。

符号文件可以包含以下任意或全部内容：

- 所有函数的名称和地址。
- 所有数据类型、结构和类定义。
- 全局变量的名称、数据类型和地址。
- 局部变量的名称、数据类型、地址和范围。
- 对应于每个二进制指令的源代码中的行号。

Windows 驱动程序工具包 (WDK) 包括一些可用于减少符号文件中符号数量的工具。 将包含所有源级信息的符号文件称为完整的符号文件。 简化信息的符号文件被称为剥离符号文件。 有关详细信息，请参阅 [BinPlace](../devtest/binplace.md)。

由于符号数据对于从 Windows 错误报告 (WER) 数据中获取有意义的崩溃信息至关重要，因此鼓励你在提交要签名的驱动程序时提交符号。 提交符号时，将它们存储在服务器上，从而使符号数据与相关联的 WER 进程同步。 通过此存储流程，你可以轻松地对小型转储文件中报告的崩溃进行分类，并最终接收从 Microsoft 返回的更佳数据。

Microsoft 在 Internet 上提供符号服务器，你可以使用它来分析显示在小型转储文件中的 Windows 模块。 此服务器包括 Windows 中的剥离符号文件和其他一些产品。 Microsoft 已添加了适用于 Windows XP 和 Windows Server 2003 的二进制文件。 可以使用 Internet 符号服务器和 Windows 调试工具来分析小型转储文件。

## <a name="integrate-wer-into-applications"></a>将 WER 集成到应用程序中

有关将 WER 集成到应用程序中的更多信息，请参阅[使用 WER](/windows/desktop/wer/using-wer)。

## <a name="related-topics"></a>相关主题

[高级驱动程序调试 \[ 336 KB \] \[ PPT\]](https://download.microsoft.com/download/f/0/5/f05a42ce-575b-4c60-82d6-208d3754b2d6/adv-drv_debug.ppt)

[WDK 和 WinDbg 下载](../download-the-wdk.md)

[驱动程序调试基础知识 \[ WinHEC 2007; 633 KB \] \[ PPT\]](https://download.microsoft.com/download/a/f/d/afdfd50d-6eb9-425e-84e1-b4085a80e34e/dvr-t410_wh07.pptx)

[如何读取 Windows 在发生崩溃时创建的小型内存转储文件](https://support.microsoft.com/help/315263/how-to-read-the-small-memory-dump-file-that-is-created-by-windows-if-a)

[资源定义声明](/windows/desktop/menurc/resource-definition-statements)

[Windows 错误报告](/windows/desktop/wer/windows-error-reporting)

[VERSIONINFO 资源](/windows/desktop/menurc/versioninfo-resource)