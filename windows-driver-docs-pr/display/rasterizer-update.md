---
title: 光栅器更新
description: 光栅器更新
ms.assetid: 0b7db462-2b04-42e1-baa0-ec9070741c1d
keywords:
- 光栅器 WDK Direct3D
- 生产光栅器 WDK Direct3D
- 参考光栅器 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05aa0ab41457b0675fa10e5790fe0c1b182fcf38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378440"
---
# <a name="rasterizer-update"></a>光栅器更新


## <span id="ddk_rasterizer_update_gg"></span><span id="DDK_RASTERIZER_UPDATE_GG"></span>


参考光栅器已提取到单独的 DLL，若要启用其他 WHQL 测试的正常 DirectX 交付周期以异步方式添加 （每季度是典型）。 已更新为支持所有添加到内核中或作为需要实现的保证的一致性的扩展 API 的光栅器级别操作。

生产光栅器可能不会更新以支持这些技术，由于在顶点级别的环境映射可能会比要快在像素级别时在软件中运行。

此光栅器很可能要升级在标识的关键用例的性能方面。

 

 





