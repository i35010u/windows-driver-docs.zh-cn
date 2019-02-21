---
title: 增强的存储证书管理工具的概述
description: 增强的存储证书管理工具的概述
ms.assetid: 963e6510-d62f-421f-9c3d-781092f98969
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89869f3ae2d630381283bcb63f13915e0ff7de92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522279"
---
# <a name="overview-of-the-enhanced-storage-certificate-management-tool"></a>增强的存储证书管理工具的概述


从 Windows 7 开始，操作系统提供*增强存储*连接到计算机的 USB 存储设备的基础结构。 此基础结构基于 IEEE 1667 标准进行设备身份验证和通信的 1.1 版。 有关 IEEE 1667 标准的概述，请参阅 IEEE 1667 标准术语和定义。

增强型存储证书管理工具可管理此工具提供了以下功能是符合 IEEE 1667 标准的 USB 存储设备中的 ASC 存储区中的证书：

-   从主机到 ASC 应用商店中导入证书。

    证书可以添加或替换任何符合 IEEE 1667 标准的 USB 存储设备的 ASC 存储区中 （除 ASCm 证书）。

    有关详细信息，请参阅[通过增强的存储证书管理工具导入证书](importing-certificates-by-using-the-enhanced-storage-certificate-manag.md)。

-   将证书从 ASC 存储导出到文件。

    一旦导出，这些证书可以导入到其他符合 IEEE 1667 标准的 USB 存储设备上的 ASC 存储区。

-   从 ASC 存储中删除证书。

    单个证书可以从存储中删除 ASC，除 ASCm 和 PCp 证书。

-   清除所有证书从 ASC 商店 ASCm 和 PCp 证书除外。

-   初始化 ASC 存储恢复到其初始状态。

    这将清除从 ASC 商店 ASCm 证书除外的所有证书。

-   列出 ASC 存储中的证书。

**请注意**  不能添加、 删除或使用此工具删除 ASCm 证书。

 

增强型存储证书管理工具执行这些函数通过 USB 存储设备上 act 发出 IEEE 1667 命令。 通过唯一卷名称采用以下格式指定每个 USB 存储设备：

```
\\?\USB_Hardware_ID{GUID}
```

其中：

-   *USB\_硬件\_ID* ，它是硬件或兼容的 USB 存储设备的标识符 (ID)。 有关这些 Id 的详细信息，请参阅[USB 设备的标识符](https://msdn.microsoft.com/library/windows/hardware/ff546284)。

-   表示设备实例的 GUID。

例如，下面是 USB 存储设备卷名称的一个示例：

```
\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}
```

**请注意**  若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，键入**EhStorCertMgrCmd /List**在命令行。

 

若要将 IEEE 1667 命令发送到在 USB 存储设备行为，用户可能需要进行身份验证来使用该设备。 身份验证基于 PCp 证书和私钥是可供用户使用。 如果用户不具有正确的 PCp 证书和私钥，用户不会通过增强型存储证书管理工具进行预配设备的访问权限。

 

 





