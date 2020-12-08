---
title: 多页扫描和 TWAIN
description: 多页扫描和 TWAIN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07b0280b7734439597ba35c98ee258ae2d20c28f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827127"
---
# <a name="multipage-scanning-and-twain"></a>多页扫描和 TWAIN





从 Windows XP 开始，如果所有扫描的页的长度相同，TWAIN 兼容层都支持从滚动馈送设备进行多页扫描。 这样做的原因是，TWAIN 仅在第一页上从调用应用程序获取有关页面长度的信息。 TWAIN 不要求调用应用程序要求在页面之间提供图像信息。 而且，TWAIN 将从应用程序收到的有关第一页的信息应用于所有后续页面。

 

 




