---
title: 文件系统安全简介
description: 文件系统安全简介
ms.assetid: 328568dc-a003-4e00-941a-9ccf15b1c735
keywords:
- 安全 WDK 文件系统、 文件系统安全性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac35e0c8f147768c762ee5e9d635009bb54f2392
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542258"
---
# <a name="introduction-to-file-systems-security"></a>文件系统安全简介


## <span id="ddk_introduction_to_file_systems_security_if"></span><span id="DDK_INTRODUCTION_TO_FILE_SYSTEMS_SECURITY_IF"></span>


文件系统的开发人员使用 WDK 期间其文件系统的实现应了解安全注意事项。 文件系统筛选器驱动程序开发人员还应注意这些问题，并应是熟悉的 Microsoft Windows 安全接口才能合并到他们的产品的安全注意事项。

本部分重点介绍 Windows 安全和文件系统。 它不是为那些想要开发安全扩展插件，Windows，或文件系统的开发人员想要实现 Windows 环境中的非 Windows 安全模型的入门读物。

本部分包括大量的代码示例。 示例提取从实际代码，但以缩写形式此处提供。 开发人员应灵活掌握在其特定环境中使用这些示例。

 

 




