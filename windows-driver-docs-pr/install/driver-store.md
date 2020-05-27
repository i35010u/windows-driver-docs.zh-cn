---
title: 驱动程序存储
description: 驱动程序存储
ms.assetid: 17abe3a4-0663-4b8b-8072-2171b4cedbe4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ceb5f6c822e6383983f2866db7f3a588e7b56779
ms.sourcegitcommit: 9111f8ebcefc41d3a10e8db241d45003a79bec56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864707"
---
# <a name="driver-store"></a>驱动程序存储

从 Windows Vista 开始，驱动程序存储区是一组受信任的收件箱和第三方[驱动程序包](driver-packages.md)。 操作系统将此集合保留在本地硬盘上的安全位置。 对于设备，只能安装驱动程序存储中的驱动程序包。

将驱动程序包复制到驱动程序存储区时，会复制其所有文件。 这[包括 inf 文件和 inf](overview-of-inf-files.md)文件引用的所有文件。 驱动程序包中的所有文件都被视为设备安装中的关键文件。 INF 文件必须引用设备安装所需的所有文件，以便这些文件位于驱动程序存储区中。 如果 INF 文件引用了驱动程序包中未包含的文件，则不会将驱动程序包复制到该存储中。

将驱动程序包复制到驱动程序存储区的过程称为 "*暂存*"。 必须将驱动程序包*暂存*到驱动程序存储区，然后才能使用包安装任何设备。 因此，驱动程序暂存和设备安装是单独的操作。

通过验证和验证，将驱动程序包暂存到驱动程序存储区。

## <a name="verifying-the-driver-package-integrity"></a>验证驱动程序包完整性

软件完整性已成为独立硬件供应商（Ihv）和原始设备制造商（Oem）的头等大事。 与 Internet 上的恶意软件增加相关，这些客户希望确保其软件未被篡改或损坏。

在将驱动程序包复制到驱动程序存储区之前，操作系统首先验证数字签名是否正确。 有关数字签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

## <a name="validating-the-driver-package"></a>验证驱动程序包

操作系统通过以下方式验证驱动程序包：

- 当前用户必须有权安装驱动程序包。
- 驱动程序包的[INF 文件](overview-of-inf-files.md)语法正确，并且 INF 文件引用的所有文件都存在于驱动程序包中。

驱动程序包通过完整性和语法检查后，会将其复制到驱动程序存储区。 之后，操作系统使用驱动程序包自动安装新设备，而无需用户交互。

文件暂存到驱动程序存储区后，不应以任何方式删除或修改它们。 此外，不应将新文件添加到暂存过程之外的驱动程序存储中。 这包括通过编程调用直接添加、删除或修改的文件，或者间接通过 INF 指令进行处理，稍后将对其进行处理。
