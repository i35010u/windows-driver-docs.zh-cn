---
title: 准备用于 NDIS 调试
description: 准备用于 NDIS 调试
ms.assetid: 9a23cc3a-5940-46c3-928f-7fac46dfaba2
keywords:
- NDIS 调试，安装程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7fbe07eac5153ee538c0bd540be3f6586b94d90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525156"
---
# <a name="preparing-for-ndis-debugging"></a>准备用于 NDIS 调试


若要调试 NDIS 组件，在目标计算机上需要 Ndis.sys 经检查的版本。 但是，而不是安装整个检查生成操作系统，可以将复制到否则为免费生成操作系统上 Ndis.sys 的经检查的版本。 将 Ndis.sys 的经检查的版本复制到目标计算机之前，必须禁用 Windows 文件保护 (WFP)。 若要确保 WFP 已禁用，请在安全模式下启动操作系统。

在 Microsoft 符号存储区上公开提供了 NDIS 符号。 有关如何访问此选项的详细信息，请参阅[Microsoft 公共符号](microsoft-public-symbols.md)。

 

 





