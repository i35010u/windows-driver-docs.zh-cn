---
title: 文件系统安全简介
description: 文件系统安全简介
keywords:
- 安全 WDK 文件系统，关于文件系统安全
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6bca0ac1e31bcdd83004da17629682c8b885c62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830575"
---
# <a name="introduction-to-file-systems-security"></a>文件系统安全简介


## <span id="ddk_introduction_to_file_systems_security_if"></span><span id="DDK_INTRODUCTION_TO_FILE_SYSTEMS_SECURITY_IF"></span>


使用 WDK 的文件系统开发人员应了解在实现其文件系统时的安全注意事项。 文件系统筛选器驱动程序开发人员还应注意这些问题，并应熟悉 Microsoft Windows 安全界面，以便将安全注意事项纳入到其产品中。

本部分重点介绍 Windows 安全和文件系统。 对于想要开发 Windows 安全扩展的用户或希望在 Windows 环境中实施非 Windows 安全模型的文件系统开发人员而言，此方法并不适用。

本部分包含一些代码示例。 这些示例是从实际代码中提取的，但此处以缩写形式提供。 开发人员应该改编这些示例以在其特定的环境中使用。

 

 




