---
title: 增强的存储证书管理工具概述
description: 增强的存储证书管理工具概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ef026987afefdbe33c9ce1dc2a355dcff42a735
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784013"
---
# <a name="overview-of-the-enhanced-storage-certificate-management-tool"></a>增强的存储证书管理工具概述


从 Windows 7 开始，操作系统为连接到计算机的 USB 存储设备提供 *增强的存储* 基础结构。 此基础结构基于适用于设备身份验证和通信的 IEEE 1667 标准1.1 版。 有关 IEEE 1667 标准的概述，请参阅 IEEE 1667 标准术语和定义。

增强的存储证书管理工具管理兼容 IEEE 1667 标准的 USB 存储设备中 ASC 存储区中的证书。该工具提供了以下功能：

-   将证书从主机导入到 ASC 存储区。

    除了符合 IEEE 1667 标准的任何 USB 存储设备的 ASC 存储区中的 ASCm 证书) 之外，还可以添加或替换证书 (。

    有关详细信息，请参阅 [通过增强的存储证书管理工具导入证书](importing-certificates-by-using-the-enhanced-storage-certificate-manag.md)。

-   从 ASC 存储区将证书导出到文件。

    一旦导出这些证书，就可以将这些证书导入到符合 IEEE 1667 标准的其他 USB 存储设备上的 ASC 存储区中。

-   从 ASC 存储区中删除证书。

    除了 ASCm 和 PCp 证书，可以从 ASC 存储区中删除单个证书。

-   清除 ASC 存储区中的所有证书（ASCm 和 PCp 证书除外）。

-   将 ASC 存储初始化回其初始状态。

    这会清除 ASC 存储区中的所有证书（ASCm 证书除外）。

-   列出 ASC 存储区中的证书。

**注意**  使用此工具无法添加、删除或删除 ASCm 证书。

 

增强的存储证书管理工具通过向 USB 存储设备上的 ACT 发出 IEEE 1667 命令来执行这些功能。 每个 USB 存储设备是通过采用以下格式的唯一卷名称指定的：

```
\\?\USB_Hardware_ID{GUID}
```

其中：

-   *USB \_硬件 \_ id* ，是 USB 存储设备的硬件或兼容标识符 (ID) 。 有关这些 Id 的详细信息，请参阅 [USB 设备的标识符](../install/identifiers-for-usb-devices.md)。

-   表示设备实例的 GUID。

例如，以下是 USB 存储设备的卷名称的示例：

```
\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}
```

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令行中键入 **EhStorCertMgrCmd/list** 。

 

为了向 USB 存储设备上的 ACT 发出 IEEE 1667 命令，可能需要对用户进行身份验证才能使用该设备。 身份验证基于用户可用的 PCp 证书和私钥。 如果用户没有正确的 PCp 证书和私钥，用户将无法访问设备以通过增强的存储证书管理工具进行设置。

 

