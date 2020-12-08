---
title: 身份验证和标识
description: 身份验证和标识
keywords:
- 安全 WDK 文件系统，最大限度地减少威胁
- 身份验证 WDK 文件系统
- 标识 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b74f6a7ed08246179cfed69d0deb39f3f371e6d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837283"
---
# <a name="authentication-and-identification"></a>身份验证和标识


## <span id="ddk_authentication_and_identification_if"></span><span id="DDK_AUTHENTICATION_AND_IDENTIFICATION_IF"></span>


大多数驱动程序不会涉及到身份验证或识别问题，而是将此任务留给各个服务。 在访问管理中，驱动程序可能会涉及到身份验证或标识处理的一种情况。 在这种情况下，通常通过调用安全引用监视器来处理身份验证步骤。 身份验证和标识信息通常由操作系统由安全令牌跟踪，这是一个用于封装给定线程或进程的安全凭据的内部数据结构。

 

 




