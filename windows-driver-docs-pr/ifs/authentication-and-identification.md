---
title: 身份验证和标识
description: 身份验证和标识
ms.assetid: fe118cf3-05ce-43b1-b878-4bb99b97dc2e
keywords:
- 安全 WDK 文件系统、 最大程度减少威胁
- 身份验证 WDK 文件系统
- 标识 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c7226c90c48c91c8a80a9c28dd2bfb01115f3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556199"
---
# <a name="authentication-and-identification"></a>身份验证和标识


## <span id="ddk_authentication_and_identification_if"></span><span id="DDK_AUTHENTICATION_AND_IDENTIFICATION_IF"></span>


大多数驱动程序将不参与身份验证或标识问题，此任务留给各个服务。 其中一个驱动程序可能会在身份验证或标识处理过程中涉及的一种情况是在访问管理。 在这种情况下，通过调用安全引用监视器通常处理身份验证步骤。 身份验证和标识信息通常由安全令牌，封装给定的线程或进程的安全凭据的内部数据结构跟踪由操作系统。

 

 




