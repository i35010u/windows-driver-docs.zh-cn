---
title: MakeCat
description: MakeCat
ms.assetid: 348c5069-0360-4ff9-897e-9a8832ac196c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75da0ae6bf8e0658591ca13055a92ff899c18dfa
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769633"
---
# <a name="makecat"></a>MakeCat


MakeCat （Makecat）是一种命令行[CryptoAPI](https://docs.microsoft.com/windows/win32/seccrypto/cryptography-portal)工具，用于为[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)创建[编录文件](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)。

有关 MakeCat 工具及其命令行参数的详细信息，请参阅[使用 MakeCat](https://docs.microsoft.com/windows/win32/seccrypto/using-makecat)网站。

有关如何使用 MakeCat 工具的详细信息，请参阅[创建用于对驱动程序包进行发布签名的目录文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-a-catalog-file-for-release-signing-a-driver-package)。

**注意**   只有使用 MakeCat 工具才能为未使用 INF 文件安装的驱动程序包创建编录文件。 如果使用 INF 文件安装了驱动程序包，请使用[**Inf2Cat**](inf2cat.md)工具创建编录文件。 Inf2Cat 自动包括在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅[使用 Inf2Cat 创建编录文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-inf2cat-to-create-a-catalog-file)。

 

 

 





