---
title: MakeCat
description: MakeCat
ms.assetid: 348c5069-0360-4ff9-897e-9a8832ac196c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9edd4df75722af640b63a92de0298d5ff010db44
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384037"
---
# <a name="makecat"></a>MakeCat


MakeCat ( # A0) 是一个命令行[CryptoAPI](/windows/win32/seccrypto/cryptography-portal)工具，用于为[驱动程序包](../install/driver-packages.md)创建[编录文件](../install/catalog-files.md)。

有关 MakeCat 工具及其命令行参数的详细信息，请参阅 [使用 MakeCat](/windows/win32/seccrypto/using-makecat) 网站。

有关如何使用 MakeCat 工具的详细信息，请参阅 [创建用于对驱动程序包进行发布签名的目录文件](../install/creating-a-catalog-file-for-release-signing-a-driver-package.md)。

**注意**   只有使用 MakeCat 工具才能为未使用 INF 文件安装的驱动程序包创建编录文件。 如果使用 INF 文件安装了驱动程序包，请使用 [**Inf2Cat**](inf2cat.md) 工具创建编录文件。 Inf2Cat 自动包括在包的 INF 文件中引用的驱动程序包中的所有文件。 有关如何使用 Inf2Cat 工具的详细信息，请参阅 [使用 Inf2Cat 创建编录文件](../install/using-inf2cat-to-create-a-catalog-file.md)。

 

 

