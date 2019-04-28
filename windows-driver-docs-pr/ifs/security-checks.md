---
title: 安全检查
description: 安全检查
ms.assetid: 2883910a-72f3-4be9-b1dd-6fb02abffe73
keywords:
- 安全 WDK 文件系统、 安全检查
- 安全检查 WDK 的文件系统
- 安全检查 WDK 的文件系统，有关安全检查
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fe72a499e4938a4a969eeae2071bd6bed9e519d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344503"
---
# <a name="security-checks"></a>安全检查


## <span id="ddk_security_checks_if"></span><span id="DDK_SECURITY_CHECKS_IF"></span>


大容量的文件系统安全性方面是责任的安全检查的区域中。 因为它属于的实际"拥有"该对象的 Windows 文件系统中实现。 安全实现的目标是单独的 （实现由文件系统） 的策略以保护其对象、 和的机制 （实现安全引用监视器） 进行访问决策。

换而言之，文件系统开发人员负责在适当的时间来验证对文件系统资源的正确访问使安全引用监视器对的调用。 文件系统不需要了解安全引用监视器如何使这些安全决策的详细的信息。 本部分介绍其中的文件系统可以考虑增加安全检查点。

本部分包括以下主题：

[将安全描述符应用到的设备对象](applying-security-descriptors-on-the-device-object.md)

[IRP\_MJ\_CREATE](irp-mj-create-dispatch-routine.md)

[IRP\_MJ\_查询\_安全性和 IRP\_MJ\_设置\_安全](irp-mj-query-security-and-irp-mj-set-security.md)

[IRP\_MJ\_DIRECTORY\_控件](irp-mj-directory-control2.md)

[IRP\_MJ\_FILE\_SYSTEM\_CONTROL](https://msdn.microsoft.com/library/windows/hardware/ff548670)

[IRP\_MJ\_设置\_信息](https://msdn.microsoft.com/library/windows/hardware/ff549366)

[模拟](impersonation.md)

[进程和线程终止问题](process-and-thread-termination-issues.md)

 

 




