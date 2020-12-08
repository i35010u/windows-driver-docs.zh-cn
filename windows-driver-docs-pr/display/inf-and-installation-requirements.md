---
title: INF 和安装要求
description: INF 和安装要求
keywords:
- INF 文件 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22f58c3a455854d0a00aaa82f489d44cd5080cc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839307"
---
# <a name="inf-and-installation-requirements"></a>INF 和安装要求


## <span id="ddk_inf_and_installation_requirements_gg"></span><span id="DDK_INF_AND_INSTALLATION_REQUIREMENTS_GG"></span>


必须使用 INF 文件安装基于 NT 的操作系统显示和视频微型端口驱动程序。 若要确保正确初始化与视频驱动程序关联的所有注册表项，必须由系统提供的显示类安装程序解释此 INF，并将其标记为 **class = display**。

 

 





