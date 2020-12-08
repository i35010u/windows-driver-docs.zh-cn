---
title: 配置支持发布签名的计算机
description: 配置支持发布签名的计算机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37fd118ceede3316d68441c336f93caf0f5e679d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782969"
---
# <a name="configuring-a-computer-to-support-release-signing"></a>配置支持发布签名的计算机


在计算机上安装发布签名的驱动程序包之前，请按照以下步骤将计算机配置为支持版本签名：

-   禁用 TESTSIGNING Boot 配置选项。 有关此选项的详细信息，请参阅 [TESTSIGNING Boot Configuration 选项](the-testsigning-boot-configuration-option.md)。

-   启用代码完整性事件日志记录和系统审核，以便在安装和加载发布签名驱动程序时解决问题。 有关详细信息，请参阅 [启用代码完整性事件日志记录和系统审核](enabling-code-integrity-event-logging-and-system-auditing.md)。

重新配置计算机以启用发布签名后，请重新启动计算机以使更改生效。

 

 





