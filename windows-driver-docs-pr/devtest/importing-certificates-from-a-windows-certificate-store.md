---
title: 从 Windows 证书存储中导入证书
description: 从 Windows 证书存储中导入证书
ms.assetid: abdf19c7-2cea-4af3-8a86-37fc4a9e7c3d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 125d944c7888b59b867d3a14f4767bfe09ddd852
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533752"
---
# <a name="importing-certificates-from-a-windows-certificate-store"></a>从 Windows 证书存储中导入证书


增强型存储证书管理工具可用于从专用证书存储在计算机中的证书导入到 IEEE 1667 合规 USB 存储设备。

若要从专用证书存储中导入证书，必须指定证书名称使用 **-存储**的参数[ **/add** ](enhstor-add-switch.md)和[**/替换**](-replace-switch.md)增强存储证书管理工具的开关。 该工具将搜索所有指定的证书将私有证书存储和 (如果找到) 将其导入到指定的 USB 存储设备。

**请注意**  该工具会不从导入证书的 Windows 根证书存储。

 

 

 





