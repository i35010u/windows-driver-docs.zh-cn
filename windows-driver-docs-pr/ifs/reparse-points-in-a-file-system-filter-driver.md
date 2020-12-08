---
title: 重新分析点的安全注意事项
description: 文件系统筛选器驱动程序的安全注意事项
keywords:
- 安全 WDK 文件系统，重新分析点
- 重新分析点 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8098d1dddf9d3952d64e3f180684fc71083a07b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831443"
---
# <a name="security-considerations-for-reparse-points"></a>重新分析点的安全注意事项


处理重新分析点的筛选器驱动程序必须知道应用程序可能会创建无效的重新分析点的风险。 若要确保最严格的安全性，处理重新分析点的驱动程序必须确保重新分析点本身的数据内容是可验证的，无论是通过安全校验和、加密内容还是某些其他确保无效重新分析点无法由无特权应用程序创建的机制。 例如，筛选器驱动程序可能要求使用应用程序 (或本地安全机构（例如) 和驱动程序）之间共享的密码来加密其重新分析点，以确保重新分析点的数据内容有效。

否则，恶意应用程序可能会创建具有无效重新分析点信息的重新分析点。 在这种情况下，文件系统筛选器驱动程序必须准备好处理无效的重新分析点数据，包括自引用数据 (创建可能导致某种溢出的引用循环，例如) 、数据溢出问题和无效数据内容。

 

 




