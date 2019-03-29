---
title: 设置受保护输出的保护级别
description: 设置受保护输出的保护级别
ms.assetid: 2f041190-8001-4e79-8398-8b642884f751
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1423974d09b271acc21b8d2781aa814bb2e5fbaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565459"
---
# <a name="setting-the-protection-level-for-a-protected-output"></a>设置受保护输出的保护级别


OPM 配置可以在受保护的输出设置保护类型的保护级别。 若要设置的保护级别，显示微型端口驱动程序的[ **DxgkDdiOPMConfigureProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559701)函数接收指向[ **DXGKMDT\_OPM\_配置\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560849)结构**guidSetting**成员设置为 DXGKMDT\_OPM\_集\_保护\_级别 GUID 和**abParameters**成员设置为一个指向[ **DXGKMDT\_OPM\_设置\_保护\_级别\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff560921)结构，它指定到保护组和要设置的保护级别的类型。 可以为所指示的保护类型设置以下保护级别：

-   有关 DXGKMDT\_OPM\_PROTECTION\_类型\_中指定的 ACP **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数中的保护级别值之一[ **DXGKMDT\_OPM\_ACP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560834)枚举中只能指定**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

-   有关 DXGKMDT\_OPM\_保护\_类型\_中指定 CGMSA **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数中的保护级别值之一[ **DXGKMDT\_OPM\_CGMSA** ](https://msdn.microsoft.com/library/windows/hardware/ff560846)枚举可以在中指定**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

-   有关 DXGKMDT\_OPM\_PROTECTION\_类型\_HDCP 或 DXGKMDT\_OPM\_保护\_类型\_COPP\_兼容\_中指定 HDCP **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_之一的参数保护级别值从[ **DXGKMDT\_OPM\_HDCP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560878)中只能指定枚举**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

-   有关 DXGKMDT\_OPM\_保护\_类型\_中指定 DPCP **ulProtectionType** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数中的保护级别值之一[ **DXGKMDT\_OPM\_DPCP\_保护\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff560861)枚举中只能指定**ulProtectionLevel** DXGKMDT 成员\_OPM\_设置\_保护\_级别\_参数。

**请注意**   DXGKMDT\_OPM\_设置\_保护\_级别\_ACCORDING\_TO\_CSS\_DVD GUID 是新增功能Windows 7 和用来指示驱动程序应根据新的 CSS 规则启用 HDCP。 设置 DXGKMDT\_OPM\_设置\_保护\_级别\_ACCORDING\_TO\_CSS\_DVD 命令等同于设置现有 DXGKMDT\_OPM\_设置\_保护\_除该 DXGKMDT 级别命令\_OPM\_设置\_保护\_级别\_根据\_TO\_CSS\_DVD 具有绝对无需启用请求的保护。

 

 

 





