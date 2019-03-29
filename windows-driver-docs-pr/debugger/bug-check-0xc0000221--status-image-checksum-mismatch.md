---
title: Bug 检查 0xC0000221 STATUS_IMAGE_CHECKSUM_MISMATCH
description: STATUS_IMAGE_CHECKSUM_MISMATCH bug 检查具有 0xC0000221 值。 这表示一个驱动程序或系统 DLL 具有已损坏。
ms.assetid: d0baccb0-51a2-45c7-ae08-507217d0ac96
keywords:
- Bug 检查 0xC0000221 STATUS_IMAGE_CHECKSUM_MISMATCH
- STATUS_IMAGE_CHECKSUM_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- STATUS_IMAGE_CHECKSUM_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7baae75919a0e07e1deabb99a743e6b6f089c793
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564143"
---
# <a name="bug-check-0xc0000221-statusimagechecksummismatch"></a>Bug 检查 0xC0000221：状态\_图像\_校验和\_不匹配


状态\_图像\_校验和\_不匹配错误检查的值为 0xC0000221。 这表示一个驱动程序或系统 DLL 具有已损坏。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="statusimagechecksummismatch-parameters"></a>状态\_图像\_校验和\_不匹配参数


<a name="cause"></a>原因
-----

此 bug 检查从驱动程序或其他系统文件中的严重错误的结果。 文件标头校验和与预期校验和不匹配。

这也可能引起的文件 （磁盘错误、 有故障的 RAM 或已损坏的页面文件） 的 I/O 路径中的硬件故障。

<a name="resolution"></a>分辨率
----------

若要更正此错误，运行紧急情况下恢复磁盘 (ERD)，并允许系统在修复或替换系统分区上的丢失或损坏驱动程序文件。

此外可以通过 Windows 的现有副本运行就地升级。 这会保留所有的注册表设置和配置信息，但会替换所有系统文件。 如果先前已应用任何 Service Pack 和/或修补程序，您需要重新之后以适当顺序 （最新 Service Pack，然后在其中它们最初安装，如果适用的顺序的任何 Service Pack 修补程序） 安装它们。

如果为损坏导致的 bug 检查消息中标识特定的文件，则可以尝试手动替换该单个文件。 如果使用 FAT 格式化是系统分区，您可以启动从 MS-DOS 启动磁盘和的文件复制到硬盘上的原始源。 如果你有一双引导计算机，可以启动到其他操作系统，并替换该文件。

如果你想要启动单个系统上的文件替换为在 NTFS 分区，需要重启系统，请在操作系统中按 F8**加载程序**菜单，然后选择**安全模式下使用命令提示符**。 在这里，将复制到硬盘上的原始源中的文件的最新版本。 如果该文件用作在安全模式下在系统启动过程的一部分，您需要启动计算机才能访问该文件使用恢复控制台。 如果这些方法都失败，请尝试重新安装 Windows，然后从备份还原系统。

**请注意**  产品 CD 中的原始文件是否以结尾的文件扩展名的\_（下划线），需要为未压缩，然后才能使用该文件。 恢复控制台**复制**命令会自动检测压缩的文件，并根据它们复制到目标位置扩展它们。 如果使用安全模式下访问驱动器，使用**展开**命令来解压缩并将文件复制到目标文件夹。 可以使用**展开**命令，在安全模式下在命令行环境。

 

**解决磁盘错误问题：** 磁盘错误可能是损坏的文件的源。 运行**Chkdsk /f /r**检测和解决任何文件系统结构损坏。 系统分区上的磁盘扫描开始之前，必须重新启动系统。

**在解决内存问题：** 如果 RAM 已添加到系统后立即发生错误，可能已损坏的页面文件或新 RAM 本身可能发生故障或不兼容。

**若要确定新添加的 RAM 导致的 bug 检查**

1.  返回到原始 RAM 配置系统。

2.  使用恢复控制台访问包含分页文件的分区并删除文件 pagefile.sys。

3.  在仍在恢复控制台中，运行**Chkdsk /r**包含分页文件的分区上。

4.  重新启动系统。

5.  设置为以最佳水平所添加的 RAM 量的分页文件。

6.  关闭系统并添加 RAM。

    新的 RAM 必须满足的速度、 校验和类型 （即，快速页模式 (FPM) 与扩展数据输出 （克瓦语），而不是同步的动态随机存取内存 (SDRAM)） 的系统制造商的规格。 尝试尽可能接近地匹配到现有的已安装 RAM 的新 RAM。 RAM 会出现在许多不同的容量，并更重要的是，在不同的格式 （单个内联内存模块-SIMM-或双内联内存模块-内存）。 金级或 tin 电气联系人可以是并不是比较明智的做法混用这些联系人类型。

如果重新安装新的 RAM 后遇到相同的错误消息，运行硬件诊断提供的系统制造商，尤其是内存扫描程序。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。

时你可以登录到系统试，请检查事件查看器中的系统日志可能有助于确定该设备或导致错误的驱动程序的其他错误消息。

禁用内存中缓存的 bios 还可能会解决此错误。

 

 




