---
title: 文件系统的安全功能
description: 文件系统的安全功能
keywords:
- 安全 WDK 文件系统，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c41dcacabe59619a0c3ef9a42c3fa5e709f6ddf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839919"
---
# <a name="security-features-for-file-systems"></a>文件系统的安全功能


## <span id="ddk_security_features_for_file_systems_if"></span><span id="DDK_SECURITY_FEATURES_FOR_FILE_SYSTEMS_IF"></span>


与大多数其他类型的驱动程序不同的是，文件系统在正常的安全处理中是它紧密的。 这是因为安全的性质及其在 Microsoft Windows 中的实现。 常规 Windows 安全模式将安全描述符与对象（在本例中为 FILE 对象）相关联 \_ 。 支持 Windows 安全的文件系统负责存储和检索安全描述符。 此外，文件系统负责处理在标准内核模式驱动程序的常规范围之外的多个其他特殊安全注意事项。

本部分介绍了可添加到文件系统以支持 Windows 安全性的主要功能。 这些都不是必需的，无需使用任何这些接口即可构造文件系统。 此外，可以实现某些安全功能，同时忽略其他安全功能--这特定于文件系统的实现。

本节包括下列主题：

[安全描述符](security-descriptors.md)

[权限](privileges.md)

[审核](auditing.md)

[内核扩展属性](kernel-extended-attributes.md)

 


