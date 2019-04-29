---
title: 配置支持发布签名的计算机
description: 配置支持发布签名的计算机
ms.assetid: 90115bb8-6ca0-4c08-b69c-f3f5388d3ff6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69c6bb487c33a22f3fd946c1fc2d58be115c6d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366175"
---
# <a name="configuring-a-computer-to-support-release-signing"></a>配置支持发布签名的计算机


在计算机上安装已发布签名驱动程序包之前，请执行以下步骤来配置计算机以支持版本签名：

-   禁用 TESTSIGNING 启动配置选项。 有关此选项的详细信息，请参阅[TESTSIGNING 启动配置选项](the-testsigning-boot-configuration-option.md)。

-   启用代码完整性事件日志记录和审核系统，以帮助在已发布签名驱动程序安装和加载过程中解决问题。 有关详细信息，请参阅[启用代码完整性事件日志记录和审核系统](enabling-code-integrity-event-logging-and-system-auditing.md)。

在计算机重新配置为启用版本签名后，重新启动计算机，更改才能生效。

 

 





