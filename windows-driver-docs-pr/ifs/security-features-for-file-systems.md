---
title: 对于文件系统的安全功能
description: 对于文件系统的安全功能
ms.assetid: 344083d5-781a-46e3-ab90-b70e57d07dd0
keywords:
- 安全 WDK 文件系统功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5c946b7a0bd284656990cec4583e29358d1f628
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524212"
---
# <a name="security-features-for-file-systems"></a>对于文件系统的安全功能


## <span id="ddk_security_features_for_file_systems_if"></span><span id="DDK_SECURITY_FEATURES_FOR_FILE_SYSTEMS_IF"></span>


与大多数其他类型的驱动程序，不同的文件系统是紧密相关常规安全处理中。 这是安全和 Microsoft Windows 中的实现的性质。 常规的 Windows 安全模型将与对象-在这种情况下，该文件相关联的安全描述符\_对象。 支持 Windows 安全文件系统负责存储和检索安全描述符。 此外，文件系统负责处理处于标准内核模式驱动程序的正常作用域之外的其他几个特殊安全注意事项。

本部分讨论可能会添加到文件系统，以支持 Windows 安全性的主要功能。 这些都不是必需的以及可以不使用任何这些接口构造的文件系统。 此外，就可以实施一些安全功能，同时忽略其他人-这是特定于文件系统的实现。

本部分包括以下主题：

[安全描述符](security-descriptors.md)

[权限](privileges.md)

[审核](auditing.md)

[扩展属性的内核](kernel-extended-attributes.md)

 


