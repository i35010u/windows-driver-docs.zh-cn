---
title: Wi-Fi 直接打印
description: Windows 8.1 和更高版本的 Windows 支持通过 Wi-fi Direct （WFD）打印。
ms.assetid: B2FC1293-F9E4-43A4-84BF-21EF8C3D27E0
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: e5047730ad7ba5a80785ff4b654c5b55e606c19b
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793737"
---
# <a name="wi-fi-direct-printing"></a>Wi-Fi 直接打印

Windows 8.1 和更高版本的 Windows 支持通过 Wi-fi Direct （WFD）打印。

实现 Windows Wi-fi Direct 支持打印的打印设备必须实现以下各项：

- Wi-fi 直接垂直配对

- 物理设备中所有逻辑设备的匹配容器 ID

- WSD/WS 打印

本主题中使用的定义及其子主题：

| 术语 | 说明 |
|--|--|
| WFD | WLAN Direct |
| DAF | 设备关联框架 |
| 转移 | 设备关联服务 |
| GO | 组所有者 |
| PBC | 推送按钮连接 |

[Wi-fi 直接打印概述](wfd-overview.md)中介绍了有关 Wi-fi direct 打印支持的一般信息。 有关如何实现 Wi-fi 直接打印的详细信息，请参阅[Wi-fi Direct 打印实现](wfd-implementation.md)。

## <a name="certification-requirements"></a>认证要求

此功能没有任何新的认证要求。 有关适用的现有要求，请参阅下面的[相关文档](#related-documents)。

## <a name="hck-requirements"></a>HCK 要求

如果实现，设备必须具有 wi-fi Direct 证书。

打印设备的所有现有证书要求都适用，包括在所有可用传输中运行适用的 HCK 测试的要求。 如果有任何更改，合作伙伴应始终引用 Windows 证书团队发布的官方认证要求文档。

> [!NOTE]
> Wi-fi 联盟认证要求适用于 Wi-fi Direct。 Wi-fi 联盟 Wi-fi Direct 服务是单独的规范，在目前 Windows 中不受支持。

## <a name="related-documents"></a>相关文档

[容器 ID 概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)

[Pnp-x： Windows 规范即插即用扩展](https://docs.microsoft.com/previous-versions/gg463082(v=msdn.10))

[Wi-fi 联盟-wi-fi Direct 工业白皮书](https://www.wi-fi.org)
