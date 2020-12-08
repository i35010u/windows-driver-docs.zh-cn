---
title: Bug 检查 0xC0000221 STATUS_IMAGE_CHECKSUM_MISMATCH
description: STATUS_IMAGE_CHECKSUM_MISMATCH bug 检查的值为0xC0000221。 这表明驱动程序或系统 DLL 已损坏。
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
ms.openlocfilehash: dd22889b6c82bb84f04d4dd566c4b7eb34f9b16f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833713"
---
# <a name="bug-check-0xc0000221-status_image_checksum_mismatch"></a>Bug 检查0xC0000221：状态 \_ 映像 \_ 校验和 \_ 不匹配


状态 \_ 图像 \_ 校验和 \_ bug 检查的值为0xC0000221。 这表明驱动程序或系统 DLL 已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="status_image_checksum_mismatch-parameters"></a>状态 \_ 图像 \_ 校验和 \_ 参数不匹配


<a name="cause"></a>原因
-----

此 bug 检查驱动程序或其他系统文件中出现严重错误。 文件头校验和与预期的校验和不匹配。

这也可能是由文件的 i/o 路径中的硬件错误 (磁盘错误、有故障的 RAM 或损坏的页面文件) 导致的。

<a name="resolution"></a>解决方法
----------

若要解决此错误，请运行紧急恢复磁盘 (ERD) ，并允许系统修复或替换系统分区上丢失或损坏的驱动程序文件。

你还可以在现有的 Windows 副本上运行就地升级。 这会保留所有注册表设置和配置信息，但会替换所有系统文件。 如果以前应用了任何 Service Pack 和/或修补程序，则需要按照 (最新的 Service Pack 的适当顺序重新安装它们，然后按最初安装时的顺序安装任何 Service Pack 修补程序（如果适用）) 。

如果 bug 检查消息中的特定文件已被损坏，则可以尝试手动替换该文件。 如果使用 FAT 格式化系统分区，则可以从 MS-DOS 启动盘开始，并将文件从原始源复制到硬盘上。 如果使用的是双启动计算机，则可以启动到其他操作系统并替换该文件。

如果要使用 NTFS 分区替换单启动系统上的文件，则需要重新启动系统，在操作系统 **加载** 器菜单中按 F8，并 **使用命令提示符选择安全模式**。 从此处将文件的新版本从原始源复制到硬盘上。 如果在安全模式下将该文件用作系统启动过程的一部分，则需要使用恢复控制台启动计算机才能访问该文件。 如果这些方法失败，请尝试重新安装 Windows，然后从备份还原系统。

**注意**   如果产品 CD 中的原始文件的文件扩展名以 \_ (下划线) 结尾，则需要对该文件进行解压缩，然后才能使用该文件。 恢复控制台的 **复制** 命令会自动检测压缩的文件，并在将其复制到目标位置时对它们进行扩展。 如果使用安全模式访问驱动器，请使用 **Expand** 命令解压缩文件并将其复制到目标文件夹。 可以在安全模式下使用命令行环境中的 **Expand** 命令。

 

**解决磁盘错误问题：** 磁盘错误可能是文件损坏的原因。 运行 **Chkdsk/f/r** 来检测和解决任何文件系统结构损坏。 在系统分区上开始磁盘扫描之前，必须重启系统。

**解决 RAM 问题：** 如果在 RAM 添加到系统后立即发生错误，则页面文件可能已损坏，或者新 RAM 本身可能有故障或不兼容。

**确定新添加的 RAM 是否会导致 bug 检查**

1.  将系统恢复为原始 RAM 配置。

2.  使用恢复控制台访问包含页面文件的分区，并删除 pagefile.sys 的文件。

3.  在仍处于恢复控制台中时，请在包含分页文件的分区上运行 **Chkdsk/r** 。

4.  重新启动系统。

5.  将页面文件设置为添加的 RAM 量的最佳级别。

6.  关闭系统并添加 RAM。

    新 RAM 必须满足系统制造商对速度、奇偶校验和类型 (的规范，即 fast page 模式 (PHP-FPM) 与扩展数据输出 (克瓦语) 与同步动态随机存取内存 (SDRAM) # A7。 尝试尽可能将新 RAM 与现有的已安装 RAM 匹配。 RAM 可以有许多不同的容量，更重要的是 (单内联内存模块（SIMM--或双内联内存模块--DIMM) 的不同格式。 电气联系人可以是金或 tin，因此，不太明智地混合这些触点类型。

如果在重新安装新 RAM 后遇到相同的错误消息，请运行系统制造商提供的硬件诊断，尤其是内存扫描器。 有关这些过程的详细信息，请参阅计算机的用户手册。

当你可以再次登录到系统时，请查看事件查看器中的系统日志，以获取可帮助查明导致错误的设备或驱动程序的其他错误消息。

禁用 BIOS 的内存缓存还可能会解决此错误。

 

 




